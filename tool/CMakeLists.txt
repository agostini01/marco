add_custom_target(MARCO-Tools)

add_subdirectory(marco-lsp)
if (MARCO_ENABLE_DRIVER)
  add_subdirectory(marco-driver)
endif()

add_subdirectory(marco-opt)
add_subdirectory(marco-verifier)
