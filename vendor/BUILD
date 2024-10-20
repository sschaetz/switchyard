load("@rules_cc//cc:defs.bzl", "cc_binary", "cc_library")

cc_library(
    name = "hidapi",
    srcs = select({
        "@platforms//os:linux": ["hidapi/linux/hid.c"],
        "@platforms//os:macos": ["hidapi/mac/hid.c"],
        "//conditions:default": [],
    }),
    hdrs = [
        "hidapi/hidapi/hidapi.h",
    ] + select({
        "@platforms//os:macos": ["hidapi/mac/hidapi_darwin.h"],
        "//conditions:default": [],
    }),
    includes = [
        "hidapi/hidapi",
    ] + select({
        "@platforms//os:macos": ["hidapi/mac"],
        "//conditions:default": [],
    }),
    strip_include_prefix = "hidapi/",
    deps = ["@libusb//:libusb"],
)

cc_binary(
    name = "uhidctl",
    srcs = [
        "uhidctl/uhidctl.c",
    ],
    deps = [
        ":hidapi"
    ],
    defines = [
        'PROGRAM_VERSION=\\"1.0.0\\"',
    ],
    linkopts = select({
        "@platforms//os:macos": ["-framework IOKit"],
        "//conditions:default": [],
    }),
)


cc_library(
    name = "ykush_lib",
    srcs = [
        "ykush/src/commandParser.cpp",
        "ykush/src/help/ykush_help.cpp",
        "ykush/src/utils/command_parser.cpp",
        "ykush/src/utils/string2val.cpp",
        "ykush/src/yk_usb_device.cpp",
        "ykush/src/ykush/ykush.cpp",
        "ykush/src/ykush2/ykush2.cpp",
        "ykush/src/ykush3/ykush3.cpp",
        "ykush/src/ykushxs/ykushxs.cpp",
        
    ] + select({
        "@platforms//os:linux": [
            "ykush/src/usbhid/usbhid.cpp",
        ],
        "//conditions:default": [],
    }),
    hdrs = [
        "ykush/src/commandParser.h",
        "ykush/src/help/ykush_help.h",
        "ykush/src/platformdefs.h",
        "ykush/src/stdafx.h",
        "ykush/src/usbhid/usbhid.h",
        "ykush/src/utils/command_parser.h",
        "ykush/src/utils/string2val.h",
        "ykush/src/yk_usb_device.h",
        "ykush/src/ykush/ykush.h",
        "ykush/src/ykush2/ykush2.h",
        "ykush/src/ykush3/ykush3.h",
        "ykush/src/ykushxs/ykushxs.h",
    ],
    includes = [
        "ykush/src",
        "ykush/src/ykush",
        "ykush/src/ykush2",
        "ykush/src/ykushxs",
        "ykush/src/ykush3",
        "ykush/src/utils",
        "ykush/src/help",
        "ykush/src/usbhid",
    ],
    linkopts = select({
        "@platforms//os:macos": ["-framework IOKit"],
        "//conditions:default": [],
    }),
    deps = select({
        "@platforms//os:linux": [
            "@libusb//:libusb",
            
        ],
        "@platforms//os:macos": [":hidapi"],
        "//conditions:default": [],
    }),
    defines = select({
        "@platforms//os:linux": [
            "_LINUX_",
            "_LIBUSB_",
            
        ],
        "//conditions:default": [],
    }),
)


cc_binary(
    name = "ykush",
    srcs = ["ykush/src/yktrl.cpp"],
    deps = [":ykush_lib"],
)
