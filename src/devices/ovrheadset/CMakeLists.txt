# Copyright (C) 2006-2020 Istituto Italiano di Tecnologia (IIT)
# All rights reserved.
#
# This software may be modified and distributed under the terms of the
# BSD-3-Clause license. See the accompanying LICENSE file for details.

yarp_prepare_plugin(ovrheadset
  CATEGORY device
  TYPE yarp::dev::OVRHeadset
  INCLUDE OVRHeadset.h
  DEPENDS "LibOVR_FOUND;glfw3_FOUND;GLEW_FOUND;OpenGL_FOUND"
  INTERNAL
  QUIET
)

if(NOT ENABLE_ovrheadset)
  return()
endif()

yarp_add_plugin(yarp_ovrheadset)

set(yarp_ovrheadset_SRCS
  OVRHeadset.cpp
  OVRHeadsetLogComponent.cpp
  TextureBuffer.cpp
  TextureStatic.cpp
  TextureBattery.cpp
  InputCallback.cpp
  GLDebug.cpp
)

set(yarp_ovrheadset_IMGS
  img-yarp-robot-64.h
  img-crosshairs.h
  img-battery-100.h
  img-battery-080.h
  img-battery-060.h
  img-battery-040.h
  img-battery-caution.h
  img-battery-low.h
  img-battery-charging.h
  img-battery-charging-080.h
  img-battery-charging-060.h
  img-battery-charging-040.h
  img-battery-charging-caution.h
  img-battery-charging-low.h
  img-battery-missing.h
)

set(yarp_ovrheadset_HDRS
  ImageType.h
  OVRHeadset.h
  OVRHeadsetLogComponent.h
  TextureBuffer.h
  TextureStatic.h
  TextureBattery.h
  InputCallback.h
  GLDebug.h
  ${yarp_ovrheadset_IMGS}
)

source_group("Texture Images"
  FILES ${yarp_ovrheadset_IMGS}
)

target_sources(yarp_ovrheadset
  PRIVATE
    ${yarp_ovrheadset_SRCS}
    ${yarp_ovrheadset_HDRS}
)

target_link_libraries(yarp_ovrheadset
  PRIVATE
    YARP::YARP_os
    YARP::YARP_sig
    YARP::YARP_dev
    YARP::YARP_math
    LibOVR::OVR
    GLEW::GLEW
    glfw
    OpenGL::GL
)

yarp_install(
  TARGETS yarp_ovrheadset
  EXPORT yarp-device-ovrheadset
  COMPONENT yarp-device-ovrheadset
  LIBRARY DESTINATION ${YARP_DYNAMIC_PLUGINS_INSTALL_DIR}
  ARCHIVE DESTINATION ${YARP_STATIC_PLUGINS_INSTALL_DIR}
  YARP_INI DESTINATION ${YARP_PLUGIN_MANIFESTS_INSTALL_DIR}
)


set_property(TARGET yarp_ovrheadset PROPERTY FOLDER "Plugins/Device")
