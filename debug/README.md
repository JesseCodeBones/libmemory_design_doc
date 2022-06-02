# build debug memorylib and debug it.

## source
https://github.com/embeddedartistry/libmemory

## build debug version  
`make DEBUG=1 default`

## import relevent lib to project

* file structure:  
```
lib
  |_libmemory_freelist.a.p
  | |_aligned_malloc.c.o
  | |_malloc_freelist.c.o
  | |_posiz_memalign.c.o
  |
  |_libmemory_freelist.a
```  
* CMakeLists import static lib:  
```cmake
add_library(libmemory STATIC IMPORTED)
set_property(TARGET libmemory PROPERTY
             IMPORTED_LOCATION "/home/jesse/workspace/libmemorytest/lib/libmemory_freelist.a")
target_link_libraries( ${PROJECT_NAME} libmemory )
```

* include headers
```
include
  |_aligned_malloc.h
  |_malloc.h
```  

add include dir  
`include_directories(SYSTEM ${CMAKE_SOURCE_DIR}/include)`  

* add launch.json for vscode
```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "glibc main test",
            "type": "cppdbg",
            "request": "launch",
            "program": "${command:cmake.launchTargetPath}",
            "cwd":"${workspaceFolder}",
            "stopAtEntry": false,
            "environment": [
                {
                    "name": "PATH",
                    "value": "${env:PATH}:${command:cmake.getLaunchTargetDirectory}"
                }
            ],
            "setupCommands": [
                
                {   "description": "mlib source",
                    "text": "directory /home/jesse/workspace/libmemory/src",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
```
