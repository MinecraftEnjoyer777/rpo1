cmake_minimum_required(VERSION 3.22.1)

# Declares and names the project.

project("fclient")

# Creates and names a library, sets it as either STATIC
# or SHARED, and provides the relative paths to its source code.
# You can define multiple libraries, and CMake builds them for you.
# Gradle automatically packages shared libraries with your APK.
add_library(spdlog STATIC IMPORTED)
add_library(native-lib SHARED C:/Users/Ilya/AndroidStudioProjects/fclient/app/src/main/cpp/native-lib.cpp)

set_target_properties(spdlog PROPERTIES IMPORTED_LOCATION
        C:/Users/Ilya/AndroidStudioProjects/libs/spdlog/build/x86_64/libspdlog.a)
target_include_directories(native-lib PUBLIC
        C:/Users/Ilya/AndroidStudioProjects/libs/spdlog/spdlog/include)

# Links the target library to the log library included in the NDK.
find_library( log-lib log )

# Specifies libraries CMake should link to your target library. You
# can link multiple libraries, such as libraries you define in this
# build script, prebuilt third-party libraries, or system libraries.

target_link_libraries( # Specifies the target library.
        native-lib
        spdlog
        # Links the target library to the log library included in the NDK.
        ${log-lib}
        )