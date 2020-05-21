#
#  TOPPERS/ASP Kernel
#      Toyohashi Open Platform for Embedded Real-Time Systems/
#      Advanced Standard Profile Kernel
# 
#  Copyright (C) 2000-2003 by Embedded and Real-Time Systems Laboratory
#                              Toyohashi Univ. of Technology, JAPAN
#  Copyright (C) 2006-2016 by Embedded and Real-Time Systems Laboratory
#              Graduate School of Information Science, Nagoya Univ., JAPAN
# 
#  上記著作権者は，以下の(1)〜(4)の条件を満たす場合に限り，本ソフトウェ
#  ア（本ソフトウェアを改変したものを含む．以下同じ）を使用・複製・改
#  変・再配布（以下，利用と呼ぶ）することを無償で許諾する．
#  (1) 本ソフトウェアをソースコードの形で利用する場合には，上記の著作
#      権表示，この利用条件および下記の無保証規定が，そのままの形でソー
#      スコード中に含まれていること．
#  (2) 本ソフトウェアを，ライブラリ形式など，他のソフトウェア開発に使
#      用できる形で再配布する場合には，再配布に伴うドキュメント（利用
#      者マニュアルなど）に，上記の著作権表示，この利用条件および下記
#      の無保証規定を掲載すること．
#  (3) 本ソフトウェアを，機器に組み込むなど，他のソフトウェア開発に使
#      用できない形で再配布する場合には，次のいずれかの条件を満たすこ
#      と．
#    (a) 再配布に伴うドキュメント（利用者マニュアルなど）に，上記の著
#        作権表示，この利用条件および下記の無保証規定を掲載すること．
#    (b) 再配布の形態を，別に定める方法によって，TOPPERSプロジェクトに
#        報告すること．
#  (4) 本ソフトウェアの利用により直接的または間接的に生じるいかなる損
#      害からも，上記著作権者およびTOPPERSプロジェクトを免責すること．
#      また，本ソフトウェアのユーザまたはエンドユーザからのいかなる理
#      由に基づく請求からも，上記著作権者およびTOPPERSプロジェクトを
#      免責すること．
# 
#  本ソフトウェアは，無保証で提供されているものである．上記著作権者お
#  よびTOPPERSプロジェクトは，本ソフトウェアに関して，特定の使用目的
#  に対する適合性も含めて，いかなる保証も行わない．また，本ソフトウェ
#  アの利用により直接的または間接的に生じたいかなる損害に関しても，そ
#  の責任を負わない．
# 
#  $Id: Makefile 773 2017-01-18 23:47:30Z ertl-hiro $
# 

#
#  ターゲットの指定（Makefile.targetで上書きされるのを防ぐため）
#
all:

#
#  ターゲット略称の定義
#
TARGET = v850_gcc

#
#  プログラミング言語の定義
#
SRCLANG = c
ifeq ($(SRCLANG),c)
	LIBS = -lc -lgcc
endif
ifeq ($(SRCLANG),c++)
	USE_CXX = true
	CXXLIBS = -lstdc++ -lm -lc
	CXXRTS = cxxrt.o newlibrt.o
endif

#
#  ソースファイルのディレクトリの定義
#
SRCDIR = ../..

#  mruby 関係の設定
MRUBY_SRC_DIR = $(SRCDIR)/../mruby_asp3
#MRUBY_LIB = $(MRUBY_SRC_DIR)/build/ARM/lib/libmruby.a -lm
MRUBY_LIB = $(MRUBY_SRC_DIR)/build/V850/lib/libmruby.a -lm

# mruby compiler and test driver
ifeq ($(OS),Windows_NT)
MRBC = $(MRUBY_SRC_DIR)/bin/mrbc.exe
EXE := $(TARGET).exe
else
MRBC = $(MRUBY_SRC_DIR)/bin/mrbc
EXE := $(TARGET)
endif
#
#  オブジェクトファイル名の拡張子の設定
#
OBJEXT = 

#
#  カーネルライブラリ（libkernel.a）のディレクトリ名
#  （カーネルライブラリもmake対象にする時は，空に定義する）
#
KERNEL_LIB = 

#
#  カーネルを関数単位でコンパイルするかどうかの定義
#
KERNEL_FUNCOBJS = 

#
#  TECSを外すかどうかの定義
#
OMIT_TECS = 

#
#  トレースログを取得するかどうかの定義
#
ENABLE_TRACE = 

