project(audiodecoder.2sf)

cmake_minimum_required(VERSION 2.6)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${PROJECT_SOURCE_DIR})

enable_language(CXX)

find_package(Kodi REQUIRED)
find_package(ZLIB REQUIRED)

include_directories(${KODI_INCLUDE_DIR}/..
                    ${ZLIB_INCLUDE_DIR}
                    ${PROJECT_SOURCE_DIR}/lib/vio2sf/src/vio2sf/desmume
                    ${PROJECT_SOURCE_DIR}/lib/psflib)

add_subdirectory(lib/vio2sf)
add_subdirectory(lib/psflib)

set(2SF_SOURCES src/2SFCodec.cpp)

set(DEPLIBS vio2sf psflib ${ZLIB_LIBRARIES})

build_addon(audiodecoder.2sf 2SF DEPLIBS)

if(CORE_SYSTEM_NAME MATCHES windows)
  target_compile_definitions(audiodecoder.2sf PRIVATE -Dstrcasecmp=_stricmp)
endif()

include(CPack)
