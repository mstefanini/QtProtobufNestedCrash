cmake_minimum_required(VERSION 3.16)
include(CMakePrintHelpers)

project(QtProtobufNestedCrash VERSION 0.1 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(Qt6 REQUIRED COMPONENTS Quick Protobuf)

qt_standard_project_setup(REQUIRES 6.5)

qt_add_executable(appQtProtobufNestedCrash
    main.cpp
)

qt_add_qml_module(appQtProtobufNestedCrash
    URI QtProtobufNestedCrash
    VERSION 1.0
    QML_FILES
        Main.qml
)

qt_add_protobuf(appQtProtobufNestedCrash
    GENERATE_PACKAGE_SUBFOLDERS
    PROTO_FILES
        "proto/project.proto"
    PROTO_INCLUDES
        "/proto"
)

# Qt for iOS sets MACOSX_BUNDLE_GUI_IDENTIFIER automatically since Qt 6.1.
# If you are developing for iOS or macOS you should consider setting an
# explicit, fixed bundle identifier manually though.
set_target_properties(appQtProtobufNestedCrash PROPERTIES
#    MACOSX_BUNDLE_GUI_IDENTIFIER com.example.appQtProtobufNestedCrash
    MACOSX_BUNDLE_BUNDLE_VERSION ${PROJECT_VERSION}
    MACOSX_BUNDLE_SHORT_VERSION_STRING ${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}
    MACOSX_BUNDLE TRUE
    WIN32_EXECUTABLE TRUE
)

target_link_libraries(appQtProtobufNestedCrash
    PRIVATE Qt6::Quick
    PRIVATE Qt6::Protobuf
)

include(GNUInstallDirs)
install(TARGETS appQtProtobufNestedCrash
    BUNDLE DESTINATION .
    LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}
)