#
#  開発ツール（コンパイラ等）のディレクトリの定義
#
DEVTOOLDIR = 

#
#  ユーティリティプログラムの名称
#
CFG = ruby $(SRCDIR)/cfg/cfg.rb
#
#  TECSインタフェースジェネレータ関係の定義
# tecsgen.rb (ruby + racc)を利用する場合は下記のRUBYLIBとTECSGENの定義を利用する

TECSGEN_DIR = ../../tecsgen
TECSGEN_TOP_DIR = $(TECSGEN_DIR)
#RUBYLIB = $(SRCDIR)/tecsgen/tecsgen
#RUBYLIB = $(SRCDIR)/tecsgen
RUBYLIB = $(TECSGEN_TOP_DIR)
#TECSGEN = $(RUBY) $(TECSGEN_TOP_DIR)/tecsgen.rb -L $(RUBYLIB) -k euc --cpp="$(GCC_TARGET_PREFIX)gcc -E"
TECSGEN = $(RUBY) $(TECSGEN_TOP_DIR)/tecsgen.rb -L $(RUBYLIB) -cpp="$(GCC_TARGET_PREFIX)gcc -E"

ifndef TECSGEN_EXE
    TECSGEN_EXE = $(TECSGEN)
endif

TECSLIB_DIR = $(SRCDIR)/tecs_lib
MRUBY_LIB_DIR = $(SRCDIR)/mruby_lib

PRE_TECSGEN_TARGET =
POST_TECSGEN_TARGET =

#
#  オブジェクトファイル名の定義
#
OBJNAME = asp
ifdef OBJEXT
	OBJFILE = $(OBJNAME).$(OBJEXT)
	CFG1_OUT = cfg1_out.$(OBJEXT)
else
	OBJFILE = $(OBJNAME)
	CFG1_OUT = cfg1_out.exe
endif

#
#  依存関係ファイルを置くディレクトリの定義
#
DEPDIR = deps

#
#  ターゲット依存部のディレクトリの定義
#
TARGETDIR = $(SRCDIR)/target/$(TARGET)

#
#  ターゲット依存の定義のインクルード
#
include $(TARGETDIR)/Makefile.target

#
#  TECS生成ファイルのディレクトリの定義
#
TECSGENDIR = ./gen
ifndef OMIT_TECS
	TECS_TIMESTAMP = tecs.timestamp
	INIT_TECS_COBJ = init_tecs.o
endif

#
#  TECSが生成する定義のインクルード
#
ifndef OMIT_TECS
	GEN_DIR = $(TECSGENDIR)
	-include $(TECSGENDIR)/Makefile.tecsgen
endif

#
#  共通コンパイルオプションの定義
#
COPTS := -g  $(COPTS)
ifndef OMIT_WARNING_ALL
	COPTS := -Wall $(COPTS)
endif
ifndef OMIT_OPTIMIZATION
	COPTS := -O2 $(COPTS)
endif
ifdef OMIT_TECS
	CDEFS := -DTOPPERS_OMIT_TECS $(CDEFS)
endif
CDEFS := $(CDEFS) 
INCLUDES := -I. -I$(SRCDIR)/include $(INCLUDES) -I$(SRCDIR) \
            -I$(MRUBY_SRC_DIR)/include \
	    -I$(TECSGEN_TOP_DIR)/tecs \
	    -I$(TECSGEN_TOP_DIR)/tecs/mruby \
	    -I$(TECSGEN_TOP_DIR)/tecs/TLSFMalloc \
            -I$(TECSGEN_TOP_DIR)/tecs/posix \
            -I$(SRCDIR)/tecs_lib/mindstorms_ev3 \
            -I$(SRCDIR)/tecs_lib/mindstorms_ev3/balancer \
	    -I$(SRCDIR)/tecs_lib/common \

LDFLAGS := $(LDFLAGS) 
LIBS := $(LIBS) $(CXXLIBS)
CFLAGS = $(COPTS) $(CDEFS) $(INCLUDES)

#
#  アプリケーションプログラムに関する定義
#
COMMON_DIR = ../../sdk/common

APPLNAME = tEV3Sample
APPLDIR = .
APPL_CFG = $(APPLNAME).cfg
ifeq ($(RUNNING_BODY_TIRE),big)
    APPL_CDL = $(APPLNAME)_bigtire.cdl
else
    APPL_CDL = $(APPLNAME).cdl
endif

