

find_package(ImageMagick COMPONENTS Magick++)
if(ImageMagick_FOUND)
  project(send-image)
  add_executable(${PROJECT_NAME} ${PROJECT_NAME}.cc)
  target_link_libraries(${PROJECT_NAME} api ${ImageMagick_LIBRARIES})
  target_include_directories(${PROJECT_NAME} PUBLIC "${ImageMagick_INCLUDE_DIRS}")
else()
  message(STATUS "ImageMagick not found, not building image-viewer")
endif()


project(send-video)

file(GLOB SOURCES ${PROJECT_NAME}.cc)

find_path(AVCODEC_INCLUDE_DIR libavcodec/avcodec.h)
find_library(AVCODEC_LIBRARY avcodec)
find_library(AVFORMT_LIBRARY avformat)
find_library(SWSCALE_LIBRARY swscale)
find_library(AVUTIL_LIBRARY avutil)

#find_path(AO_INCLUDE_DIR ao/ao.h)
#find_library(AO_LIBRARY ao)

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

target_include_directories(${PROJECT_NAME} PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_include_directories(${PROJECT_NAME} PRIVATE ${AVCODEC_INCLUDE_DIR}) #${AO_INCLUDE_DIR})
target_link_libraries(${PROJECT_NAME} PRIVATE
  api
  ${AVCODEC_LIBRARY}
  ${AVFORMT_LIBRARY}
  ${SWSCALE_LIBRARY}
  ${AVUTIL_LIBRARY}
  #${AO_LIBRARY}
)
