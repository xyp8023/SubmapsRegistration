project(feature_matching)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/bin/)

include_directories(include)

find_package(LibXTF REQUIRED)
find_package(LibGSF REQUIRED)
find_package(EigenCereal REQUIRED)
find_package(DataTools REQUIRED)
find_package(PkgConfig)
pkg_check_modules(YAMLCPP REQUIRED yaml-cpp>=0.5)
include_directories(${YAMLCPP_INCLUDE_DIRS})

add_executable (submap_registration
	src/submap_registration.cpp)
target_link_libraries (submap_registration
	${PCL_LIBRARIES} ${YAMLCPP_LIBRARIES})

add_executable (submaps_construction
	src/create_submaps.cpp
	src/submaps.cpp)
target_link_libraries (submaps_construction
	std_data	
	navi_data
	data_transforms
	${PCL_LIBRARIES} ${YAMLCPP_LIBRARIES})

add_executable (visualize_submaps
	src/visualize_submaps.cpp
	src/submaps.cpp)
target_link_libraries (visualize_submaps
	std_data
	navi_data
	data_transforms
	${PCL_LIBRARIES} ${YAMLCPP_LIBRARIES})
