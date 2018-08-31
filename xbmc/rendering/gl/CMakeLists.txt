set(SOURCES GUIWindowTestPatternGL.cpp
            RenderSystemGL.cpp
            ../MatrixGL.cpp
            ../MatrixGL_neon.cpp
            GLShader.cpp)

set(HEADERS GUIWindowTestPatternGL.h
            RenderSystemGL.h
            ../MatrixGL.h
            GLShader.h)

if(HAVE_NEON)
  if(CMAKE_SIZEOF_VOID_P EQUAL 4)
    set_source_files_properties(../MatrixGL_neon.cpp PROPERTIES COMPILE_OPTIONS -mfpu=neon)
  endif()
endif()

core_add_library(rendering_gl)