#APPL_DIR = $(APPLDIR) $(SRCDIR)/library
#APPL_ASMOBJS =
ifdef USE_CXX
  APPL_CXXOBJS +=
  APPL_COBJS += $(TECS_COBJS) $(INIT_TECS_COBJ)
else
  APPL_COBJS += $(TECS_COBJS) $(INIT_TECS_COBJ)
endif
#APPL_COBJS += log_output.o t_perror.o strerror.o
APPL_CFLAGS =
APPL_LIBS +=
ifdef APPLDIR
	INCLUDES := $(INCLUDES) -I$(APPLDIR)/$(COMMON_DIR) \
		-I$(APPLDIR)/$(COMMON_DIR)/ev3api/src \
		-I$(APPLDIR)/$(COMMON_DIR)/ev3api/include \
		-I$(TARGETDIR)/platform/include \
		-I$(TARGETDIR)/drivers/common/include \
		-I$(TARGETDIR)/drivers/gpio/include \
		-I$(TARGETDIR)/drivers/uart/include \
		-I$(TARGETDIR)/drivers/brick/include \
		-I$(TARGETDIR)/drivers/motor/include \
		-I$(TARGETDIR)/TLSF-2.4.6/include \
		-I/mnt/c/Users/ykomi/cur/athrill/athrill/trunk/apl/include \
		-I$(TARGETDIR)/pil/include \
		-I$(TARGETDIR)/athrill \
		-I$(APPLDIR)/$(COMMON_DIR)/ev3api $(foreach dir,$(APPLDIR),-I$(dir))
endif
# target/v850_gcc/ev3.h

#APPLNAME = app

APPLDIRS = $(SRCDIR)/OBJ $(COMMON_DIR) $(COMMON_DIR)/ev3api $(COMMON_DIR)/ev3api/include 
APPLDIRS += $(COMMON_DIR)/ev3api/src ../../target/v850_gcc ../../target/v850_gcc/pil/include
APPLDIRS += ../../target/v850_gcc/pil/src
APPLDIRS += ../../target/v850_gcc/platform/src
APPLDIRS += ../../target/v850_gcc/platform/include
APPLDIRS += ../../target/v850_gcc/drivers/gpio/src
APPLDIRS += ../../target/v850_gcc/drivers/gpio/include
APPLDIRS += ../../target/v850_gcc/drivers/brick/src
APPLDIRS += ../../target/v850_gcc/drivers/brick/include
APPLDIRS += ../../target/v850_gcc/drivers/uart/src
APPLDIRS += ../../target/v850_gcc/drivers/uart/include
APPLDIRS += ../../target/v850_gcc/drivers/motor/src
APPLDIRS += ../../target/v850_gcc/drivers/motor/include
APPLDIRS += ../../target/v850_gcc/drivers/common/include
APPLDIRS += ../../target/v850_gcc/TLSF-2.4.6/include ../../target/v850_gcc/TLSF-2.4.6/src
APPLDIRS += ../../target/v850_gcc/athrill
APPLDIRS += ../../../../../../athrill/trunk/apl/include
APPLDIRS += ../../../../../../athrill/trunk/apl/src
#APPL_CFG = app.cfg
APPL_CFG = $(APPLNAME).cfg
#APPL_CDL = app.cdl
#APPL_CDL = $(APPLNAME).cdl
CDEFS += -DTOPPERS_SUPPORT_PROTECT
APPL_LIBS =  -nostartfiles  -lnosys


APPL_DIRS := $(APPLDIRS) $(SRCDIR)/library
APPL_ASMOBJS :=
#ifdef USE_CXX
#	APPL_CXXOBJS := $(APPLNAME).o
#	APPL_COBJS :=
#else
#	APPL_COBJS := $(APPLNAME).o
#endif
APPL_COBJS := $(APPL_COBJS) log_output.o vasyslog.o t_perror.o strerror.o
APPL_COBJS += ev3main.o 
APPL_COBJS += ev3_svc.o
APPL_COBJS += driver_interface_brick.o
APPL_COBJS += brick_dri.o
APPL_COBJS += uart_dri.o
APPL_COBJS += motor_dri.o
APPL_COBJS += gpio_dri.o

APPL_CFLAGS := $(APPL_CFLAGS)
#ifdef APPLDIRS
#	INCLUDES := $(INCLUDES) $(foreach dir,$(APPLDIRS),-I$(dir))
#endif

