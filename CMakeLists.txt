cmake_minimum_required(VERSION 3.30)

set(ORG KarypisLab)
set(NAME METIS)
set(VERSION 5.2.1)
set(EXT tar.gz)
set(SHA256 1a4665b2cd07edc2f734e30d7460afb19c1217c2547c2ac7bf6e1848d50aff7a)
set(TAG_PREFIX refs/tags/v)

project("cmeel-${NAME}" VERSION "${VERSION}")

find_path(GKLIB_PATH NAMES "include/GKlib.h")

include(ExternalProject)
ExternalProject_Add(
  ${NAME}
  URL "https://github.com/${ORG}/${NAME}/archive/${TAG_PREFIX}${VERSION}.${EXT}"
  URL_HASH "SHA256=${SHA256}"
  DOWNLOAD_EXTRACT_TIMESTAMP OFF
  BUILD_IN_SOURCE ON
  CONFIGURE_COMMAND "make" "config" "shared=1"
      "prefix=${CMAKE_INSTALL_PREFIX}" "gklib_path=${GKLIB_PATH}"
  BUILD_COMMAND "make" "-i"
  INSTALL_COMMAND "make" "install" "-i"
  )

# dummy file for install target
install(FILES "README.md" DESTINATION "share/cmeel-${NAME}/")
