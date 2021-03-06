PROJECT(OSG_Integrations)

SET(CMAKE_MODULE_PATH "${PROJECT_SOURCE_DIR};${CMAKE_MODULE_PATH}")
SET(CMAKE_DEBUG_POSTFIX "d" CACHE STRING "add a postfix, usually d on windows")
INCLUDE(CheckIncludeFiles)
FIND_PACKAGE(OpenGL)
FIND_PACKAGE(GLEW)

IF(WIN32)
    IF(MSVC)
        ADD_DEFINITIONS(-D_SCL_SECURE_NO_WARNINGS)
        ADD_DEFINITIONS(-D_CRT_SECURE_NO_DEPRECATE)
    ENDIF(MSVC)
ELSE(WIN32)
    SET(CMAKE_CXX_FLAGS "-W -Wall -Wno-unused")
ENDIF(WIN32)

FIND_PATH(OPENSCENEGRAPH_INCLUDE_DIR osg/Referenced
    PATHS
    $ENV{OSG_ROOT}/include
    $ENV{OSG_DIR}/include
    /usr/include 
    /usr/local/include
)

FIND_PATH(OPENSCENEGRAPH_LIB_DIR libosg.so osg.lib
    PATHS
    $ENV{OSG_ROOT}/lib
    $ENV{OSG_DIR}/lib
    /usr/lib 
    /usr/local/lib
)

INCLUDE_DIRECTORIES(${OPENSCENEGRAPH_INCLUDE_DIR})
LINK_DIRECTORIES(${OPENSCENEGRAPH_LIB_DIR})

MACRO(START_EXAMPLE)

    INCLUDE_DIRECTORIES(${EXTERNAL_INCLUDE_DIR})
    ADD_EXECUTABLE(${EXAMPLE_NAME} ${EXAMPLE_FILES})
    SET_TARGET_PROPERTIES(${EXAMPLE_NAME} PROPERTIES DEBUG_POSTFIX "${CMAKE_DEBUG_POSTFIX}")
    
    TARGET_LINK_LIBRARIES(${EXAMPLE_NAME}
        debug osg${CMAKE_DEBUG_POSTFIX}          optimized osg
        debug osgAnimation${CMAKE_DEBUG_POSTFIX} optimized osgAnimation
        debug osgParticle${CMAKE_DEBUG_POSTFIX}  optimized osgParticle
        debug osgDB${CMAKE_DEBUG_POSTFIX}        optimized osgDB
        debug osgGA${CMAKE_DEBUG_POSTFIX}        optimized osgGA
        debug osgText${CMAKE_DEBUG_POSTFIX}      optimized osgText
        debug osgUtil${CMAKE_DEBUG_POSTFIX}      optimized osgUtil
        debug osgViewer${CMAKE_DEBUG_POSTFIX}    optimized osgViewer
        debug OpenThreads${CMAKE_DEBUG_POSTFIX}  optimized OpenThreads
        ${EXTERNAL_LIBRARIES}
    )
    INSTALL(TARGETS ${EXAMPLE_NAME} RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)

ENDMACRO(START_EXAMPLE)

#ADD_SUBDIRECTORY(osganimata)          # OSG & Animata
ADD_SUBDIRECTORY(osganttweakbar)      # OSG & AntTweakBar
ADD_SUBDIRECTORY(osgawesomium)        # OSG & Awesomium
#ADD_SUBDIRECTORY(osgberkelium)        # OSG & Berkelium
#ADD_SUBDIRECTORY(osgbox2d)            # OSG & Box2D
#ADD_SUBDIRECTORY(osgdirectwrite)      # OSG & Microsoft DirectWrite
#ADD_SUBDIRECTORY(osggameswf)          # OSG & GameSWF
#ADD_SUBDIRECTORY(osgguichan)          # OSG & GUIChan
ADD_SUBDIRECTORY(osggizmo)            # OSG & libGizmo
#ADD_SUBDIRECTORY(osgmini)             # OSG & libMini
ADD_SUBDIRECTORY(osgmicropather)      # OSG & MicroPather
ADD_SUBDIRECTORY(osgmskinect)         # OSG & Microsoft Kinect SDK
ADD_SUBDIRECTORY(osgmygui)            # OSG & MyGUI
#ADD_SUBDIRECTORY(osgnewton)           # OSG & Newton Physics
ADD_SUBDIRECTORY(osgphysx3)           # OSG & Nvidia PhysX 3.x
#ADD_SUBDIRECTORY(osgnurbs)            # OSG & openNURBS
#ADD_SUBDIRECTORY(osgois)              # OSG & OIS
ADD_SUBDIRECTORY(osgrvo2)             # OSG & RVO2
ADD_SUBDIRECTORY(osgspark)            # OSG & Spark Particle
ADD_SUBDIRECTORY(osgtuio)             # OSG & TUIO
#ADD_SUBDIRECTORY(osgtriton)           # OSG & Sundog Triton
ADD_SUBDIRECTORY(osgvlc)              # OSG & libVLC SDK
#ADD_SUBDIRECTORY(osgwoody3d)          # OSG & Woody3D
#ADD_SUBDIRECTORY(osgxaos)             # OSG & XaoS

MACRO(START_LIBRARY)

    INCLUDE_DIRECTORIES(${EXTERNAL_INCLUDE_DIR})
    ADD_LIBRARY(${LIBRARY_NAME} MODULE ${LIBRARY_FILES})
    SET_TARGET_PROPERTIES(${LIBRARY_NAME} PROPERTIES DEBUG_POSTFIX "${CMAKE_DEBUG_POSTFIX}")
    
    TARGET_LINK_LIBRARIES(${LIBRARY_NAME}
        debug osg${CMAKE_DEBUG_POSTFIX}          optimized osg
        debug osgAnimation${CMAKE_DEBUG_POSTFIX} optimized osgAnimation
        debug osgParticle${CMAKE_DEBUG_POSTFIX}  optimized osgParticle
        debug osgDB${CMAKE_DEBUG_POSTFIX}        optimized osgDB
        debug osgGA${CMAKE_DEBUG_POSTFIX}        optimized osgGA
        debug osgText${CMAKE_DEBUG_POSTFIX}      optimized osgText
        debug osgUtil${CMAKE_DEBUG_POSTFIX}      optimized osgUtil
        debug osgViewer${CMAKE_DEBUG_POSTFIX}    optimized osgViewer
        debug OpenThreads${CMAKE_DEBUG_POSTFIX}  optimized OpenThreads
        ${EXTERNAL_LIBRARIES}
    )
    INSTALL(TARGETS ${LIBRARY_NAME} RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/bin
                                    ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/lib
                                    LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/bin)

ENDMACRO(START_LIBRARY)

ADD_SUBDIRECTORY(osgdb_assimp)        # OSG & Open Asset Import Library
ADD_SUBDIRECTORY(osgdb_freeimage)     # OSG & FreeImage
ADD_SUBDIRECTORY(osgdb_otl)           # OSG & Oracle/ODBC/DB2 Template Library
