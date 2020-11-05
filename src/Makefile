

# default values in case these are not set in upstream Makefile
ifndef Def_Server
  Def_Server = localhost
endif
ifndef Def_DB_Port
  Def_DB_Port = 5679
endif

CC = gcc -Wall
AR = ar
CFLAGS = -O2

# for debugging
# CFLAGS += -g


.PHONY: all clean

all: alivedb libaliveclient.a

alive_client.o: alive_client.c alive_client.h
	$(CC) $(CFLAGS) -DDEF_SERVER=\"$(Def_Server)\" -DDEF_DB_PORT=$(Def_DB_Port) -c alive_client.c
libaliveclient.a: alive_client.o alive_client.h
	$(AR) rcs libaliveclient.a alive_client.o

alivedb.o: alivedb.c alive_client.h
	$(CC) $(CFLAGS) -DDB_SERVER=\"$(Def_Server)\" -c alivedb.c
alivedb: alivedb.o libaliveclient.a
	$(CC) alivedb.o libaliveclient.a -o alivedb

clean:
	-rm alivedb libaliveclient.a *.o

