set(CMAKE_AUTORCC ON)

pkg_check_modules(XKBCommon REQUIRED IMPORTED_TARGET xkbcommon)

add_executable(tastenbrett
    application.cpp
    doodad.cpp
    geometry.cpp
    key.cpp
    main.cpp
    outline.cpp
    qml.qrc
    row.cpp
    section.cpp
    shape.cpp
    xkbobject.cpp
)

target_compile_definitions(tastenbrett
    PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)

target_link_libraries(tastenbrett
    PRIVATE
        Qt5::Core
        Qt5::Quick
        Qt5::Gui
        Qt5::X11Extras
        XCB::XCB
        PkgConfig::XKBCommon
        ${X11_Xkbfile_LIB}
        ${X11_LIBRARIES}
)

install(TARGETS tastenbrett DESTINATION ${KDE_INSTALL_TARGETS_DEFAULT_ARGS})
