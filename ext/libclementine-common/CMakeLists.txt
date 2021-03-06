include_directories(${PROTOBUF_INCLUDE_DIRS})
include_directories(${CMAKE_CURRENT_BINARY_DIR})
include_directories(${CMAKE_CURRENT_SOURCE_DIR})
include_directories(${CMAKE_SOURCE_DIR}/src)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} --std=c++0x")

set(SOURCES
  core/closure.cpp
  core/logging.cpp
  core/messagehandler.cpp
  core/messagereply.cpp
  core/waitforsignal.cpp
  core/workerpool.cpp
)

set(HEADERS
  core/closure.h
  core/messagehandler.h
  core/messagereply.h
  core/workerpool.h
)

if(APPLE)
  list(APPEND SOURCES core/scoped_nsautorelease_pool.mm)
endif(APPLE)

qt4_wrap_cpp(MOC ${HEADERS})

add_library(libclementine-common STATIC
  ${SOURCES}
  ${MOC}
)

target_link_libraries(libclementine-common
  ${PROTOBUF_LIBRARY}
  ${TAGLIB_LIBRARIES}
  ${CMAKE_THREAD_LIBS_INIT}
)
