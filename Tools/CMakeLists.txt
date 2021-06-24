# CmakeLists.txt in Tools

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3  -g   -fPIC")

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3  -g   -fPIC")

include_directories(  ${CMAKE_BINARY_DIR})


#FIND_PACKAGE(Qt4 REQUIRED)
set(Qt5_DIR  /home/alex/Qt5.12.10/5.12.10/gcc_64/lib/cmake/Qt5   )
#FIND_PACKAGE(Qt5 REQUIRED   PATHS   /home/alex/Qt5.12.10/5.12.10/gcc_64   )
find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets REQUIRED)
#SET(QT_USE_QTSVG TRUE)
#INCLUDE(${QT_USE_FILE})

include_directories(/home/alex/Qt5.12.10/5.12.10/gcc_64/include)
include_directories(/home/alex/Qt5.12.10/5.12.10/gcc_64/include/QtWidgets)
include_directories(/home/alex/Qt5.12.10/5.12.10/gcc_64/include/QtScript)


FILE(GLOB Tools_CPP "*.cpp")
FILE(GLOB Tools_H "*.h")
FILE(GLOB Tools_UI "*.ui")

#QT4_WRAP_UI(Tools_H ${Tools_UI})

LIST(APPEND Tools_Sources ${Tools_CPP} ${Tools_H})

#QT4_AUTOMOC(${Tools_Sources})

#This is for moc files
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})

#And this is for config.h
INCLUDE_DIRECTORIES(${CMAKE_BINARY_DIR})

INCLUDE_DIRECTORIES(${Cornucopia_SOURCE_DIR}/Cornucopia)

ADD_EXECUTABLE(CornucopiaTools ${Tools_Sources})

TARGET_LINK_LIBRARIES(CornucopiaTools    PRIVATE Qt${QT_VERSION_MAJOR}::Widgets
#    Qt${QT_VERSION_MAJOR}::Script
    Cornucopia ${QT_LIBRARIES}    )

CONFIGURE_FILE(config.h.cmake config.h )
