# Minimal Makefile for hello_world

#hello_world.exe: Main.cpp Hello.cpp Hello.h
#	g++ -o $@.debug Main.cpp Hello.h
#	strip $@.debug -o $@

# Other style
# Makefile for hello_world
# Setting a defualt configuration if invoked with just "make":
CFG ?= dedug

# Set the compiler tools (change here for cross-compiling)
CC = gcc
CXX = g++
LD = $(CXX) # Use the C++ compiler an linker for converience
STRIP = strip

# The executable to build
TARGET = hello_world.exe

# The source files
SRC = Main.cpp Hello.cpp

# Compilation & linker flags
CFLAGS = -MMD -MP
LDFLAGS = 


# # Generate the lists of compiled object and depencency files
# OBJS = $(patsubst %.cpp, %.o, ${SRC})
# DEPS = $(patsubst %.cpp, %.o, ${SRC})

BUILD_DIR = build
OBJS_DIR = $(BUILD_DIR)/objs

# Generate the lists of compiled object and depencency files
OBJS = $(patsubst %.cpp, $(OBJS_DIR)/%.o, ${SRC})
DEPS = $(patsubst %.cpp, $(OBJS_DIR)/%.d, ${SRC})

# The default build rule
.PHONY: all
all: $(TARGET)

$(TARGET): $(OBJS)
	$(LD) $(LDFLAGS) -o $@.debug $(OBJS)
	strip $@.debug - $@

%.o: %.cpp
	$(CXX) -c $(LDFLAGS) -o $@ $<

inform:
	ifneq ($(CFG), release)
	ifneq ($(CFG), debug)
		@echo "Invalid configuretion "$(CFG)" specified."
		@echo 
		@echo "Possible choicse for configuretion are "CFG=release" and "CFG=debug"
		@exit 1
	endif
	endif
		@echo "Configuretion "$(CFG)
		@echo "------------------------------------------------------------------------"

$(BUILD_DIR)/$(TARGET): $(OBJS) | inform
	mkdir -p "$(dir $@)"
	$(LD) $(LDFLAGS) -o $@.debug $(OBJS)
	$(STRIP) $@.debug -o $@

$(OBJS_DIR)/%.o: %.cpp | inform
	mkdir -p "(dir $@)"
	$(CXX) -c $(CFLAGS) -o $@ $<

.PHONY: clean
clean: 
#	rm $(OBJS) $(DEPS) $(TARGET) $(TARGET).debug
	rm $(OBJS) $(DEPS) $(BUILD_DIR)/$(TARGET) $(BUILD_DIR)/$(TARGET).debug

-include $(DEPS)