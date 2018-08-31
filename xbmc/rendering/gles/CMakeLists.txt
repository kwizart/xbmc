if(OPENGLES_FOUND)
  set(SOURCES RenderSystemGLES.cpp
              ../MatrixGL.cpp
              ../MatrixGL_neon.cpp
              GLESShader.cpp)

  set(HEADERS RenderSystemGLES.h
              ../MatrixGL.h
              GLESShader.h)

  if(HAVE_NEON)
    if(CMAKE_SIZEOF_VOID_P EQUAL 4)
      set_source_files_properties(../MatrixGL_neon.cpp PROPERTIES COMPILE_OPTIONS -mfpu=neon)
    endif()
  endif()

  core_add_library(rendering_gles)
endif()
