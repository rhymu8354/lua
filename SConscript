"""
SConscript

This file is used by SCons as a blueprint for how to build this
component as a program (linked executable).
"""

import os

# Import the default build environments for all supported build platforms.
Import("platformEnvironments")

# Import other projects in the workspace on which this project depends.
#Import("<other project name>")

# This is the name of the project, used to form the names of build products
# such as the executable file name and the name of the directory
# containing the object code.
name = "lua"

# List all supported platforms here.
# For each one, list any platform-specific dependencies.
platforms = {
    "arm-linux": {
        # If the project depends on object/library code from another project
        # in the workspace, list their build nodes here.
        "deps": [
        ],

        # If the project depends on additional system libraries,
        # list their names here.
        "libs": [
            "m",
        ],
    },
}

# Build the program for every supported platform.  The platform must be
# listed in this project in the platforms list and must have a
# corresponding platform build environment in order for the project
# to be built for that platform.
products = {
    "interface": [Dir("src")],
    "library": {}
}
for platform in platforms:
    if platform not in platformEnvironments:
        continue
    env = platformEnvironments[platform].Clone()
    env.Append(CPPDEFINES = [])
    env.Append(CPPPATH = [])
    env.Append(SOURCE_DIRECTORIES = ["src"])
    env.Append(
        SOURCE_EXCLUDE = [
            "src/lua.c",
            "src/luac.c",
        ]
    )
    products["library"][platform] = env.LibraryProject(
        name,
        platforms[platform]["deps"],
        platforms[platform]["libs"]
    )
Return("products")
