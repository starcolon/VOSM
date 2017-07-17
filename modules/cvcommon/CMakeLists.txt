include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include" "${CMAKE_CURRENT_SOURCE_DIR}/../common/include" "${CMAKE_CURRENT_SOURCE_DIR}/../smbuilding/include")

# Set library source
set(LIB_SRC src/VO_AnnotationDBIO.cpp src/VO_FaceCompPos.cpp src/VO_DetectionDBIO.cpp src/VO_FaceKeyPoint.cpp)

# Generate shared library
add_library(cvcommon_shared SHARED ${LIB_SRC} )
set_target_properties(cvcommon_shared PROPERTIES OUTPUT_NAME "vosm_cvcommon")
get_target_property(OUTPUT_NAME cvcommon_shared OUTPUT_NAME)
message(STATUS "Shared library outname:" ${OUTPUT_NAME})

if (UNIX)
target_link_libraries(cvcommon_shared ${OPENCV_CORE_LIB}
                                      ${OPENCV_IMGPROC_LIB}
                                      ${OPENCV_HIGHGUI_LIB}
                                      ${OPENCV_FEATURES2D_LIB})
endif (UNIX)

file(GLOB INSTALL_HEADERS
    "include/*.h"
)
install(TARGETS cvcommon_shared DESTINATION lib)
install(FILES ${INSTALL_HEADERS} DESTINATION include/vosm)
