load("@rules_java//java:defs.bzl", "java_binary")

package(default_visibility = ["//visibility:public"])

java_binary(
    name = "npe-bug",
    srcs = glob([
        "**/*.java",
    ]),
    main_class = "ysfaran.npebug.NpeBugMain",
    deps = [
        "@maven//:org_springframework_spring_core",
    ],
)
