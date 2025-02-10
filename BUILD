load("@rules_bison//bison:bison.bzl", "bison_cc_library")
load("@rules_flex//flex:flex.bzl", "flex_cc_library")

cc_library(
    name = "pcap_lib",
    srcs = [
        "bpf_dump.c",
        "bpf_filter.c",
        "bpf_image.c",
        "config.h",
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
        "-DBUILDING_PCAP",
        "-DHAVE_CONFIG_H",
        "-I$(GENDIR)/libpcap",  # For config.h.
        "-Dpcap_EXPORTS",
        "-fno-sanitize=alignment",  # TODO(b/299519097)
    ],
    includes = [
        "pcap",
    ],
    textual_hdrs = glob(["**/*.h"]),
)

bison_cc_library(
    name = "grammar_lib",
    src = "grammar.y",
)

flex_cc_library(
    name = "scanner_lib",
    src = "scanner.l",
)

genrule(
    name = "config.h",
    srcs = ["config.h.in"],
    outs = ["pcap/config.h"],
    cmd = "cp $< $@",
)
