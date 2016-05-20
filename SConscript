"""
SConscript

This file is used by SCons to learn what to build for this project, along
with metadata about the interface and dependencies of the project.
"""

import os

# Import the default build environments for all supported build platforms.
Import("platformEnvironments")

# Define products tree
products = {}

#### LuaLibrary

# This is the name of the project, used to form the names of build products.
name = "LuaLibrary"

# List directories containing external interfaces here.
interface = [
    Dir("src")
]

# If the project depends on libraries from another project
# in the workspace, list their product trees here.
deps = [
]

# List all supported platforms here.
# For each one, list any platform-specific environment variables.
platforms = {
    "Linux": {
        "LIBS": [
            "m",
        ],
    },
}

# Build the project for every supported platform.  The platform must be
# listed in this project in the platforms list and must have a
# corresponding platform build environment in order for the project
# to be built for that platform.
products[name] = {}
for platform in platforms:
    if platform not in platformEnvironments:
        continue
    env = platformEnvironments[platform].Clone(
        PRODUCT = "lua"
    )
    env.AppendUnique(**platforms[platform])
    env.Append(CPPDEFINES = [])
    env.Append(CPPPATH = [])
    env.Replace(SOURCE_DIRECTORIES = ["src"])
    env.Append(
        SOURCE_EXCLUDE = [
            "src/lua.c",
            "src/luac.c",
        ]
    )
    products[name][platform] = env.LibraryProject(
        name,
        platform,
        interface,
        deps,
    )

#### LuaInterpreter

# This is the name of the project, used to form the names of build products.
name = "LuaInterpreter"

# If the project depends on libraries from another project
# in the workspace, list their product trees here.
deps = [
    products["LuaLibrary"]
]

# List all supported platforms here.
# For each one, list any platform-specific environment variables.
platforms = {
    "Linux": {
        "LIBS": [
        ],
    },
}

# Build the project for every supported platform.  The platform must be
# listed in this project in the platforms list and must have a
# corresponding platform build environment in order for the project
# to be built for that platform.
products[name] = {}
for platform in platforms:
    if platform not in platformEnvironments:
        continue
    env = platformEnvironments[platform].Clone(
        PRODUCT = "lua"
    )
    env.AppendUnique(**platforms[platform])
    env.Append(CPPDEFINES = [])
    env.Append(CPPPATH = [])
    env.Replace(SOURCE_DIRECTORIES = [])
    env.Append(
        SOURCE_INCLUDE = [
            "src/lua.c",
        ]
    )
    products[name][platform] = env.ProgramProject(
        name,
        platform,
        deps
    )

#### LuaCompiler

# This is the name of the project, used to form the names of build products.
name = "LuaCompiler"

# If the project depends on libraries from another project
# in the workspace, list their product trees here.
deps = [
    [products["LuaLibrary"], "static"]
]

# List all supported platforms here.
# For each one, list any platform-specific environment variables.
platforms = {
    "Linux": {
        "LIBS": [
        ],
    },
}

# Build the project for every supported platform.  The platform must be
# listed in this project in the platforms list and must have a
# corresponding platform build environment in order for the project
# to be built for that platform.
products[name] = {}
for platform in platforms:
    if platform not in platformEnvironments:
        continue
    env = platformEnvironments[platform].Clone(
        PRODUCT = "luac"
    )
    env.AppendUnique(**platforms[platform])
    env.Append(CPPDEFINES = [])
    env.Append(CPPPATH = [])
    env.Replace(SOURCE_DIRECTORIES = [])
    env.Append(
        SOURCE_INCLUDE = [
            "src/luac.c",
        ]
    )
    products[name][platform] = env.ProgramProject(
        name,
        platform,
        deps
    )

# Return products tree
Return("products")
