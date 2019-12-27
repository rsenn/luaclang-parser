cmake_minimum_required(VERSION 2.6)
project(luaclang CXX)

set(CMAKE_INSTALL_PREFIX /opt/openresty/luajit)



find_package(Lua51 REQUIRED)
find_library(CLANG_LIBRARY NAMES clang libclang)

if(APPLE)
   set(CMAKE_SHARED_MODULE_CREATE_CXX_FLAGS
       "${CMAKE_SHARED_MODULE_CREATE_CXX_FLAGS} -flat_namespace -undefined dynamic_lookup")
endif(APPLE)

include_directories(${LUA_INCLUDE_DIR})
add_library(luaclang-parser MODULE luaclang-parser.cpp)
target_link_libraries(luaclang-parser ${CLANG_LIBRARY} ${LUA_LIBRARIES})
set_target_properties(luaclang-parser PROPERTIES PREFIX "")

install(TARGETS luaclang-parser DESTINATION lib/lua/5.1)
