CC = gcc
CFLAGS = -O2
TARGET = PrxEncrypter
ifdef UNIX
FINAL_TARGET = $(TARGET)
else
WIN32 = 1
FINAL_TARGET = $(TARGET).exe
endif
EXTRA_TARGETS = maketree $(FINAL_TARGET)

OBJ = PrxEncrypter

AR = ar
CC = gcc
LD = gcc

ifdef WIN32
MD = mkdir.exe
RM = rm.exe
else
MD = mkdir
RM = rm
endif

INCDIR = \
	src
#	src/zlib

OBJDIRS = \
	$(OBJ)
#	$(OBJ)/zlib

OBJS = \
	$(OBJ)/crypto.o \
	$(OBJ)/kirk_engine.o \
	$(OBJ)/main.o
#	$(OBJ)/zlib.a

CFLAGS = -O2

LDFLAGS = -s

ifdef WIN32
LDFLAGS += -mconsole -mno-cygwin
endif

LIBS =

ifdef WIN32
LIBS = -luser32 -lcomdlg32 -lshell32
endif

all: $(EXTRA_TARGETS)

$(FINAL_TARGET): $(OBJS)
	@echo Linking $@...
	$(LD) $(LDFLAGS) $(OBJS) $(LIBS) -o $@

#$(OBJ)/zlib.a:  \
#	$(OBJ)/zlib/adler32.o \
#	$(OBJ)/zlib/compress.o \
#	$(OBJ)/zlib/crc32.o \
#	$(OBJ)/zlib/deflate.o \
#	$(OBJ)/zlib/inflate.o \
#	$(OBJ)/zlib/inftrees.o \
#	$(OBJ)/zlib/inffast.o \
#	$(OBJ)/zlib/trees.o \
#	$(OBJ)/zlib/zutil.o

$(OBJ)/%.o: src/%.c
	@echo Compiling $<...
	@$(CC) $(CDEFS) $(CFLAGS) -c $< -o$@

$(OBJ)/%.a:
	@echo Archiving $@...
	@$(AR) -r $@ $^

clean:
	@$(RM) -rf $(OBJS)

maketree:
	@$(MD) -p $(subst //,\,$(sort $(OBJDIRS)))

all: $(TARGET)

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $@ $(OBJS)
