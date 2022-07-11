workspace(name = "npe-bug")

load("@bazel_tools//tools/build_defs/repo:http.bzl", "http_archive")

http_archive(
    name = "rules_jvm_external",
    sha256 = "f36441aa876c4f6427bfb2d1f2d723b48e9d930b62662bf723ddfb8fc80f0140",
    strip_prefix = "rules_jvm_external-4.1",
    url = "https://github.com/bazelbuild/rules_jvm_external/archive/4.1.zip",
)

load("@bazel_tools//tools/jdk:remote_java_repository.bzl", "remote_java_repository")

remote_java_repository(
    name = "amazon_corretto_macos",
    exec_compatible_with = [
        "@platforms//os:macos",
    ],
    prefix = "amazon_corretto",
    sha256 = "36afb7f091cd9b986a50c3f878f167c59eae615f004b2cb1c5c394f9f2fc215a",
    strip_prefix = "amazon-corretto-11.jdk/Contents/Home",
    urls = [
        "https://corretto.aws/downloads/latest/amazon-corretto-11-x64-macos-jdk.tar.gz",
    ],
    version = "11",
)

register_toolchains(
    "//:repository_default_toolchain",
)

load("@rules_jvm_external//:defs.bzl", "maven_install")
load("@rules_jvm_external//:specs.bzl", "maven")

maven_install(
    name = "maven",
    artifacts = [
        maven.artifact("org.springframework", "spring-core", "5.3.15"),
    ],
    repositories = [
        "https://repo1.maven.org/maven2",
    ],
    use_unsafe_shared_cache = True,
)
