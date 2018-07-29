set(SOURCES BaseRenderer.cpp
            ColorManager.cpp
            OverlayRenderer.cpp
            OverlayRendererGUI.cpp
            OverlayRendererUtil.cpp
            RenderCapture.cpp
            RenderFactory.cpp
            RenderFlags.cpp
            RenderManager.cpp
            DebugRenderer.cpp)

set(HEADERS BaseRenderer.h
            ColorManager.h
            OverlayRenderer.h
            OverlayRendererGUI.h
            OverlayRendererUtil.h
            RenderCapture.h
            RenderFactory.h
            RenderFlags.h
            RenderInfo.h
            RenderManager.h
            DebugRenderer.h)

if(CORE_SYSTEM_NAME STREQUAL windows OR CORE_SYSTEM_NAME STREQUAL windowsstore)
  list(APPEND SOURCES WinRenderer.cpp
                      WinRenderBuffer.cpp
                      OverlayRendererDX.cpp)
  list(APPEND HEADERS WinRenderer.h
                      WinRenderBuffer.h
                      OverlayRendererDX.h)
endif()

if (OPENGL_FOUND OR OPENGLES_FOUND)
  list(APPEND SOURCES OverlayRendererGL.cpp)
  list(APPEND HEADERS OverlayRendererGL.h)
endif()

if(OPENGL_FOUND)
  list(APPEND SOURCES LinuxRendererGL.cpp
                      FrameBufferObject.cpp)
  list(APPEND HEADERS LinuxRendererGL.h
                      FrameBufferObject.h)
endif()

if(OPENGLES_FOUND AND (CORE_PLATFORM_NAME_LC STREQUAL android OR
                       CORE_PLATFORM_NAME_LC STREQUAL ios OR
                       CORE_PLATFORM_NAME_LC STREQUAL aml OR
                       CORE_PLATFORM_NAME_LC STREQUAL gbm OR
                       CORE_PLATFORM_NAME_LC STREQUAL wayland))
  list(APPEND SOURCES LinuxRendererGLES.cpp
                      FrameBufferObject.cpp)
  list(APPEND HEADERS LinuxRendererGLES.h
                      FrameBufferObject.cpp)
endif()

if(ARCH MATCHES arm AND ENABLE_NEON)
  list(APPEND SOURCES yuv2rgb.neon.S)
  list(APPEND HEADERS yuv2rgb.neon.h)
  if(NOT DEFINED NEON_FLAGS)
    set_source_files_properties(yuv2rgb.neon.S PROPERTIES COMPILE_OPTIONS -mfpu=neon)
  endif()
endif()

core_add_library(videorenderers)
