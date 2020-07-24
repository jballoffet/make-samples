################################################################
# AUTHOR INFORMATION                                           #
################################################################

AUTHOR   = "JavierBalloffet"
CLASS    = "R1042"
EXERCISE = "1_1"
YEAR     = "2020"

################################################################
# SOURCES, HEADERS, OBJECTS, LIBRARIES AND EXECUTABLES         #
################################################################

SRC_DIR   = src
BUILD_DIR = build
BIN_DIR   = bin

SOURCES = $(shell find $(SRC_DIR) -name '*.c')
HEADERS = $(shell find $(SRC_DIR) -name '*.h')
OBJS    = $(patsubst %.c, $(BUILD_DIR)/%.o, $(SOURCES))
EXEC    = app

################################################################
# COMPILER AND ARGUMENTS                                       #
################################################################

CC           = gcc
CFLAGS       = -c -Wall
EXTRA_CFLAGS =
LDFLAGS      = -lm

ifdef DEBUG
  EXTRA_CFLAGS += -g -O0 -DDEBUG
endif

################################################################
# TAR FILE INFORMATION                                         #
################################################################

FILE_NAME = $(AUTHOR)-$(CLASS)-$(EXERCISE)-$(YEAR).tar.gz

################################################################
# TEXT EDITOR                                                  #
################################################################

TEXT_EDITOR = code

################################################################
# DOCUMENTATION                                                #
################################################################

DOC_GEN  = doxygen
DOC_FILE = Doxyfile
DOC_DIR  = doc

################################################################
# MAKE TARGETS                                                 #
################################################################

.PHONY: all clean compress edit doc help

all: $(EXEC)

$(EXEC): $(OBJS)
	@echo '[LD] Linking C executable $@'
	@mkdir -p $(BIN_DIR)
	$(CC) $(OBJS) $(LDFLAGS) -o $(BIN_DIR)/$@
	@echo 'Built target $@'

$(BUILD_DIR)/%.o: %.c Makefile
	@echo '[CC] Compiling C object $@'
	@mkdir -p $(dir $@)
	$(CC) $(CFLAGS) $(EXTRA_CFLAGS) $< -o $@

clean:
	@echo '[RM] Cleaning workspace'
	rm -rf $(BUILD_DIR) $(BIN_DIR) $(DOC_DIR)

compress:
	@echo '[TAR] Packing workspace'
	tar -zcvf $(FILE_NAME) $(SRC_DIR) Makefile $(DOC_FILE)

edit:
	@echo '[ED] Editing workspace'
	$(TEXT_EDITOR) .

doc:
	@echo '[DOC] Generating documentation'
	@mkdir -p $(DOC_DIR)
	$(DOC_GEN) $(DOC_FILE)

help:
	@echo ''
	@echo '********************************************************'
	@echo '  Usage:'
	@echo '    make all:       Compiles and links the application'
	@echo '    make clean:     Removes objects and executable'
	@echo '    make compress:  Generates .tar.gz file'
	@echo '    make edit:      Opens code files with text editor'
	@echo '    make doc:       Generates code documentation'
	@echo '    make help:      Shows help'
	@echo '********************************************************'
	@echo ''