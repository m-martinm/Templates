cmake_minimum_required(VERSION 3.20)
project(example_project C/C++) # choose C or C++

if(UNIX) # compile options if on linux system
    add_compile_options(-std=c11 -g)
    add_compile_options(-Werror -Wall -pedantic)
    add_compile_options(-fsanitize=address)
    add_compile_options(-Wno-unused-variable)
    add_compile_options(-Wno-unused-function)
    add_compile_options(-Wno-error=return-type)
    add_link_options(-fsanitize=address)
endif(UNIX)

add_library(Libraryname OBJECT src/something.c) # static library option
target_include_directories(Libraryname PUBLIC include) # filepath to included header files

add_executable(Example src/main.c)
target_link_libraries(Example Libraryname)

######################### Alternative #########################################

list(APPEND SOURCE "path to c file" "path to c file...") 
list(APPEND LIBS "${CMAKE_CURRENT_SOURCE_DIR}.........") # for example for .lib files

add_executable(Example ${SOURCE})
target_link_libraries(Example ${LIBS})

################ Adding resources to project (images, etc) ####################

list(APPEND DATA "path to /resources")
file(COPY ${data} DESTINATION resources) # copy files to build directory
