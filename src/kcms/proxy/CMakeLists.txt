add_library(kcm_proxy MODULE)

kcoreaddons_desktop_to_json(kcm_proxy proxy.desktop)
target_sources(kcm_proxy PRIVATE
    kproxydlg.cpp
    ../ksaveioconfig.cpp
)

ki18n_wrap_ui(kcm_proxy
    kproxydlg.ui
)

target_link_libraries(kcm_proxy PRIVATE
    Qt${QT_MAJOR_VERSION}::Widgets
    KF5::CoreAddons
    KF5::ConfigCore
    KF5::I18n
    KF5::ConfigWidgets
    KF5::KIOWidgets
)

install(TARGETS kcm_proxy DESTINATION ${KDE_INSTALL_PLUGINDIR})
if (NOT WIN32)
    add_custom_target(kcm_proxy_link ALL
                    COMMAND ${CMAKE_COMMAND} -E create_symlink ../../../kcm_proxy.so ${CMAKE_CURRENT_BINARY_DIR}/kcm_proxy.so)
    install(FILES ${CMAKE_CURRENT_BINARY_DIR}/kcm_proxy.so DESTINATION ${KDE_INSTALL_PLUGINDIR}/plasma/kcms/systemsettings_qwidgets)
endif()

install(FILES proxy.desktop DESTINATION  ${KDE_INSTALL_KSERVICESDIR})
