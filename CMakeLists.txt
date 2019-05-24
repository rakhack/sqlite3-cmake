project(sqlite3)
cmake_minimum_required(VERSION 3.1)

include_directories(${CMAKE_SOURCE_DIR}/src)

add_library(sqlite3 STATIC src/sqlite3.c src/sqlite3.h src/sqlite3ext.h)

add_definitions(-DSQLITE_ENABLE_RTREE)
add_definitions(-DSQLITE_ENABLE_FTS4)
add_definitions(-DSQLITE_ENABLE_FTS5)
add_definitions(-DSQLITE_ENABLE_JSON1)
add_definitions(-DSQLITE_ENABLE_RBU)
add_definitions(-DSQLITE_ENABLE_STAT4)

# Uncomment this for single-threaded variant (faster)
#add_definitions(-DSQLITE_THREADSAFE=0)

if(NOT WIN32)
  target_link_libraries(sqlite3 pthread dl)
endif()

install(FILES src/sqlite3.h src/sqlite3ext.h DESTINATION include)
install(TARGETS sqlite3 LIBRARY DESTINATION lib ARCHIVE DESTINATION lib)
