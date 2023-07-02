cmake_minimum_required(VERSION 3.20)

set(NAME metis)
set(VERSION 5.1.0)

project(cmeel-${NAME} VERSION ${VERSION})

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "http://glaros.dtc.umn.edu/gkhome/fetch/sw/${NAME}/${NAME}-${VERSION}.tar.gz"
      DOWNLOAD_EXTRACT_TIMESTAMP
      OFF
  CMAKE_ARGS "-DSHARED=1" "-DCMAKE_INSTALL_PREFIX=${CMAKE_INSTALL_PREFIX}"
             "-DGKLIB_PATH=${CMAKE_BINARY_DIR}/${NAME}-prefix/src/${NAME}/GKlib"
)

# dummy file for install target
install(FILES README.md DESTINATION share/cmeel-${NAME}/)
