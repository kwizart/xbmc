set(SOURCES GUIWindowTestPatternGL.cpp
            RenderSystemGL.cpp
            ../MatrixGL.cpp
            GLShader.cpp)

set(HEADERS GUIWindowTestPatternGL.h
            RenderSystemGL.h
            ../MatrixGL.h
            GLShader.h)

if(ARCH MATCHES arm AND ENABLE_NEON)
  if (CMAKE_SIZEOF_VOID_P EQUAL 4)
    list(APPEND SOURCES ../MatrixGL.neon.cpp)
    set_source_files_properties(../MatrixGL.neon.cpp PROPERTIES COMPILE_OPTIONS -mfpu=neon)
  endif()
endif()

core_add_library(rendering_gl)