#EV3RT_SDK_API_DIR	:= ../common/ev3api
EV3RT_SDK_API_DIR	:= $(COMMON_DIR)/ev3api
#include ../common/ev3api/Makefile
include $(COMMON_DIR)/ev3api/Makefile

#
#  システムサービスに関する定義
#
SYSSVC_DIRS := $(TECSGENDIR) $(SRCDIR)/tecs_kernel \
				$(SYSSVC_DIRS) $(SRCDIR)/syssvc
SYSSVC_ASMOBJS := $(SYSSVC_ASMOBJS)
SYSSVC_COBJS := $(SYSSVC_COBJS) \
				 $(CXXRTS)
SYSSVC_CFLAGS := $(SYSSVC_CFLAGS)
INCLUDES := $(INCLUDES) -I$(TECSGENDIR) -I$(SRCDIR)/tecs_kernel

#
#  ターゲットファイル
#
.PHONY: all
ifndef OMIT_TECS
all: tecs
	@$(MAKE) check
#	@$(MAKE) check $(OBJNAME).bin
#	@$(MAKE) check $(OBJNAME).srec
else
all: check
#all: check $(OBJNAME).bin
#all: check $(OBJNAME).srec
endif

##### 以下は編集しないこと #####

#
#  コンフィギュレータに関する定義
#
CFG_TABS := --api-table $(SRCDIR)/kernel/kernel_api.def \
			--symval-table $(SRCDIR)/kernel/kernel_sym.def $(CFG_TABS)
CFG_ASMOBJS := $(CFG_ASMOBJS)
CFG_COBJS := kernel_cfg.o $(CFG_COBJS)
CFG_OBJS := $(CFG_ASMOBJS) $(CFG_COBJS)
CFG2_OUT_SRCS := kernel_cfg.h kernel_cfg.c $(CFG2_OUT_SRCS)
CFG_CFLAGS := -DTOPPERS_CB_TYPE_ONLY $(CFG_CFLAGS)

#
#  カーネルに関する定義
#
#  KERNEL_ASMOBJS: カーネルライブラリに含める，ソースがアセンブリ言語の
#				   オブジェクトファイル．
#  KERNEL_COBJS: カーネルのライブラリに含める，ソースがC言語で，ソース
#				 ファイルと1対1に対応するオブジェクトファイル．
#  KERNEL_LCSRCS: カーネルのライブラリに含めるC言語のソースファイルで，
#				  1つのソースファイルから複数のオブジェクトファイルを生
#				  成するもの．
#  KERNEL_LCOBJS: 上のソースファイルから生成されるオブジェクトファイル．
#
KERNEL_DIRS := $(KERNEL_DIRS) $(SRCDIR)/kernel
KERNEL_ASMOBJS := $(KERNEL_ASMOBJS)
KERNEL_COBJS := $(KERNEL_COBJS)
KERNEL_CFLAGS := $(KERNEL_CFLAGS) -I$(SRCDIR)/kernel

#
#  カーネルのファイル構成の定義
#
include $(SRCDIR)/kernel/Makefile.kernel
ifdef KERNEL_FUNCOBJS
	KERNEL_LCSRCS := $(KERNEL_FCSRCS)
	KERNEL_LCOBJS := $(foreach file,$(KERNEL_FCSRCS),$($(file:.c=)))
else
	KERNEL_CFLAGS := -DALLFUNC $(KERNEL_CFLAGS)
	KERNEL_COBJS := $(KERNEL_COBJS) \
					$(foreach file,$(KERNEL_FCSRCS),$(file:.c=.o))
endif
ifdef OMIT_OFFSET_H
	OFFSET_H =
else
	OFFSET_H = offset.h
endif
ifndef TARGET_OFFSET_TRB
	TARGET_OFFSET_TRB := $(TARGETDIR)/target_offset.trb
endif
ifndef TARGET_KERNEL_TRB
	TARGET_KERNEL_TRB := $(TARGETDIR)/target_kernel.trb
endif
ifndef TARGET_CHECK_TRB
	TARGET_CHECK_TRB := $(TARGETDIR)/target_check.trb
endif
ifndef TARGET_KERNEL_CFG
	TARGET_KERNEL_CFG := $(TARGETDIR)/target_kernel.cfg
endif

