find_package(pybind11 QUIET)
if(NOT pybind11_FOUND)#
  message("-- Cannot build the python bindings because pybind is missing.")
  return()
endif()

## Python configuration file (build tree), the lib in the source dir (easier while developping .py files)
file(WRITE "${CMAKE_BINARY_DIR}/etc/sofa/python.d/plugin.SofaPython3.bindings" "${CMAKE_BINARY_DIR}/${SP3_PYTHON_PACKAGES_DIRECTORY}\n")

## Python configuration file (install tree)
file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/installed-bindings-config"
    "${CMAKE_INSTALL_PREFIX}/${SP3_PYTHON_PACKAGES_DIRECTORY}\n")


install(FILES "${CMAKE_CURRENT_BINARY_DIR}/installed-bindings-config"
    DESTINATION "etc/sofa/python.d"
    RENAME "plugin.SofaPython3.bindings")

add_subdirectory(Sofa)
add_subdirectory(SofaRuntime)
add_subdirectory(SofaTypes)