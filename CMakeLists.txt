cmake_minimum_required(VERSION 3.8)

if(MSVC)
    add_definitions(
        -D_CRT_SECURE_NO_WARNINGS
    )
endif(MSVC)

add_library(LuaLibrary STATIC
    src/lapi.c
    src/lapi.h
    src/lauxlib.c
    src/lauxlib.h
    src/lbaselib.c
    src/lbitlib.c
    src/lcode.c
    src/lcode.h
    src/lcorolib.c
    src/lctype.c
    src/lctype.h
    src/ldblib.c
    src/ldebug.c
    src/ldebug.h
    src/ldo.c
    src/ldo.h
    src/ldump.c
    src/lfunc.c
    src/lfunc.h
    src/lgc.c
    src/lgc.h
    src/linit.c
    src/liolib.c
    src/llex.c
    src/llex.h
    src/llimits.h
    src/lmathlib.c
    src/lmem.c
    src/lmem.h
    src/loadlib.c
    src/lobject.c
    src/lobject.h
    src/lopcodes.c
    src/lopcodes.h
    src/loslib.c
    src/lparser.c
    src/lparser.h
    src/lprefix.h
    src/lstate.c
    src/lstate.h
    src/lstring.h
    src/lstring.c
    src/lstrlib.c
    src/ltable.c
    src/ltable.h
    src/ltablib.c
    src/ltm.c
    src/ltm.h
    src/lua.h
    src/lua.hpp
    src/luaconf.h
    src/lualib.h
    src/lundump.c
    src/lundump.h
    src/lutf8lib.c
    src/lvm.c
    src/lvm.h
    src/lzio.c
    src/lzio.h
)
target_include_directories(LuaLibrary PUBLIC src)
set_target_properties(LuaLibrary PROPERTIES
    FOLDER Libraries/lua
)

add_executable(LuaInterpreter
    src/lua.c
)
target_link_libraries(LuaInterpreter
    LuaLibrary
)
if(UNIX)
    target_link_libraries(LuaInterpreter m)
endif(UNIX)
set_target_properties(LuaInterpreter PROPERTIES 
    OUTPUT_NAME lua
    FOLDER Libraries/lua
)

add_executable(LuaCompiler
    src/luac.c
)
target_link_libraries(LuaCompiler
    LuaLibrary
)
if(UNIX)
    target_link_libraries(LuaCompiler m)
endif(UNIX)
set_target_properties(LuaCompiler PROPERTIES 
    OUTPUT_NAME luac
    FOLDER Libraries/lua
)
