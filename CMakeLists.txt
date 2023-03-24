cmake_minimum_required(VERSION 3.5)

project(Qt_ProjectTemplate LANGUAGES CXX)

set(CMAKE_BUILD_TYPE "Debug")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/build/bin)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Set Qt path and version
set(QT_DIR "C:/path/Qt/6.4.1/mingw_64")
set(QT_VERSION 6)

set(Qt${QT_VERSION}_DIR ${QT_DIR}/lib/cmake/Qt6)
set(Qt${QT_VERSION}CoreTools_DIR ${QT_DIR}/lib/cmake/Qt6CoreTools)
set(Qt${QT_VERSION}GuiTools_DIR ${QT_DIR}/lib/cmake/Qt6GuiTools)

find_package(Qt${QT_VERSION} REQUIRED COMPONENTS Widgets)

# set(3RDPARTY_DIR ${PROJECT_SOURCE_DIR}/3rdparty)

include_directories(${QT_DIR}/include)

aux_source_directory(src PROJECT_SOURCES)

add_executable(Qt_ProjectTemplate ${PROJECT_SOURCES})

target_link_libraries(Qt_ProjectTemplate PRIVATE Qt${QT_VERSION}::Widgets)

add_custom_command(
    TARGET ${CMAKE_PROJECT_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory
        "${QT_DIR}/plugins/platforms"
        "$<TARGET_FILE_DIR:${CMAKE_PROJECT_NAME}>/platforms"
    COMMAND ${CMAKE_COMMAND} -E copy
        "${QT_DIR}/bin/Qt${QT_VERSION}Core.dll"
        "$<TARGET_FILE_DIR:${CMAKE_PROJECT_NAME}>/"
    COMMAND ${CMAKE_COMMAND} -E copy
        "${QT_DIR}/bin/Qt${QT_VERSION}Gui.dll"
        "$<TARGET_FILE_DIR:${CMAKE_PROJECT_NAME}>/"
    COMMAND ${CMAKE_COMMAND} -E copy
        "${QT_DIR}/bin/Qt${QT_VERSION}Widgets.dll"
        "$<TARGET_FILE_DIR:${CMAKE_PROJECT_NAME}>/"
)
