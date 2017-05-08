# OpenCV IMM

OpenCV IMM uses [OpenCV](http://opencv.org/), an open-source BSD-licensed library 
that includes several hundreds of computer vision algorithms. 

## Major Dependencies

- [Facebook Thrift](https://github.com/facebook/fbthrift)

# Structure

- `server/`: implementation of the template server
- `test/`: implementation of the template testing client

### Step 0: move the directory 

To get started, place the directory under 'lucida/lucida' folder, and change the name of your directory into a specified name represent your service.

### Step1: change the configuration

Change the port number for your service (default is 8889) in [server/TemplateServer.cpp](server/TemplateServer.cpp).

### Step2: implement your own create/learn/infer methods

Implement your own create/learn/infer methods in [server/TemplateHandler.cpp](server/TemplateHandler.cpp). The spec of these three function is in the toppest-level readme. Your are free to import different packages for your service, but remember to add the dependence correctly.

### Step3: update the 'Makefile'

Update the [README.md](README.md). The default one has included the generating Thrift stubs code. You only need to add the dependence of your own service.

### Step4: test your service individually

Change the [test application](test) corresponding to your service. After that, do the following steps under this directory to test your service.

- build 
'''
make all
'''
- start server
'''
make start_server
'''
- start testing
'''
make start_test
'''

### Step5: insert your service into Lucida

Modify the top-level 'Makefile' and 'lucida/Makefile' so that 'make local' and




Open 

## Build

```
make all
```

## Run

Start the server:

```
make start_server
```

Wait until you see `8082`.

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
