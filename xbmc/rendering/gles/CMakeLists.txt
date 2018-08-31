if(OPENGLES_FOUND)
  set(SOURCES RenderSystemGLES.cpp
              ../MatrixGL.cpp
              GLESShader.cpp)

  set(HEADERS RenderSystemGLES.h
              ../MatrixGL.h
              GLESShader.h)

  if(ARCH MATCHES arm)
    if(CMAKE_SIZEOF_VOID_P EQUAL 4)
      list(APPEND SOURCES ../MatrixGL.neon.cpp)
      set_source_files_properties(../MatrixGL.neon.cpp PROPERTIES COMPILE_OPTIONS -mfpu=neon)
    endif()
  endif()

  core_add_library(rendering_gles)
endif()
