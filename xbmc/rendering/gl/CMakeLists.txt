set(SOURCES GUIWindowTestPatternGL.cpp
            RenderSystemGL.cpp
            ../MatrixGL.cpp
            GLShader.cpp)

set(HEADERS GUIWindowTestPatternGL.h
            RenderSystemGL.h
            ../MatrixGL.h
            GLShader.h)

if(ARCH MATCHES arm)
  if(HAVE_NEON)
    list(APPEND SOURCES ../MatrixGL.neon.cpp)
    set_source_files_properties(../MatrixGL.neon.cpp PROPERTIES COMPILE_OPTIONS -mfpu=neon)
  endif()
endif()

core_add_library(rendering_gl)
