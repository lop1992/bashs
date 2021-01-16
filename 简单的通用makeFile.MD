bash: mkdir include src obj bin

```bash
# makefile
# 编译结果
TARGET = main

# 文件夹
DIR_INC = ./include
DIR_SRC = ./src
DIR_OBJ = ./obj
DIR_BIN = ./bin

# 目标 如果有多级文件夹都需要加上***
SRC = $(wildcard ${DIR_SRC}/*.cpp ${DIR_SRC}/***/*.cpp)
OBJ = $(patsubst %.cpp,${DIR_OBJ}/%.o,$(notdir ${SRC}))

BIN_TARGET = ${DIR_BIN}/${TARGET}


# 编译指令
CC = g++
CFLAGS = -g -Wall -I${DIR_INC}
LFLAGS = -Wall

#target:
#	@echo $(SRC)
#	@echo $(OBJ)


#主文件
${BIN_TARGET}:${OBJ}
	${CC} $(OBJ) -o $@

#第一层文件
${DIR_OBJ}/%.o:${DIR_SRC}/%.cpp
	${CC} $(CFLAGS) -c $< -o $@

#第二层文件
${DIR_OBJ}/%.o:${DIR_SRC}/***/%.cpp
	${CC} $(CFLAGS) -c $< -o $@

.PHONY:clean
clean:
	find ${DIR_OBJ} -name *.o | xargs rm -rf {}

```
