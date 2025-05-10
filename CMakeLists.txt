cmake_minimum_required(VERSION 3.19)
project(ConnText-Desktop LANGUAGES CXX)

find_package(Qt6 6.5 REQUIRED COMPONENTS Core Widgets LinguistTools)

qt_standard_project_setup()

qt_add_executable(ConnText-Desktop
    WIN32 MACOSX_BUNDLE
    "sources/main.cpp"
    "sources/mainwindow.cpp"
    "headers/mainwindow.h"
    "forms/mainwindow.ui"
)

set_property(TARGET ConnText-Desktop PROPERTY AUTOUIC_SEARCH_PATHS "${CMAKE_SOURCE_DIR}/forms")

qt_add_translations(
    TARGETS ConnText-Desktop
    TS_FILES ConnText-Desktop_en_GB.ts
)

target_link_libraries(ConnText-Desktop PRIVATE
    Qt::Core
    Qt::Widgets
)

target_include_directories(ConnText-Desktop PRIVATE
    "${CMAKE_BINARY_DIR}"
    # "${CMAKE_BINARY_DIR}/ui_${PROJECT_NAME}_autogen/include"
    "${CMAKE_SOURCE_DIR}/headers"
)

include(GNUInstallDirs)

install(TARGETS ConnText-Desktop
    BUNDLE DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET ConnText-Desktop
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})
