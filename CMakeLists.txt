add_library(opengl-loader STATIC)

target_compile_definitions(opengl-loader PUBLIC -DCERLIB_HAVE_OPENGL)

if (EMSCRIPTEN OR ANDROID OR IOS)
  set(gladDir ${CMAKE_CURRENT_SOURCE_DIR}/GLES)
  target_compile_definitions(opengl-loader PUBLIC -DCERLIB_GFX_IS_GLES)
else ()
  set(gladDir ${CMAKE_CURRENT_SOURCE_DIR}/desktop)
endif ()

target_sources(opengl-loader PRIVATE
  ${gladDir}/glad.h
  ${gladDir}/glad.c
  ${gladDir}/khrplatform.h
)

target_include_directories(opengl-loader SYSTEM PUBLIC ${gladDir})

set_target_properties(opengl-loader PROPERTIES FOLDER "cerlib")
