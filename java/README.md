# Template microservice in Java

This is a template of microservice built in lucida

## Major Dependencies

- [OpenCV](http://opencv.org/)
- [Facebook Thrift](https://github.com/facebook/fbthrift)
- [MongoDB](https://www.mongodb.com/)
 and [C++ legacy driver](https://github.com/mongodb/mongo-cxx-driver/tree/legacy)

# Structure

- `server/`: implementation of the IMM server
- `test/`: implementation of the IMM testing client

## Build

```
make
```

## Run

Start the server:

```
make start_server
```

Wait until you see `IMM at 8082`.

Alternatively,

```
cd server
./imm_server
```

## Test

```
make start_test
```

Alternatively,

```
cd test
./imm_client (num_images)
```

7 images `test/test*.jpg` are provided.

## Developing Notes

1. The linker flags in `server/Makefile` are complicated and should be modified with caution.
Specifically, `-lmongoclient` should precede `-lssl` and `-lcrypto`.

2. `server/Image.cpp` uses `cv::SurfFeatureDetector` to turn
an image into a descriptor matrix both represented as `std::string`,
and `server/IMMHandler.cpp` saves the matrix into and loads it from
[GridFS](https://docs.mongodb.com/manual/core/gridfs/).



## Local Development

- Implement your own create/learn/infer function, and change corresponding configuration such as host and port.

- From this directory, type `make` to compile, and `make start_server` to start the service. It requires Java 8. 

- From this directory, type `make start_test` to test the running server.

## How to 
