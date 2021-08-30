SOURCE = src/application.cpp \
         src/main.cpp \
         src/graph.cpp \
         src/bfsPaths.cpp \
         src/dfsPaths.cpp \
         src/bridges.cpp

OBJS = $(SOURCE:.cpp=.o)

#GNU C/C++ Compiler
GCC = g++

# GNU C/C++ Linker
LINK = g++

# Compiler flags
CFLAGS = -Wall -O3 -I inc
CXXFLAGS = $(CFLAGS)

# Fill in special libraries needed here
LIBS = -lX11 -lGL -lpng -lpthread -lstdc++fs

.PHONY: clean

# Targets include all, clean, debug, tar

all : application generateGraph

application: $(OBJS)
	$(LINK) -o $@ $^ $(LIBS)

generateGraph: generateGraph.cpp
	$(LINK) -o $@ $^ $(LIBS)

clean:
	rm -rf src/*.o src/*.d core application generateGraph

debug: CXXFLAGS = -Wall -I inc -DDEBUG -g -lX11 -lGL -lpng -lpthread -lstdc++fs
debug: application

tar: clean
	tar zcvf application.tgz $(SOURCE) inc/*.h Makefile

help:
	@echo "	make application  - same as make all"
	@echo "	make all   - builds the main target"
	@echo "	make       - same as make all"
	@echo "	make clean - remove .o .d core main"
	@echo "	make debug - make all with -g and -DDEBUG"
	@echo "	make tar   - make a tarball of .cpp and .h files"
	@echo "	make help  - this message"

-include $(SOURCE:.cpp=.d)

%.d: %.cpp
	@set -e; rm -rf $@;$(GCC) -MM $< $(CXXFLAGS) > $@
