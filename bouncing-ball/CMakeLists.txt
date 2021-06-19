cmake_minimum_required(VERSION 3.14)

project(bouncing-ball LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# include necessary modules
find_package(Qt5 REQUIRED COMPONENTS 3DCore 3DRender 3DInput 3DExtras 3DQuick Qml Quick 3DQuickExtras 3DAnimation)

set(PROJECT_SOURCES
        main.cpp
)

set(OTHER_FILES
        main.qml
        DefaultSceneEntity.qml
        AnimatedEntity.qml
)

qt5_add_big_resources(PROJECT_SOURCES 
        ../resources/cedar-bridge.qrc
        ../resources/gltf.qrc
        bouncing-ball.qrc
)

add_executable(bouncing-ball ${PROJECT_SOURCES} ${OTHER_FILES})

target_compile_definitions(bouncing-ball PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)

# link the libraries
target_link_libraries(bouncing-ball PRIVATE 
        Qt5::3DCore
        Qt5::3DRender
        Qt5::3DInput
        Qt5::3DExtras
        Qt5::3DQuick
        Qt5::Qml
        Qt5::Quick
        Qt5::3DQuickExtras
        Qt5::3DAnimation
)
