load("@rules_bison//bison:bison.bzl", "bison_cc_library")
load("@rules_flex//flex:flex.bzl", "flex_cc_library")

_workspace_root = package_relative_label("invalid").workspace_root

# genrule(
#     name = "config_h",
#     srcs = ["cmakeconfig.h.in"],
#     outs = [
#         "config.h",
#     ],
#     cmd = "awk '{ gsub(/^#cmakedefine/, \"//cmakedefine\"); print; }' $(<) > $(@)",
# )

genrule(
    name = 'config_h',
    srcs = ['config.h.in'],
    outs = ['config.h'],
    cmd = 'cp $< $@',
)


cc_library(
    name = "pcap_lib",
    srcs = [
        "bpf_dump.c",
        "bpf_filter.c",
        "bpf_image.c",
        "etherent.c",
        "fad-getad.c",
        "fmtutils.c",
        "gencode.c",
        "missing/strlcat.c",
        "missing/strlcpy.c",
        "nametoaddr.c",
        "optimize.c",
        "pcap.c",
        "pcap-common.c",
        "pcap-linux.c",
        "pcap-netfilter-linux.c",
        "pcap-usb-linux.c",
        "savefile.c",
        "sf-pcap.c",
        "sf-pcapng.c",
    ],
    copts = [
        "-w",
        "-I" +_workspace_root + "pcap",
        "-DBUILDING_PCAP",
        "-DHAVE_CONFIG_H",
        "-Dpcap_EXPORTS",
        "-fno-sanitize=alignment",  # TODO(b/299519097)
    ],
    includes = [
        "pcap",
    ],
    hdrs = glob(["**/*.h"]),
    # data = [":grammar_lib"],
    
)

# bison_cc_library(
#     name = "grammar_lib",
#     src = "grammar.y",
# )

flex_cc_library(
    name = "scanner_lib",
    src = "scanner.l",
    deps = [":config_h"],
)