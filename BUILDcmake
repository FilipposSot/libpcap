load("@rules_foreign_cc//foreign_cc:defs.bzl", "cmake")
load("@rules_license//rules:license.bzl", "license")

package(
    default_applicable_licenses = [":license"],
    default_visibility = ["//visibility:public"],
)

license(
    name = "license",
    package_name = "libpcap",
)

filegroup(
    name = "all_srcs",
    srcs = glob(["**"]),
)

cmake(
    name = "libpcap",
    build_args = [
        "-j4",
    ],
    env = {
        "CMAKE_BUILD_TYPE": "Release",
        "CMAKE_BUILD_PARALLEL_LEVEL": "4",
    },
    cache_entries = {
           "BUILD_SHARED_LIBS": "OFF",},
    includes = [
      ".",
      "pcap",
    ],
    lib_source = ":all_srcs",
    out_static_libs = ["libpcap.a"],
)