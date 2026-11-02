cmake_minimum_required(VERSION 3.19)
project(TcpFileSender LANGUAGES CXX)

find_package(Qt6 6.5 REQUIRED COMPONENTS Core Widgets LinguistTools Network)

qt_standard_project_setup()

qt_add_executable(TcpFileSender
    WIN32 MACOSX_BUNDLE
    main.cpp
    tcpfilesender.cpp
    tcpfilesender.h
)

qt_add_translations(
    TARGETS TcpFileSender
    TS_FILES TcpFileSender_zh_TW.ts
)

# 2. 在 target_link_libraries 中加入 Qt::Network
target_link_libraries(TcpFileSender
    PRIVATE
        Qt::Core
        Qt::Widgets
        Qt::Network
)

install(TARGETS TcpFileSender
    BUNDLE  DESTINATION .
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
)

qt_generate_deploy_app_script(
    TARGET TcpFileSender
    OUTPUT_SCRIPT deploy_script
    NO_UNSUPPORTED_PLATFORM_ERROR
)
install(SCRIPT ${deploy_script})