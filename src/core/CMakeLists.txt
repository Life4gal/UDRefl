set(c_options "")
if(MSVC)
  list(APPEND c_options "/wd5030")
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
  list(APPEND c_options "-Wno-attributes")
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  list(APPEND c_options "-Wno-attributes")
endif()

set(c_options_i "")
if(MSVC)
  set(c_options_i "/bigobj")
endif()

Ubpa_AddTarget(
  MODE STATIC
  RET_TARGET_NAME tname
  SOURCE
    "${PROJECT_SOURCE_DIR}/include/UDRefl"
  INC
    "${PROJECT_SOURCE_DIR}/include"
  C_OPTION
    ${c_options}
  C_OPTION_INTERFACE
    ${c_options_i}
  LIB
    Ubpa::UContainer_core
    Ubpa::UTemplate_core
)

target_precompile_headers(${tname} PRIVATE "${PROJECT_SOURCE_DIR}/include/UDRefl/UDRefl.h")
