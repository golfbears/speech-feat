cmake_minimum_required(VERSION 3.5.1)

# Download and build googletest
include(${CMAKE_MODULE_PATH}/BuildGoogleTest.cmake)

function(build_test SRCFILE)
  get_filename_component(src_name ${SRCFILE} NAME_WE)
  message(STATUS "build_test SRCFILE:${SRCFILE}\n src_name:${src_name} \n GTEST_INCLUDE_DIR:${GTEST_INCLUDE_DIR} \n GMOCK_LIBRARIES ${GMOCK_LIBRARIES} \n CMAKE_CXX_STANDARD ${CMAKE_CXX_STANDARD}")
  set(target "${src_name}")
  add_executable(${target} ${SRCFILE})
  add_dependencies(${target} gtest) # make sure gtest is built first
  target_link_libraries(
    ${target}
    PUBLIC
    speech_feat
    ${GTEST_LIBRARIES}
    ${GMOCK_LIBRARIES}
    ${CBLAS_LIBRARIES}
    ${FFTW_LIBRARIES}
    pthread
    )
#target_link_libraries(test gmock gtest pthread)
  target_include_directories(
    ${target}
    PUBLIC
    ${CMAKE_SOURCE_DIR}/..
    ${PROJECT_SOURCE_DIR}/include
    ${GTEST_INCLUDE_DIR}
    ${GMOCK_INCLUDE_DIR}
    ${CBLAS_INCLUDE_DIR}
    )
  target_compile_definitions(
    ${target}
    PUBLIC
#    "DATA_TEST_DATADIR=\"${CMAKE_SOURCE_DIR}/src/data/test/testdata\""
#    "DECODER_TEST_DATADIR=\"${CMAKE_SOURCE_DIR}/src/decoder/test\""
    "FEATURE_TEST_DATADIR=\"${CMAKE_SOURCE_DIR}/test/data\""
#    "MODULE_TEST_ARCHDIR=\"${CMAKE_SOURCE_DIR}/src/module/test\""
    )
  add_test(${target} ${target})
endfunction(build_test)

if (BUILD_TESTS)
  # Common
#  build_test(${CMAKE_SOURCE_DIR}/src/common/test/W2lCommonTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/src/common/test/DictionaryTest.cpp)
#  set(
#    W2L_DICTIONARY_TEST_DIR
#    "\"${CMAKE_SOURCE_DIR}/src/common/test/\""
#    )
#  target_compile_definitions(
#    DictionaryTest
#    PRIVATE
#    -DW2L_DICTIONARY_TEST_DIR=${W2L_DICTIONARY_TEST_DIR}
#  )

  # Criterion
#  build_test(${CMAKE_SOURCE_DIR}/src/criterion/test/CriterionTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/src/criterion/test/Seq2SeqTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/src/criterion/attention/test/AttentionTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/src/criterion/attention/test/WindowTest.cpp)
  # Data
#  build_test(${CMAKE_SOURCE_DIR}/src/data/test/DataTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/src/data/test/ListFileDatasetTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/src/data/test/SoundTest.cpp)
  # Decoder
#  build_test(${CMAKE_SOURCE_DIR}/src/decoder/test/DecoderTest.cpp)
  # Feature
  build_test(${CMAKE_SOURCE_DIR}/test/CeplifterTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/DctTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/DerivativesTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/DitherTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/MfccTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/PreEmphasisTest.cpp)
#  build_test(${CMAKE_SOURCE_DIR}/test/SpeechUtilsTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/TriFilterbankTest.cpp)
  build_test(${CMAKE_SOURCE_DIR}/test/WindowingTest.cpp)
  # Module
#  build_test(${CMAKE_SOURCE_DIR}/src/module/test/W2lModuleTest.cpp)
  # Runtime
#  build_test(${CMAKE_SOURCE_DIR}/src/runtime/test/RuntimeTest.cpp)
endif ()
