cmake_minimum_required(VERSION 3.12)
project(TestConsumeMingw)

set(CMAKE_CXX_STANDARD 14)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../x64/Release)

add_executable(canLinkNotifications main.cpp)

target_link_libraries(canLinkNotifications SimpleDisplay.lib)

add_custom_command(TARGET canLinkNotifications POST_BUILD        # Adds a post-build event to MyTest
        COMMAND ${CMAKE_COMMAND} -E copy_if_different  # which executes "cmake - E copy_if_different..."
        ${CMAKE_CURRENT_SOURCE_DIR}/../x64/Release/SimpleDisplay.dll     # <--this is in-file
        $<TARGET_FILE_DIR:canLinkNotifications>)                 # <--this is out-file path
