project(irrlicht LANGUAGES C CXX)
cmake_minimum_required(VERSION 3.16)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

set(depdir ${CMAKE_CURRENT_LIST_DIR}/dependencies)
set(srcdir ${PROJECT_BINARY_DIR}/irrlicht/source)
set(incdir ${PROJECT_BINARY_DIR}/irrlicht/include)

find_package(Subversion REQUIRED)
find_package(Patch REQUIRED)

execute_process(COMMAND 
    ${Subversion_SVN_EXECUTABLE} checkout 
    "https://svn.code.sf.net/p/irrlicht/code/trunk"
    "${PROJECT_BINARY_DIR}/irrlicht"
)

#patch irrXML.h
#fixes build error
execute_process(COMMAND
    ${Patch_EXECUTABLE} -N
    "${incdir}/irrXML.h"
    "${CMAKE_CURRENT_LIST_DIR}/irrXML.h.patch"
)

add_custom_target(update_repo COMMAND ${Subversion_SVN_EXECUTABLE} update "${PROJECT_BINARY_DIR}/irrlicht")

# irrlicht dependencies
add_library(lzma ${srcdir}/Irrlicht/lzma/LzmaDec.c)
target_include_directories(lzma PUBLIC 
    "${srcdir}/Irrlicht/lzma"
)

add_subdirectory(${depdir}/zlib)
add_subdirectory(${depdir}/libpng)
add_subdirectory(${depdir}/libjpeg)

add_library(bzip2
    ${depdir}/bzip2-1.0.6/blocksort.c
    ${depdir}/bzip2-1.0.6/huffman.c
    ${depdir}/bzip2-1.0.6/crctable.c
    ${depdir}/bzip2-1.0.6/randtable.c
    ${depdir}/bzip2-1.0.6/compress.c
    ${depdir}/bzip2-1.0.6/decompress.c
    ${depdir}/bzip2-1.0.6/bzlib.c
    ${depdir}/bzip2-1.0.6/bzip2recover.c
)
target_compile_definitions(bzip2 PRIVATE "_FILE_OFFSET_BITS=64")
target_include_directories(bzip2 PUBLIC 
    ${PROJECT_SOURCE_DIR}/dependencies/bzip2-1.0.6
)

add_library(aesGladman
    ${srcdir}/Irrlicht/aesGladman/aescrypt.cpp
    ${srcdir}/Irrlicht/aesGladman/aeskey.cpp
    ${srcdir}/Irrlicht/aesGladman/aestab.cpp
    ${srcdir}/Irrlicht/aesGladman/fileenc.cpp
    ${srcdir}/Irrlicht/aesGladman/hmac.cpp
    ${srcdir}/Irrlicht/aesGladman/prng.cpp
    ${srcdir}/Irrlicht/aesGladman/pwd2key.cpp
    ${srcdir}/Irrlicht/aesGladman/sha1.cpp
    ${srcdir}/Irrlicht/aesGladman/sha2.cpp
)
target_include_directories(aesGladman PUBLIC 
    "${srcdir}/Irrlicht/aesGladman"
    PRIVATE "${incdir}"
)

#end dependencies

file(GLOB irrlicht_sources CONFIGURE_DEPENDS 
    "${srcdir}/Irrlicht/*.cpp"
)

add_library(Irrlicht ${irrlicht_sources})
target_include_directories(Irrlicht SYSTEM PUBLIC 
    "${srcdir}/Irrlicht"
    "${incdir}"
)
#target_compile_definitions(irrlicht PRIVATE "PNG_THREAD_UNSAFE_OK" "PNG_NO_MMX_CODE" "PNG_NO_MNG_FEATURES")

if(BUILD_SHARED_LIBS)
    set(ZLIB_LIBRARY zlib)
else()
    set(ZLIB_LIBRARY zlibstatic)
endif()

# add opengl dependency
set(OpenGL_GL_PREFERENCE GLVND)
find_package(OpenGL REQUIRED)
set(OpenGL_Targets )

if(OPENGL_opengl_LIBRARY) #GLVND GL
    list(APPEND OpenGL_Targets OpenGL::OpenGL)
    if(OpenGL_GLX_FOUND)
         list(APPEND OpenGL_Targets OpenGL::GLX Xxf86vm)
    endif()
else() #Legacy OpenGL
    list(APPEND OpenGL_Targets OpenGL::GL)
endif()

if(OpenGL_GLU_FOUND)
    list(APPEND OpenGL_Targets OpenGL::GLU)
endif()
# end opengl

target_link_libraries(Irrlicht 
    bzip2 lzma ${ZLIB_LIBRARY} png jpeg aesGladman ${OpenGL_Targets}
) 
