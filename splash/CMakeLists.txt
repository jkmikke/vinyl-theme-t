cmake_minimum_required(VERSION 3.16)

set(VINYL_SPLASH_PLUGIN_ID "com.ekaaty.vinyl-splash")

if( CMAKE_SOURCE_DIR STREQUAL CMAKE_CURRENT_SOURCE_DIR ) 
  # We are building standalone
  project(vinyl-splash)

  set(KDE_COMPILERSETTINGS_LEVEL "5.82")
  set(KF6_MIN_VERSION "6.7.0")
  set(PLASMA_MIN_VERSION "6.2.0")
  set(QT_MIN_VERSION "6.7.0")
  
  find_package(ECM ${KF6_MIN_VERSION} REQUIRED NO_MODULE)
  set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${ECM_MODULE_PATH} ${CMAKE_SOURCE_DIR}/cmake)

  find_package(Qt6 ${QT_MIN_VERSION} REQUIRED CONFIG COMPONENTS
    Core 
    Quick
  )

  find_package(KF6 ${KF6_MIN_VERSION} REQUIRED COMPONENTS
    Config
    CoreAddons
    DocTools
    I18n
    Package
  )

  find_package(Plasma ${PLASMA_MIN_VERSION} REQUIRED)

  set(KDE_INSTALL_LOCALEDIR ${KDE_INSTALL_DATADIR}/plasma/look-and-feel/${VINYL_SPLASH_PLUGIN_ID}/contents/locale)
else()  
  # We are building as part of Main project

  set(KDE_INSTALL_LOCALEDIR share/locale)
endif()

plasma_install_package(package ${VINYL_SPLASH_PLUGIN_ID} look-and-feel)

add_definitions(-DTRANSLATION_DOMAIN=\"plasma_lookandfeel_${VINYL_SPLASH_PLUGIN_ID}\")
kdoctools_install(po)
ki18n_install(po)

# vim: ts=2:sw=2:sts=2:et
