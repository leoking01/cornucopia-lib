# Cornucopia library CMakeLists.txt
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O3  -g   -fPIC")


FILE(GLOB Cornucopia_CPP "*.cpp")
FILE(GLOB Cornucopia_H "*.h")
LIST(APPEND Cornucopia_Sources ${Cornucopia_CPP} ${Cornucopia_H})

ADD_LIBRARY( Cornucopia STATIC ${Cornucopia_Sources} )

#target_link_libraries(Cornucopia PRIVATE Qt${QT_VERSION_MAJOR}::Widgets
#    )

INSTALL( TARGETS Cornucopia ARCHIVE DESTINATION lib )

INSTALL( DIRECTORY . DESTINATION include FILES_MATCHING PATTERN "*.h"  )