#
#  ソースファイルのあるディレクトリに関する定義
#
vpath %.c $(KERNEL_DIRS) $(SYSSVC_DIRS) $(APPL_DIRS) $(SRCDIR)/tecs_lib/mindstorms_ev3 $(SRCDIR)/tecs_lib/common $(TECSGEN_TOP_DIR)/tecs/mruby $(SRCDIR)/library
vpath %.S $(KERNEL_DIRS) $(SYSSVC_DIRS) $(APPL_DIRS)
vpath %.cfg $(APPL_DIRS)
vpath %.cdl $(APPL_DIRS)

#
#  コンパイルのための変数の定義
#
KERNEL_LIB_OBJS = $(KERNEL_ASMOBJS) $(KERNEL_COBJS) $(KERNEL_LCOBJS)
SYSSVC_OBJS = $(SYSSVC_ASMOBJS) $(SYSSVC_COBJS)
APPL_OBJS = $(APPL_ASMOBJS) $(APPL_COBJS) $(APPL_CXXOBJS)
ALL_OBJS = $(START_OBJS) $(APPL_OBJS) $(SYSSVC_OBJS) $(CFG_OBJS) \
											$(END_OBJS) $(HIDDEN_OBJS)
ALL_LIBS = -lkernel $(APPL_LIBS) $(LIBS)
ifdef KERNEL_LIB
	LIBS_DEP = $(KERNEL_LIB)/libkernel.a $(filter %.a,$(LIBS))
	OBJ_LDFLAGS := $(OBJ_LDFLAGS) -L$(KERNEL_LIB)
	REALCLEAN_FILES := libkernel.a $(REALCLEAN_FILES)
else
	LIBS_DEP = libkernel.a $(filter %.a,$(LIBS))
	OBJ_LDFLAGS := $(OBJ_LDFLAGS) -L.
endif

ifdef TEXT_START_ADDRESS
	LDFLAGS := $(LDFLAGS) -Wl,-Ttext,$(TEXT_START_ADDRESS)
endif
ifdef DATA_START_ADDRESS
	LDFLAGS := $(LDFLAGS) -Wl,-Tdata,$(DATA_START_ADDRESS)
endif
ifdef LDSCRIPT
	LDFLAGS := $(LDFLAGS) -Wl,-T,$(LDSCRIPT)
endif

#
#  tecsgenからCプリプロセッサを呼び出す際のオプションの定義
#
TECS_CPP = $(CC) $(CDEFS) $(INCLUDES) $(SYSSVC_CFLAGS) -D TECSGEN -E

#
#  tecsgenの呼出し
#
.PHONY: tecs
tecs $(TECSGEN_SRCS) $(TECS_HEADERS): $(TECS_TIMESTAMP) ;
$(TECS_TIMESTAMP): $(APPL_CDL) $(TECS_IMPORTS)
	$(TECSGEN_EXE) $< -R $(INCLUDES) --cpp "$(TECS_CPP)" -g $(TECSGENDIR)
	touch $(TECS_TIMESTAMP)

#
#  カーネルのコンフィギュレーションファイルの生成
#
cfg1_out.c cfg1_out.db: cfg1_out.timestamp ;
cfg1_out.timestamp: $(APPL_CFG) $(TECS_TIMESTAMP)
	$(CFG) --pass 1 --kernel asp $(INCLUDES) $(CFG_TABS) \
						-M $(DEPDIR)/cfg1_out_c.d $(TARGET_KERNEL_CFG) $<

$(CFG1_OUT): $(START_OBJS) cfg1_out.o $(END_OBJS) $(HIDDEN_OBJS)
	$(LINK) $(CFLAGS) $(LDFLAGS) $(CFG1_OUT_LDFLAGS) -o $(CFG1_OUT) \
						$(START_OBJS) cfg1_out.o $(END_OBJS)

cfg1_out.syms: $(CFG1_OUT)
	$(NM) -n $(CFG1_OUT) > cfg1_out.syms

cfg1_out.srec: $(CFG1_OUT)
	$(OBJCOPY) -O srec -S $(CFG1_OUT) cfg1_out.srec

$(CFG2_OUT_SRCS) cfg2_out.db: kernel_cfg.timestamp ;
kernel_cfg.timestamp: cfg1_out.db cfg1_out.syms cfg1_out.srec
	$(CFG) --pass 2 --kernel asp $(INCLUDES) -T $(TARGET_KERNEL_TRB)

