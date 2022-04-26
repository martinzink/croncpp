include(FetchContent)
FetchContent_Declare(Catch2
        URL https://github.com/catchorg/Catch2/archive/refs/tags/v2.13.9.tar.gz
        URL_HASH SHA256=06dbc7620e3b96c2b69d57bf337028bf245a211b3cddb843835bfe258f427a52)
FetchContent_MakeAvailable(Catch2)

set(SOURCES main.cpp test_oracle.cpp test_standard.cpp)

add_executable(test_croncpp ${SOURCES})

target_compile_features(test_croncpp PUBLIC ${CXX_STD_VER})
set_target_properties(test_croncpp PROPERTIES CXX_EXTENSIONS OFF)

target_link_libraries(test_croncpp PRIVATE croncpp croncpp_options Catch2)

add_test(NAME "test_croncpp" COMMAND "test_croncpp" "-r compact")
set_tests_properties("test_croncpp" PROPERTIES PASS_REGULAR_EXPRESSION
                                               "Passed all.*")
set_tests_properties("test_croncpp" PROPERTIES FAIL_REGULAR_EXPRESSION
                                               "Failed \\d+ test cases")
set_tests_properties("test_croncpp" PROPERTIES TIMEOUT 120)
