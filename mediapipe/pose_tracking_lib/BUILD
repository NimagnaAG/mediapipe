# Copyright 2020 The MediaPipe Authors.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#      http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

load("windows_dll_library.bzl", "windows_dll_library")
licenses(["notice"])

package(default_visibility = ["//mediapipe/examples:__subpackages__"])

# -------------------------------------------------------------
# Windows DLL
# -------------------------------------------------------------

# Define the shared library for windows
windows_dll_library(
    name = "pose_tracking_windows_lib",
    srcs = ["pose_tracking.cpp"],
    hdrs = ["pose_tracking.h"],
    # Define COMPILING_DLL to export symbols during the DLL compilation.
    copts = ["-DCOMPILING_DLL"],
    deps = [
        "//mediapipe/framework:calculator_framework",
        "//mediapipe/framework/formats:image_frame",
        "//mediapipe/framework/formats:image_frame_opencv",
        "//mediapipe/framework/formats:landmark_cc_proto",
        "//mediapipe/framework/formats:rect_cc_proto",
        "//mediapipe/framework/port:file_helpers",
        "//mediapipe/framework/port:parse_text_proto",
        "//mediapipe/framework/port:status",
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/flags:parse",

        "//mediapipe/graphs/pose_tracking:pose_tracking_cpu_deps",
    ]
)

# **Implicitly link to face_mesh_lib.dll**
cc_binary(
    name = "pose_tracking_cpu_windows",
	linkopts = ["/FORCE:MULTIPLE"],
    deps = [
        "//mediapipe/examples/desktop:demo_run_graph_main",
        "//mediapipe/graphs/pose_tracking:pose_tracking_cpu_deps",
		":pose_tracking_windows_lib"
    ],
)

# -------------------------------------------------------------
# MacOS Dylib
# -------------------------------------------------------------

# Define the shared library for macos
cc_library(
    name = "pose_tracking_macos_lib",
    srcs = ["pose_tracking.cpp"],
    hdrs = ["pose_tracking.h"],
    deps = [
        "//mediapipe/framework:calculator_framework",
        "//mediapipe/framework/formats:image_frame",
        "//mediapipe/framework/formats:image_frame_opencv",
        "//mediapipe/framework/formats:landmark_cc_proto",
        "//mediapipe/framework/formats:rect_cc_proto",
        "//mediapipe/framework/port:file_helpers",
        "//mediapipe/framework/port:parse_text_proto",
        "//mediapipe/framework/port:status",
        "@com_google_absl//absl/flags:flag",
        "@com_google_absl//absl/flags:parse",

        "//mediapipe/graphs/pose_tracking:pose_tracking_cpu_deps",
    ],
    alwayslink = 1
)

cc_binary(
    name = "libpose_tracking_cpu_macos.dylib",
    deps = [
        ":pose_tracking_macos_lib"
    ],
    linkopts = ['-Wl,-install_name,@rpath/libpose_tracking_cpu_macos.dylib'],
    linkshared = 1
)
