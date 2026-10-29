# Generate and install the CMake package (MARCOConfig.cmake) so that external
# projects can use the installed MARCO libraries:
#
#   find_package(MLIR REQUIRED CONFIG)
#   find_package(MARCO REQUIRED CONFIG)
#   include_directories(${MARCO_INCLUDE_DIRS})
#   target_link_libraries(<target> PRIVATE marco::MLIRBaseModelica)

set(MARCO_INSTALL_PACKAGE_DIR "${CMAKE_INSTALL_LIBDIR}/cmake/marco")

# add_mlir_library() and marco_add_library() put every installed library in
# the MLIRTargets export set.
install(EXPORT MLIRTargets
    FILE MARCOTargets.cmake
    NAMESPACE marco::
    DESTINATION ${MARCO_INSTALL_PACKAGE_DIR}
    COMPONENT marco-cmake-exports)

configure_file(
    ${CMAKE_CURRENT_SOURCE_DIR}/MARCOConfig.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/MARCOConfig.cmake
    @ONLY)

install(FILES ${CMAKE_CURRENT_BINARY_DIR}/MARCOConfig.cmake
    DESTINATION ${MARCO_INSTALL_PACKAGE_DIR}
    COMPONENT marco-cmake-exports)
