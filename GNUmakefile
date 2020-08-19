SRCS = \
	src/dbg.c \
	src/lfn.c \
	src/lfnmisc.c \
	src/numfmt.c \
	src/suggest.c \
	src/tbar.c \
	src/treectl.c \
	src/wfassoc.c \
	src/wfchgnot.c \
	src/wfcomman.c \
	src/wfcopy.c \
	src/wfdir.c \
	src/wfdirrd.c \
	src/wfdirsrc.c \
	src/wfdlgs.c \
	src/wfdlgs2.c \
	src/wfdlgs3.c \
	src/wfdos.c \
	src/wfdrives.c \
	src/wfdrop.c \
	src/wfext.c \
	src/wffile.c \
	src/wfinfo.c \
	src/wfinit.c \
	src/wfmem.c \
	src/wfloc.c \
	src/wfprint.c \
	src/wfsearch.c \
	src/wftree.c \
	src/wfutil.c \
	src/winfile.c \
	src/wnetcaps.c

OBJS = $(subst .c,.o,$(SRCS)) src/wfgoto.o src/res.o

CFLAGS = -DUNICODE -DFASTMOVE -DSTRSAFE_NO_DEPRECATE -DWINVER=0x0600 -O2
LIBS = -mwindows -lgdi32 -lcomctl32 -lole32 -lshlwapi -loleaut32 -lversion \
	-static-libgcc -static-libstdc++
TARGET = winfile
ifeq ($(OS),Windows_NT)
TARGET := $(TARGET).exe
endif

.PHONY: all depend clean
.SUFFIXES: .c .cpp .o .res

all : $(TARGET)

$(TARGET) : $(OBJS)
	x86_64-w64-mingw32-g++ -o $@ $(OBJS) $(LIBS)

.c.o :
	x86_64-w64-mingw32-gcc -c $(CFLAGS) -I. $< -o $@

.cpp.o :
	x86_64-w64-mingw32-g++ -c $(CFLAGS) -I. $< -o $@

src/res.o : src/res.rc src/lang/*.rc src/lang/*.dlg
	x86_64-w64-mingw32-windres -DNOWINRES -I. -i src/res.rc -o src/res.o

clean :
	rm -f $(OBJS) $(TARGET)

depend:
	x86_64-w64-mingw32-gcc -E -MM -w src/*.c > Makefile.depends

-include Makefile.depends
