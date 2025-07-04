set(CRASHPAD_TOOLS_LIBRARY_FILES
    ./tool_support.cc
    ./tool_support.h
)

add_library(tools OBJECT ${CRASHPAD_TOOLS_LIBRARY_FILES})
target_compile_features(tools PUBLIC cxx_std_14)

target_include_directories(tools PUBLIC ..)
target_link_libraries(tools PUBLIC mini_chromium backtrace_common util compat snapshot)

add_executable(generate_dump generate_dump.cc)
target_include_directories(generate_dump PRIVATE ..)
target_compile_features(generate_dump PRIVATE cxx_std_14)
target_link_libraries(generate_dump PRIVATE tools snapshot minidump)
