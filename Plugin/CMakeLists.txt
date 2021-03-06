cmake_minimum_required(VERSION 3.15)
set(CMAKE_OSX_DEPLOYMENT_TARGET "10.12" CACHE STRING "Minimum OS X deployment target")
set(CMAKE_CXX_STANDARD 17)
project(CHOWTapeModel VERSION 2.7.2)

add_subdirectory(modules)
include_directories(modules/RTNeural)

# set up plugin project
# juce_set_vst2_sdk_path(C:/SDKs/VST_SDK/VST2_SDK/)
# include_directories(C:/SDKs/asiosdk2.3/common)

juce_add_plugin(CHOWTapeModel
    COMPANY_NAME chowdsp
    PLUGIN_MANUFACTURER_CODE Chow
    PLUGIN_CODE Jdox
    FORMATS AU VST3 Standalone LV2 #VST
    ProductName "CHOWTapeModel"
    LV2_URI https://github.com/jatinchowdhury18/AnalogTapeModel
    ICON_BIG Source/GUI/Assets/logo.png
)

# create JUCE header
juce_generate_juce_header(CHOWTapeModel)

add_subdirectory(Source)

target_compile_definitions(CHOWTapeModel
    PUBLIC
    JUCE_DISPLAY_SPLASH_SCREEN=0
    JUCE_REPORT_APP_USAGE=0
    JUCE_WEB_BROWSER=0
    JUCE_USE_CURL=0
    JUCE_VST3_CAN_REPLACE_VST2=0
)

target_link_libraries(CHOWTapeModel PUBLIC
    juce_plugin_modules
)

# we need these flags for notarization on MacOS
option(MACOS_RELEASE "Set build flags for MacOS Release" OFF)
if(MACOS_RELEASE)
    message(STATUS "Setting MacOS release flags...")
    set_target_properties(CHOWTapeModel_Standalone PROPERTIES
        XCODE_ATTRIBUTE_ENABLE_HARDENED_RUNTIME YES)
    # set_target_properties(ChowCentaur_AUv3 PROPERTIES
    #     XCODE_ATTRIBUTE_ENABLE_HARDENED_RUNTIME YES)
endif()
