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
