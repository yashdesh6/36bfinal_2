# Makefile for f2022, ecs36b
# https://macappstore.org/libjson-rpc-cpp/
# https://github.com/cinemast/libjson-rpc-cpp

CC = g++ -std=c++14
CFLAGS = -g

# LDFLAGS = 	-L/Users/sfwu/vcpkg/installed/arm64-osx/lib -ljsoncpp -L/opt/homebrew/lib/ -lmicrohttpd -ljsonrpccpp-common -ljsonrpccpp-server -ljsonrpccpp-client -lcurl

LDFLAGS = 	-ljsoncpp -lmicrohttpd -ljsonrpccpp-common -ljsonrpccpp-server -ljsonrpccpp-client -lcurl

# INC	=	ecs36b_Common.h
# INC_CL	=	 auto_v.h Car.h Motorcycle.h truck.h 
OBJ	=	auto_v.o Car.o Motorcycle.o truck.o

# rules.
all: finalServer auto_v Car Motorcycle truck

#
#
# <target> : [... tab...] <dependency>
# [... tab ....] <action>


finalServer.h:		params.json
	jsonrpcstub params.json --cpp-server=finalServer --cpp-client=finalClient

finalClient.o:		finalClient.cpp finalClient.h $(INC_CL) $(INC)
	$(CC) -c $(CFLAGS) finalClient.cpp

finalServer.o:		finalServer.cpp finalServer.h $(INC_CL) $(INC)
	$(CC) -c $(CFLAGS) finalServer.cpp $(LDFLAGS)


finalServer:	finalServer.o $(OBJ)
	$(CC) -o finalServer finalServer.o $(OBJ) $(LDFLAGS)

auto_v.o:		auto_v.cpp auto_v.h $(INC_CL) $(INC)
	$(CC) -c $(CFLAGS) auto_v.cpp $(LDFLAGS)

Car.o:		auto_v.h Car.cpp Car.h finalServer.o $(INC_CL) $(INC)
	$(CC) -c $(CFLAGS) Car.cpp $(LDFLAGS)

Motorcycle.o:	auto_v.h Motorcycle.cpp Motorcycle.h finalServer.o $(INC_CL) $(INC)
	$(CC) -c $(CFLAGS) Motorcycle.cpp $(LDFLAGS)

truck.o:	auto_v.h truck.cpp truck.h finalServer.o $(INC_CL) $(INC)
	$(CC) -c $(CFLAGS) truck.cpp $(LDFLAGS)


auto_v:	 auto_v.o $(OBJ)
	$(CC) -o auto_v auto_v.o $(OBJ) $(LDFLAGS)

Car:	 auto_v.o Car.o finalServer.h$(OBJ)
	$(CC) -o Car Car.o auto_v.o $(OBJ) $(LDFLAGS)

Motorcycle:	 auto_v.o Motorcycle.o finalServer.h$(OBJ)
	$(CC) -o Motorcycle Motorcycle.o auto_v.o $(OBJ) $(LDFLAGS)

truck:	 auto_v.o truck.o finalServer.h$(OBJ)
	$(CC) -o truck truck.o auto_v.o $(OBJ) $(LDFLAGS)

clean:
	rm -f *.o *~ core finalClient.h finalServer.h auto_v.h Car.h Motorcycle.h truck.h finalClient finalServer auto_v Car Motorcycle truck
