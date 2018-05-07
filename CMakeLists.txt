project(flaschen-taschen)
cmake_minimum_required (VERSION 3.1)

option(WALL_ON "Compile with all warnings" ON)
if(WALL_ON)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic -Wextra")
endif()


# set(FT_LOCATION "../flaschen-taschen" CACHE PATH "Location of flaschen-taschen project")
# message(STATUS "FT_LOCATION -> ${FT_LOCATION}")


add_subdirectory(api)
add_subdirectory(client)

