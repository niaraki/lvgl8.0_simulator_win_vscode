#
# Makefile
# WARNING: relies on invocation setting current working directory to Makefile location
# This is done in .vscode/task.json
#
PROJECT 			?= lvgl-sdl
MAKEFLAGS 			:= -j 1
SRC_EXT      		:= c
OBJ_EXT				:= o
CC 					:= gcc

SRC_DIR				:= $(shell chdir)
WORKING_DIR			:= ./build
BUILD_DIR			:= $(WORKING_DIR)/obj
BIN_DIR				:= $(WORKING_DIR)/bin
UI_DIR 				:= ui

WARNINGS 			:=  -Wall -Wextra \
						-Wshadow -Wundef -Wmaybe-uninitialized -Wmissing-prototypes -Wno-discarded-qualifiers \
						-Wno-unused-function -Wno-error=strict-prototypes -Wpointer-arith -fno-strict-aliasing -Wno-error=cpp -Wuninitialized \
						-Wno-unused-parameter -Wno-missing-field-initializers -Wno-format-nonliteral -Wno-cast-qual -Wunreachable-code -Wno-switch-default  \
					  	-Wreturn-type -Wmultichar -Wformat-security -Wno-ignored-qualifiers -Wno-error=pedantic -Wno-sign-compare -Wno-error=missing-prototypes -Wdouble-promotion -Wclobbered -Wdeprecated  \
						-Wempty-body -Wshift-negative-value -Wstack-usage=2048 \
            			-Wtype-limits -Wsizeof-pointer-memaccess -Wpointer-arith

CFLAGS 				:= -O0 -g $(WARNINGS)

# Add simulator define to allow modification of source
DEFINES				:= -D SIMULATOR=1 -D LV_BUILD_TEST=0

# Include simulator inc folder first so lv_conf.h from custom UI can be used instead
INC 				:= -I./ui/simulator/inc/ -I. -I./lvgl/ -I..\libs\SDL2-2.26.1\i686-w64-mingw32\include
LDLIBS	 			:= -lSDL2main -lSDL2 -lm -L..\libs\SDL2-2.26.1\i686-w64-mingw32\lib
BIN 				:= $(BIN_DIR)/demo
COMPILE				:= $(CC) $(CFLAGS) $(INC) $(DEFINES) $(LDLIBS)

# Automatically include all source files
SUBDIR 				:= $(shell dir /W /S /a:d /b)
SRCS				:= $(wildcard *.c $(foreach fd, $(SUBDIR), $(fd)/*.c))
OBJS				:= $(SRCS:.$(SRC_EXT)=.$(OBJ_EXT))
OBJECTS    			:= $(patsubst $(SRC_DIR)%,$(BUILD_DIR)%, $(OBJS))

$(BUILD_DIR)%.$(OBJ_EXT): $(SRC_DIR)%.$(SRC_EXT)
	@echo 'Building project file: $<'
	@IF NOT EXIST "$(dir $@)" md "$(dir $@)" 2>nul
	@$(COMPILE) -c -o "$@" "$<"

all: default

default: $(OBJECTS)
	@echo 'Building final program...'
	@IF NOT EXIST "$(BIN)" md "$(BIN)" 2>nul
	$(CC) -o $(BIN) $(OBJECTS) $(LDFLAGS) ${LDLIBS}
	@IF NOT EXIST ".\build\bin\sdl2.dll" @copy "..\libs\SDL2-2.26.1\i686-w64-mingw32\bin\sdl2.dll" ".\build\bin\sdl2.dll"
	
clean: 
	del /q/f/s "$(WORKING_DIR)" 

.PHONY: clean default