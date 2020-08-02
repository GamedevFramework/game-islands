cmake_minimum_required(VERSION 3.10)

project(ISLANDS
  VERSION 0.1.0
)

include(GNUInstallDirs)

find_package(gf REQUIRED COMPONENTS graphics)

set(ISLANDS_DATA_DIR "${CMAKE_INSTALL_PREFIX}/share/games/islands")
configure_file(${CMAKE_CURRENT_SOURCE_DIR}/code/config.h.in ${CMAKE_CURRENT_BINARY_DIR}/config.h @ONLY)

add_executable(islands
  code/islands.cc
  code/local/Compass.cc
  code/local/DecorationManager.cc
  code/local/Gold.cc
  code/local/Hero.cc
  code/local/Sea.cc
  code/local/Singletons.cc
  code/local/Steam.cc
  code/local/TreasureManager.cc
  code/local/TurretManager.cc
  code/local/WaveManager.cc
)

target_include_directories(islands
  PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/code
    ${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(islands
  PRIVATE
    gf::graphics
)

install(
  TARGETS islands
  RUNTIME DESTINATION "${CMAKE_INSTALL_BINDIR}"
)

install(
  DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}/data/islands"
  DESTINATION "${CMAKE_INSTALL_DATAROOTDIR}/games"
)
