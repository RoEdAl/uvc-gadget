cmake_minimum_required(VERSION 3.0)
project(uvc-gadget)

ADD_COMPILE_OPTIONS(-Wall)
ADD_COMPILE_OPTIONS(-Wextra)
ADD_COMPILE_OPTIONS(-Wno-unused)
ADD_COMPILE_OPTIONS(-Wno-unused-parameter)
ADD_COMPILE_OPTIONS(-Wno-missing-field-initializers)
ADD_COMPILE_OPTIONS(-fvisibility=hidden)
ADD_COMPILE_OPTIONS(-ffile-prefix-map=${CMAKE_SOURCE_DIR}=.)

IF(DEFINED ENV{CPPFLAGS})
    ADD_DEFINITIONS($ENV{CPPFLAGS})
ENDIF()

IF(DEFINED ENV{SOURCE_DATE_EPOCH})
    STRING(TIMESTAMP SOURCE_DATE_EPOCH UTC)
    MESSAGE(STATUS "Source date epoch: ${SOURCE_DATE_EPOCH}")
ENDIF()

include_directories(${CMAKE_BINARY_DIR}/generated)

add_subdirectory(lib)

# Generate config.h
configure_file(${CMAKE_SOURCE_DIR}/include/config.h.in
	       ${CMAKE_BINARY_DIR}/generated/config.h)

add_executable(uvc-gadget main.c)
target_link_libraries(uvc-gadget uvcgadget)
install(TARGETS uvc-gadget DESTINATION bin)