#
#  オフセットファイル（offset.h）の生成規則
#
$(OFFSET_H): offset.timestamp ;
offset.timestamp: cfg1_out.db cfg1_out.syms cfg1_out.srec
	$(CFG) --pass 2 -O --kernel asp $(INCLUDES) -T $(TARGET_OFFSET_TRB) \
				--rom-symbol cfg1_out.syms --rom-image cfg1_out.srec

#
#  カーネルライブラリファイルの生成
#
libkernel.a: $(OFFSET_H) $(KERNEL_LIB_OBJS)
	rm -f libkernel.a
	$(AR) -rcs libkernel.a $(KERNEL_LIB_OBJS)
	$(RANLIB) libkernel.a

#
#  特別な依存関係の定義
#
tBannerMain.o: $(filter-out tBannerMain.o,$(ALL_OBJS)) $(LIBS_DEP)

#
#  全体のリンク
#
$(OBJFILE): $(ALL_OBJS) $(LIBS_DEP)
	$(LINK) $(CFLAGS) $(LDFLAGS) $(OBJ_LDFLAGS) -o $(OBJFILE) \
			$(START_OBJS) $(APPL_OBJS) $(MRUBY_LIB) $(SYSSVC_OBJS) $(CFG_OBJS) \
			$(ALL_LIBS) $(END_OBJS)

#
#  シンボルファイルの生成
#
$(OBJNAME).syms: $(OBJFILE)
	$(NM) -n $(OBJFILE) > $(OBJNAME).syms

#
#  バイナリファイルの生成
#
$(OBJNAME).bin: $(OBJFILE)
	$(OBJCOPY) -O binary -S $(OBJFILE) $(OBJNAME).bin

#
#  Sレコードファイルの生成
#
$(OBJNAME).srec: $(OBJFILE)
	$(OBJCOPY) -O srec -S $(OBJFILE) $(OBJNAME).srec

#
#  エラーチェック処理
#
.PHONY: check
check: check.timestamp ;
check.timestamp: cfg2_out.db $(OBJNAME).syms $(OBJNAME).srec
	$(CFG) --pass 3 --kernel asp -O $(INCLUDES) -T $(TARGET_CHECK_TRB) \
				--rom-symbol $(OBJNAME).syms --rom-image $(OBJNAME).srec
	@echo "configuration check passed"

#
#  simulator実行
#
.PHONY: start
start: 
	#athrill2 -c1 -m $(APLDIR)/memory.txt -d $(APLDIR)/device_config.txt -t -1 asp
	athrill2 -c1 -m ../common/memory.txt -d ../common/device_config.txt -t -1 asp

.PHONY: debug
debug: 
	gdb --args athrill2 -c1 -m ../common/memory.txt -d ../common/device_config.txt -t -1 asp

#
#  コンパイル結果の消去
#
.PHONY: clean
clean:
	rm -f \#* *~ *.o $(DEPDIR)/*.d $(CLEAN_FILES) check.timestamp
	rm -f $(OBJFILE) $(OBJNAME).syms $(OBJNAME).srec $(OBJNAME).bin
	rm -f kernel_cfg.timestamp $(CFG2_OUT_SRCS) cfg2_out.db
	rm -f offset.timestamp $(OFFSET_H)
	rm -f cfg1_out.syms cfg1_out.srec $(CFG1_OUT)
	rm -f cfg1_out.timestamp cfg1_out.c cfg1_out.db
	rm -rf $(TECSGENDIR) $(TECS_TIMESTAMP)
ifndef KERNEL_LIB
	rm -f libkernel.a
endif

.PHONY: cleankernel
cleankernel:
	rm -f $(OFFSET_H) $(KERNEL_LIB_OBJS)
	rm -f $(KERNEL_LIB_OBJS:%.o=$(DEPDIR)/%.d)

.PHONY: cleantecs
cleantecs:
	rm -rf gen
	rm -f $(TECS_TIMESTAMP)

.PHONY: realclean
realclean: clean cleantecs
	rm -f $(REALCLEAN_FILES)


#
#  コンフィギュレータが生成したファイルのコンパイルルールの定義
#
#  コンフィギュレータが生成したファイルは，共通のコンパイルオプション
#  のみを付けてコンパイルする．
#
ALL_CFG_COBJS = $(CFG_COBJS) cfg1_out.o
ALL_CFG_ASMOBJS = $(CFG_ASMOBJS)

$(ALL_CFG_COBJS): %.o: %.c
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(CFG_CFLAGS) $<

$(ALL_CFG_COBJS:.o=.s): %.s: %.c
	$(CC) -S $(CFLAGS) $(CFG_CFLAGS) $<

