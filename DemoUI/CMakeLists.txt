# CmakeLists.txt in DemoUI

set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3  -g   -fPIC")




#FIND_PACKAGE(Qt4 REQUIRED)
set(Qt5_DIR  /home/alex/Qt5.12.10/5.12.10/gcc_64/lib/cmake/Qt5   )
#FIND_PACKAGE(Qt5 REQUIRED   PATHS   /home/alex/Qt5.12.10/5.12.10/gcc_64   )
find_package(QT NAMES Qt6 Qt5 COMPONENTS Widgets Script REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Widgets Script REQUIRED)
SET(QT_USE_QTSVG TRUE)
SET(QT_USE_QTSCRIPT TRUE)
#INCLUDE(${QT_USE_FILE})

include_directories(/home/alex/Qt5.12.10/5.12.10/gcc_64/include)
include_directories(/home/alex/Qt5.12.10/5.12.10/gcc_64/include/QtWidgets)
include_directories(/home/alex/Qt5.12.10/5.12.10/gcc_64/include/QtScript)

INCLUDE_DIRECTORIES(${Cornucopia_SOURCE_DIR}/Cornucopia)
INCLUDE_DIRECTORIES(${Cornucopia_SOURCE_DIR}/DemoUI)

FILE(GLOB DemoUI_CPP "*.cpp")
FILE(GLOB DemoUI_H "*.h")
FILE(GLOB DemoUI_UI "*.ui")

#QT4_WRAP_UI(DemoUI_H ${DemoUI_UI})

LIST(APPEND DemoUI_Sources ${DemoUI_CPP} ${DemoUI_H})

#QT4_AUTOMOC(${DemoUI_Sources})

#This is for moc files
INCLUDE_DIRECTORIES(${CMAKE_CURRENT_BINARY_DIR})

ADD_EXECUTABLE(DemoUI ${DemoUI_Sources})

TARGET_LINK_LIBRARIES(DemoUI   PRIVATE Qt${QT_VERSION_MAJOR}::Widgets    Qt${QT_VERSION_MAJOR}::Script   Cornucopia ${QT_LIBRARIES})

INSTALL( TARGETS DemoUI RUNTIME DESTINATION bin )

IF(WIN32)
    INSTALL(FILES
        "${QT_BINARY_DIR}/QtCore${QT_VERSION_MAJOR}.dll"
        "${QT_BINARY_DIR}/QtGui${QT_VERSION_MAJOR}.dll"
        "${QT_BINARY_DIR}/QtScript${QT_VERSION_MAJOR}.dll"
        DESTINATION bin
    )
ENDIF(WIN32)
