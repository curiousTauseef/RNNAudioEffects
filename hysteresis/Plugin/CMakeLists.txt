cmake_minimum_required(VERSION 3.4)

project("RNNHysteresis")

# FRUT stuff
list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/FRUT/prefix/FRUT/cmake")
include(Reprojucer)

# comment to use STL implementation instead of Eigen
add_definitions(-DUSE_EIGEN)

jucer_project_begin(
    JUCER_VERSION "5.4.7"
    PROJECT_FILE "${RNNHysteresis_jucer_FILE}"
    PROJECT_ID "gSwrk"
)

jucer_project_settings(
    PROJECT_NAME "RNNHysteresis"
    PROJECT_VERSION "1.0.0"
    COMPANY_NAME "chowdsp"
    COMPANY_COPYRIGHT "Jatin Chowdhury"
    REPORT_JUCE_APP_USAGE OFF
    DISPLAY_THE_JUCE_SPLASH_SCREEN OFF
    PROJECT_TYPE "Audio Plug-in"
    BUNDLE_IDENTIFIER "com.chowdsp.RNNHysteresis"
    CXX_LANGUAGE_STANDARD "C++17"
    HEADER_SEARCH_PATHS
        ${CMAKE_CURRENT_LIST_DIR}/../../PluginCode/
)

jucer_audio_plugin_settings(
    PLUGIN_FORMATS
        VST3
        AU
        Standalone
    PLUGIN_NAME "RNNHysteresis"
    PLUGIN_DESCRIPTION "RNNHysteresis"
    PLUGIN_MANUFACTURER "chowdsp"
    PLUGIN_MANUFACTURER_CODE "JAC"
    PLUGIN_CODE "PEYG"
    PLUGIN_AU_EXPORT_PREFIX "RNNHysteresisAU"
)

add_subdirectory(../../PluginCode shared_build)

jucer_project_files("Source"
# Compile   Xcode     Binary    File
#           Resource  Resource
  .         .         .         "${CMAKE_CURRENT_LIST_DIR}/RNNHysteresisPlugin.h"
  x         .         .         "${CMAKE_CURRENT_LIST_DIR}/RNNHysteresisPlugin.cpp"
  .         .         x         "${CMAKE_CURRENT_LIST_DIR}/../models/hysteresis_full.json"
  .         .         x         "${CMAKE_CURRENT_LIST_DIR}/../models/hysteresis_small.json"
)

# JUCE modules
jucer_project_module(
    juce_audio_basics
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_audio_devices
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_audio_plugin_client
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
    JUCE_VST3_CAN_REPLACE_VST2 OFF
)

jucer_project_module(
    juce_audio_formats
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_audio_processors
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_audio_utils
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_core
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_data_structures
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_dsp
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_events
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_graphics
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_opengl
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_gui_basics
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    juce_gui_extra
    PATH "${CMAKE_CURRENT_LIST_DIR}/../../modules/JUCE/modules"
)

jucer_project_module(
    foleys_gui_magic
    PATH "$\{CMAKE_CURRENT_LIST_DIR\}/../../modules"
    FOLEYS_SHOW_GUI_EDITOR_PALLETTE OFF # Turn on to edit your GUI!
)

jucer_export_target(
    "Xcode (MacOSX)"
    EXTERNAL_LIBRARIES_TO_LINK PluginCode
)

jucer_export_target_configuration(
    "Xcode (MacOSX)"
    NAME "Debug"
    DEBUG_MODE ON
    BINARY_NAME "RNNHysteresis"
)

jucer_export_target_configuration(
    "Xcode (MacOSX)"
    NAME "Release"
    DEBUG_MODE OFF
    BINARY_NAME "RNNHysteresis"
)

jucer_export_target(
    "Visual Studio 2017"
    EXTRA_PREPROCESSOR_DEFINITIONS
        _CRT_SECURE_NO_WARNINGS
    EXTERNAL_LIBRARIES_TO_LINK PluginCode
)

jucer_export_target_configuration(
    "Visual Studio 2017"
    NAME "Debug"
    DEBUG_MODE ON
    BINARY_NAME "RNNHysteresis"
)

jucer_export_target_configuration(
    "Visual Studio 2017"
    NAME "Release"
    DEBUG_MODE OFF
    BINARY_NAME "RNNHysteresis"
)

jucer_export_target(
    "Linux Makefile"
    EXTERNAL_LIBRARIES_TO_LINK PluginCode
)

jucer_export_target_configuration(
    "Linux Makefile"
    NAME "Debug"
    DEBUG_MODE ON
    BINARY_NAME "RNNHysteresis"
)

jucer_export_target_configuration(
    "Linux Makefile"
    NAME "Release"
    DEBUG_MODE OFF
    BINARY_NAME "RNNHysteresis"
)

jucer_project_end()
