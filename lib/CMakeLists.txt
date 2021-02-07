file(GLOB SOURCES "*.c" "*.h")
add_subdirectory(compat)

add_library(uvcgadget ${SOURCES})

target_include_directories(uvcgadget
	PUBLIC
	$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include>
	$<BUILD_INTERFACE:${CMAKE_SOURCE_DIR}/include/uvcgadget>)
