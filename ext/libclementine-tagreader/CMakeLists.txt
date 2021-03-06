include_directories(${PROTOBUF_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_SOURCE_DIR}/ext/libclementine-common)
include_directories(${CMAKE_SOURCE_DIR}/src)
include_directories(${CMAKE_BINARY_DIR}/src)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --std=c++0x")

set(MESSAGES
  tagreadermessages.proto
)

set(SOURCES
  fmpsparser.cpp
  tagreader.cpp
)

set(HEADERS
)

optional_source(HAVE_GOOGLE_DRIVE
  INCLUDE_DIRECTORIES ${SPARSEHASH_INCLUDE_DIRS}
  SOURCES
    cloudstream.cpp
  HEADERS
    cloudstream.h
)

qt4_wrap_cpp(MOC ${HEADERS})

protobuf_generate_cpp(PROTO_SOURCES PROTO_HEADERS ${MESSAGES})

add_library(libclementine-tagreader STATIC
  ${PROTO_SOURCES}
  ${SOURCES}
  ${MOC}
)

target_link_libraries(libclementine-tagreader
  libclementine-common
)

