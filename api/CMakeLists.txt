get_filename_component(PROJ_NAME ${CMAKE_CURRENT_SOURCE_DIR} NAME)
project(${PROJ_NAME})

file(GLOB SOURCES "lib/*.cc")
file(GLOB HEADERS "lib/*.h" "include/*.h")


if(UNIX)
  list(APPEND LIBS pthread)
  if("${CMAKE_SYSTEM_NAME}" MATCHES "Linux")
    list(APPEND LIBS dl rt pthread)
  endif()
endif()


add_library(${PROJ_NAME} ${SOURCES} ${HEADERS})

target_include_directories(${PROJ_NAME} PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_link_libraries(${PROJ_NAME} PRIVATE ${LIBS})

