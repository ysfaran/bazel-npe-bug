load(
    "@bazel_tools//tools/jdk:default_java_toolchain.bzl",
    "BASE_JDK9_JVM_OPTS",
    "DEFAULT_JAVACOPTS",
    "DEFAULT_TOOLCHAIN_CONFIGURATION",
    "default_java_toolchain",
)

default_java_toolchain(
    name = "repository_default_toolchain",
    configuration = DEFAULT_TOOLCHAIN_CONFIGURATION,
    java_runtime = "//:amazon_corretto_macos",
    javacopts = DEFAULT_JAVACOPTS,
    jvm_opts = BASE_JDK9_JVM_OPTS,
    source_version = "11",
)