$(ALL_CFG_ASMOBJS): %.o: %.S
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(CFG_CFLAGS) $<

#
#  依存関係ファイルのインクルード
#
-include $(DEPDIR)/*.d

#
#  開発ツールのコマンド名の定義
#
ifeq ($(TOOL),gcc)
	#
	#  GNU開発環境用
	#
	ifdef GCC_TARGET
		GCC_TARGET_PREFIX = $(GCC_TARGET)-
	else
		GCC_TARGET_PREFIX =
	endif
	CC := $(GCC_TARGET_PREFIX)gcc
	CXX := $(GCC_TARGET_PREFIX)g++
	AS := $(GCC_TARGET_PREFIX)as
	LD := $(GCC_TARGET_PREFIX)ld
	AR := $(GCC_TARGET_PREFIX)ar
	NM := $(GCC_TARGET_PREFIX)nm
	RANLIB := $(GCC_TARGET_PREFIX)ranlib
	OBJCOPY := $(GCC_TARGET_PREFIX)objcopy
	OBJDUMP := $(GCC_TARGET_PREFIX)objdump
endif

ifdef DEVTOOLDIR
	CC := $(DEVTOOLDIR)/$(CC)
	CXX := $(DEVTOOLDIR)/$(CXX)
	AS := $(DEVTOOLDIR)/$(AS)
	LD := $(DEVTOOLDIR)/$(LD)
	AR := $(DEVTOOLDIR)/$(AR)
	NM := $(DEVTOOLDIR)/$(NM)
	RANLIB := $(DEVTOOLDIR)/$(RANLIB)
	OBJCOPY := $(DEVTOOLDIR)/$(OBJCOPY)
	OBJDUMP := $(DEVTOOLDIR)/$(OBJDUMP)
endif

ifdef USE_CXX
	LINK = $(CXX)
else
	LINK = $(CC)
endif

#
#  コンパイルルールの定義
#
$(KERNEL_COBJS): %.o: %.c
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(KERNEL_CFLAGS) $<

$(KERNEL_COBJS:.o=.s): %.s: %.c
	$(CC) -S $(CFLAGS) $(KERNEL_CFLAGS) $<

$(KERNEL_LCOBJS): %.o:
	$(CC) -DTOPPERS_$(*F) -o $@ -c -MD -MP -MF $(DEPDIR)/$*.d \
									$(CFLAGS) $(KERNEL_CFLAGS) $<

$(KERNEL_LCOBJS:.o=.s): %.s:
	$(CC) -DTOPPERS_$(*F) -o $@ -S $(CFLAGS) $(KERNEL_CFLAGS) $<

$(KERNEL_ASMOBJS): %.o: %.S
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(KERNEL_CFLAGS) $<

$(SYSSVC_COBJS): %.o: %.c
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(SYSSVC_CFLAGS) $<

$(SYSSVC_COBJS:.o=.s): %.s: %.c
	$(CC) -S $(CFLAGS) $(SYSSVC_CFLAGS) $<

$(SYSSVC_ASMOBJS): %.o: %.S
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(SYSSVC_CFLAGS) $<

$(APPL_COBJS): %.o: %.c
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(APPL_CFLAGS) $<

$(APPL_COBJS:.o=.s): %.s: %.c
	$(CC) -S $(CFLAGS) $(APPL_CFLAGS) $<

$(APPL_CXXOBJS): %.o: %.cpp
	$(CXX) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(APPL_CFLAGS) $<

$(APPL_CXXOBJS:.o=.s): %.s: %.cpp
	$(CXX) -S $(CFLAGS) $(APPL_CFLAGS) $<

$(APPL_ASMOBJS): %.o: %.S
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $(APPL_CFLAGS) $<

#
#  デフォルトコンパイルルールを上書き
#
%.o: %.c
	@echo "*** Default compile rules should not be used."
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $<

%.s: %.c
	@echo "*** Default compile rules should not be used."
	$(CC) -S $(CFLAGS) $<

%.o: %.cpp
	@echo "*** Default compile rules should not be used."
	$(CXX) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $<

%.s: %.cpp
	@echo "*** Default compile rules should not be used."
	$(CXX) -S $(CFLAGS) $<

%.o: %.S
	@echo "*** Default compile rules should not be used."
	$(CC) -c -MD -MP -MF $(DEPDIR)/$*.d $(CFLAGS) $<
