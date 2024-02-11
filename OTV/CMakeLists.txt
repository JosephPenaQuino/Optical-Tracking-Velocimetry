cmake_minimum_required(VERSION 3.5.1)
set (CMAKE_BUILD_TYPE Release)
SET (CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake")
add_definitions(-std=c++0x)
project(river_flow_velocity_estimation)
file(GLOB SOURCES "src/*.cpp")

EXECUTE_PROCESS( COMMAND uname -m COMMAND tr -d '\n' OUTPUT_VARIABLE ARCHITECTURE )
message( STATUS "Architecture: ${ARCHITECTURE}" )

if( ${ARCHITECTURE} STREQUAL "x86_64" )
	link_directories("/home/joseph/libs/opencv-2.4.13.7/release/installed/lib")
	set(OpenCV_INCLUDE_DIRS
		"/home/joseph/libs/opencv-2.4.13.7/release/installed/include")
	# set (CMAKE_SHARED_LINKER_FLAGS "-Wl,-rpath=/home/joseph/libs/opencv-2.4.13.7/release/installed/lib")
else()
	link_directories("/home/pi/libs/opencv-2.4/release/installed/lib")
	set(OpenCV_INCLUDE_DIRS "/home/pi/libs/opencv-2.4/release/installed/include")
endif()
	set(OpenCV_LIBS "opencv_videostab;opencv_video;opencv_ts;opencv_superres;opencv_stitching;opencv_photo;opencv_objdetect;opencv_nonfree;opencv_ml;opencv_legacy;opencv_imgproc;opencv_highgui;opencv_gpu;opencv_flann;opencv_features2d;opencv_core;opencv_contrib;opencv_calib3d")
	# set(OpenCV_LIBS "opencv_videostab;opencv_video;opencv_superres;opencv_stitching;opencv_photo;opencv_objdetect;opencv_ml;opencv_imgproc;opencv_highgui;opencv_flann;opencv_features2d;opencv_core;opencv_calib3d")

add_executable(river_flow_velocity_estimation ${SOURCES})
set(OTV_INCLUDE_DIRS "include")

target_include_directories(river_flow_velocity_estimation PUBLIC ${OpenCV_INCLUDE_DIRS} ${OTV_INCLUDE_DIRS} ${catkin_INCLUDE_DIRS})

target_link_libraries(river_flow_velocity_estimation PUBLIC ${OpenCV_LIBS} ${catkin_LIBRARIES})

