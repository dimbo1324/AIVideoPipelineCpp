find_package(GTest REQUIRED)
add_executable(core_tests
  tests/core/TestGraphUtils.cpp
  tests/core/TestScheduler.cpp
)
target_link_libraries(core_tests PRIVATE core GTest::gtest_main)
add_test(NAME core_tests COMMAND core_tests)
