cmake_minimum_required(VERSION 2.8)

Project(test)
ADD_EXECUTABLE(main firstOpenGL.c)

IF(APPLE)
   INCLUDE_DIRECTORIES ( /System/Library/Frameworks )
   FIND_LIBRARY(COCOA_LIBRARY Cocoa)
   FIND_LIBRARY(GLUT_LIBRARY GLUT )
   FIND_LIBRARY(OpenGL_LIBRARY OpenGL )
   MARK_AS_ADVANCED (COCOA_LIBRARY
                     GLUT_LIBRARY
                     OpenGL_LIBRARY)
   SET(EXTRA_LIBS ${COCOA_LIBRARY} ${GLUT_LIBRARY} ${OpenGL_LIBRARY})
ENDIF (APPLE)

IF(CMAKE_SYSTEM_NAME MATCHES Linux)
	include_directories(/usr/X11R6/include/)
	link_directories(/usr/X11R6/lib)
	SET(EXTRA_LIBS GL X11 GLU glut)
ENDIF (CMAKE_SYSTEM_NAME MATCHES Linux)

target_link_libraries(main ${EXTRA_LIBS})

