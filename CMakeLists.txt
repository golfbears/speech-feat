cmake_minimum_required(VERSION 3.5.1)
#----------------------------- Project definition ------------------------
project(speech_feat)

set(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR}/cmake")
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(SPEECH_FEAT_SRCS 
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Ceplifter.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Dct.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Derivatives.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Dither.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Mfcc.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Mfsc.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/PowerSpectrum.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/PreEmphasis.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/SpeechUtils.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/TriFilterbank.cpp
  ${CMAKE_CURRENT_SOURCE_DIR}/src/Windowing.cpp
  )

set(SPEECH_FEAT_INCLUDE 
  ${CMAKE_CURRENT_SOURCE_DIR}/include
  )
option(BUILD_TESTS "Build tests for speech feature" ON)


message(STATUS "CMAKE_MODULE_PATH:${CMAKE_MODULE_PATH}")
message(STATUS "CMAKE_MODULE_PATH:${CMAKE_MODULE_PATH}")
message(STATUS "CMAKE_CURRENT_SOURCE_DIR:${CMAKE_CURRENT_SOURCE_DIR}\n (PROJECT_SOURCE_DIR: ${PROJECT_SOURCE_DIR})")

# ----------------------------- Dependencies -----------------------------
# CBLAS
#if (W2L_LIBRARIES_USE_MKL)
#  find_package(MKL REQUIRED)
#  set(CBLAS_LIBRARIES ${MKL_LIBRARIES})
#  set(CBLAS_INCLUDE_DIR ${MKL_INCLUDE_DIR})
#else ()
find_package(CBLAS REQUIRED)
#endif ()
message(STATUS "CBLAS found (include: ${CBLAS_INCLUDE_DIR}, library: ${CBLAS_LIBRARIES})")

# FFTW
find_package(FFTW REQUIRED)
if (FFTW_FOUND)
  message(STATUS "FFTW found (include: ${FFTW_INCLUDE_DIR}, library: ${FFTW_LIBRARIES})")
else()
  message(FATAL_ERROR "FFTW not found")
endif()

# Tests
if (BUILD_TESTS)
  enable_testing()
  add_subdirectory(${PROJECT_SOURCE_DIR}/test)
endif ()


# ----------------------------- Lib -----------------------------a

message(STATUS "CMAKE_CXX_FLAGS:${CMAKE_CXX_FLAGS}")

add_library(
  speech_feat
  SHARED
  ${SPEECH_FEAT_SRCS}
  ${SPEECH_FEAT_INCLUDE}
  ${CBLAS_LIBRARIES}
  ${FFTW_LIBRARIES}
  )

set_target_properties (
  speech_feat
  PROPERTIES 
  LINKER_LANGUAGE CXX
  CXX_STANDARD 11
  VERSION 0.1
  SOVERSION 0.1
  )

#target_link_libraries(
#  speech-feat
#  INTERFACE
#  ${CBLAS_LIBRARIES}
#  ${FFTW_LIBRARIES}
#  )


#target_include_directories(
#  speech-feat
#  PUBLIC
#  ${PROJECT_SOURCE_DIR}/include
#  ${CBLAS_INCLUDE_DIR}
#  )



