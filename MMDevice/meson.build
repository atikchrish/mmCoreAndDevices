# This Meson script is experimental and potentially incomplete. It is not part
# of the supported build system for Micro-Manager or mmCoreAndDevices.

project(
    'MMDevice',
    'cpp',
    meson_version: '>=1.1.0', # May relax
    default_options: [
        'cpp_std=c++14',
        'warning_level=3',
    ],
)

# We intentionally do NOT define NOMINMAX on Windows. MMDevice should compile
# correctly with or without Windows.h's min()/max() macros.

mmdevice_sources = files(
    'Debayer.cpp',
    'DeviceUtils.cpp',
    'ImgBuffer.cpp',
    'MMDevice.cpp',
    'ModuleInterface.cpp',
    'Property.cpp',
)

mmdevice_include_dir = include_directories('.')

mmdevice_public_headers = files(
    'Debayer.h',
    'DeviceBase.h',
    'DeviceThreads.h',
    'DeviceUtils.h',
    'ImageMetadata.h',
    'ImgBuffer.h',
    'MMDevice.h',
    'MMDeviceConstants.h',
    'ModuleInterface.h',
    'Property.h',
)
# TODO Support installing public headers

mmdevice_lib = static_library(
    'MMDevice',
    sources: mmdevice_sources,
    include_directories: mmdevice_include_dir,
    cpp_args: [
        '-DMODULE_EXPORTS',
        '-D_CRT_SECURE_NO_WARNINGS', # TODO Eliminate the need
    ],
    # MMDevice does not depend on any external library. This is a big advantage
    # in simplifing its usage (given hundreds of device adapters depending on
    # MMDevice), so think twice before adding dependencies.
)

subdir('unittest')

mmdevice = declare_dependency(
    include_directories: mmdevice_include_dir,
    link_with: mmdevice_lib,
)
