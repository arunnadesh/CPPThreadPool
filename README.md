# CPPThreadPool
Author: Arun Nadesh R(arunnadesh@gmail.com)

A simple thread pool library implemented using C++,  pthread library and C++ wrappers to pthread library. 
This will create a .so lib libthreadpool.so and the same can be linked with any application which requires
a producer-consumer model of processing jobs.
This is a cmake based project and it is advisable to create a separate build directory and build.

Dependencies: 

      libpthread

Public Headers:

       Job.h,
       Threadpool.h

Steps to build and install:
    
    mkdir <builddir>
    cd <builddir>
    cmake <path-to-source-ThreadPool> -DCMAKE_BUILD_TYPE=<Release or Debug>
    make
    make install
    
    The library will be installed in /usr/local/lib/threadpool
    The headers will be installed in /sr/local/include/threadpool

Steps to make RPM:

    mkdir <builddir>
    cd <builddir>
    cmake <path-to-source-ThreadPool> -DCMAKE_BUILD_TYPE=<Release or Debug>
    make  
    make package
    
    This will build the RPM libthreadpool-1.0.0-1.x86_64.rpm
    To install rpm package in /usr/local/lib/threadpool  and /sr/local/include/threadpool
     rpm -ivh libthreadpool-1.0.0-1.x86_64.rpm
     
    To revert the RPM
     rpm -e libthreadpool
     
Sample Application:
   A sample app built using libthreadpool.so is demonstrated in Threadpooldriver.cpp
   
    ......
       Threadpool thPool(3);

    if(TH_POOL_CREATE_SUCCESS == thPool.threadpool_create()) {

        for(int i=0; i<10; i++){

              Job* jb =  new Job(&testFun, &jobID[i]);
              if(jb){
                 cout<<"Adding new job index: "<<jobID[i]<<endl;
                 thPool.threadpool_add_job(jb);
              }
        }
    }
    sleep(30);
    thPool.threadpool_destroy();
    ........



It would be really appreciated if you send in your feedbacks, comments, suggestions and thanyou notes to arunnadesh@gmail.com 
