ADD_DEFINITIONS(-DOTL_ODBC)
SET(LIBRARY_NAME osgdb_otl)
SET(LIBRARY_FILES ReaderWriterOTL.cpp)

IF(WIN32)
    SET(EXTERNAL_LIBRARIES odbc32.lib)
ENDIF(WIN32)
START_LIBRARY()
