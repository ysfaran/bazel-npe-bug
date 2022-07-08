# Bazel 5.2.0 NullPointerException Bug

Bazel is unable to compile code that should be fixed with JDK version 11.0.4.
More details about this JDK bug can be found here: https://stackoverflow.com/a/54776592/6489012

The example used in this repo is the same as seen in the StackOverflow link.

Run following command to reproduce:

```sh
bazelisk build //java/src/ysfaran/npebug:npe-bug
```

<details>
<summary>Error Log</summary>

```sh
INFO: Analyzed target //java/src/ysfaran/npebug:npe-bug (0 packages loaded, 0 targets configured).
INFO: Found 1 target...
ERROR: /Users/yusufaran/Projects/tmp/bazel-npe-bug/java/src/ysfaran/npebug/BUILD:5:12: Building java/src/ysfaran/npebug/npe-bug.jar (1 source file) failed: (Exit 1): java failed: error executing command external/remotejdk11_macos/bin/java -XX:-CompactStrings '--add-exports=jdk.compiler/com.sun.tools.javac.api=ALL-UNNAMED' '--add-exports=jdk.compiler/com.sun.tools.javac.main=ALL-UNNAMED' ... (remaining 17 arguments skipped)
compiler message file broken: key=compiler.misc.msg.bug arguments=11.0.12, {1}, {2}, {3}, {4}, {5}, {6}, {7}
java.lang.NullPointerException
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.visitApply(Flow.java:1235)
        at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCMethodInvocation.accept(JCTree.java:1634)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:49)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$BaseAnalyzer.scan(Flow.java:398)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.visitExec(TreeScanner.java:213)
        at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCExpressionStatement.accept(JCTree.java:1452)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:49)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$BaseAnalyzer.scan(Flow.java:398)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:57)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.visitBlock(Flow.java:997)
        at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCBlock.accept(JCTree.java:1020)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:49)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$BaseAnalyzer.scan(Flow.java:398)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.visitMethodDef(Flow.java:964)
        at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCMethodDecl.accept(JCTree.java:866)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:49)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$BaseAnalyzer.scan(Flow.java:398)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.visitClassDef(Flow.java:927)
        at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCClassDecl.accept(JCTree.java:774)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:49)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$BaseAnalyzer.scan(Flow.java:398)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.visitClassDef(Flow.java:872)
        at jdk.compiler/com.sun.tools.javac.tree.JCTree$JCClassDecl.accept(JCTree.java:774)
        at jdk.compiler/com.sun.tools.javac.tree.TreeScanner.scan(TreeScanner.java:49)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$BaseAnalyzer.scan(Flow.java:398)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.analyzeTree(Flow.java:1327)
        at jdk.compiler/com.sun.tools.javac.comp.Flow$FlowAnalyzer.analyzeTree(Flow.java:1317)
        at jdk.compiler/com.sun.tools.javac.comp.Flow.analyzeTree(Flow.java:218)
        at jdk.compiler/com.sun.tools.javac.main.JavaCompiler.flow(JavaCompiler.java:1401)
        at com.google.devtools.build.buildjar.javac.BlazeJavaCompiler.flow(BlazeJavaCompiler.java:102)
        at jdk.compiler/com.sun.tools.javac.main.JavaCompiler.flow(JavaCompiler.java:1365)
        at jdk.compiler/com.sun.tools.javac.main.JavaCompiler.compile(JavaCompiler.java:960)
        at jdk.compiler/com.sun.tools.javac.api.JavacTaskImpl.lambda$doCall$0(JavacTaskImpl.java:104)
        at jdk.compiler/com.sun.tools.javac.api.JavacTaskImpl.handleExceptions(JavacTaskImpl.java:147)
        at jdk.compiler/com.sun.tools.javac.api.JavacTaskImpl.doCall(JavacTaskImpl.java:100)
        at com.google.devtools.build.buildjar.javac.BlazeJavacMain.compile(BlazeJavacMain.java:137)
        at com.google.devtools.build.buildjar.ReducedClasspathJavaLibraryBuilder.fallback(ReducedClasspathJavaLibraryBuilder.java:105)
        at com.google.devtools.build.buildjar.ReducedClasspathJavaLibraryBuilder.compileSources(ReducedClasspathJavaLibraryBuilder.java:67)
        at com.google.devtools.build.buildjar.SimpleJavaLibraryBuilder.compileJavaLibrary(SimpleJavaLibraryBuilder.java:110)
        at com.google.devtools.build.buildjar.SimpleJavaLibraryBuilder.run(SimpleJavaLibraryBuilder.java:118)
        at com.google.devtools.build.buildjar.BazelJavaBuilder.build(BazelJavaBuilder.java:105)
        at com.google.devtools.build.buildjar.BazelJavaBuilder.parseAndBuild(BazelJavaBuilder.java:85)
        at com.google.devtools.build.lib.worker.WorkRequestHandler$WorkRequestHandlerBuilder.lambda$new$0(WorkRequestHandler.java:264)
        at com.google.devtools.build.lib.worker.WorkRequestHandler$WorkRequestCallback.apply(WorkRequestHandler.java:230)
        at com.google.devtools.build.lib.worker.WorkRequestHandler.respondToRequest(WorkRequestHandler.java:424)
        at com.google.devtools.build.lib.worker.WorkRequestHandler.lambda$startResponseThread$1(WorkRequestHandler.java:381)
        at java.base/java.lang.Thread.run(Thread.java:829)
Target //java/src/ysfaran/npebug:npe-bug failed to build
Use --verbose_failures to see the command lines of failed build steps.
INFO: Elapsed time: 0.242s, Critical Path: 0.08s
INFO: 2 processes: 2 internal.
FAILED: Build did NOT complete successfully
```
</details>

<details>
<summary>Bazel Info</summary>

```sh
bazel-bin: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/execroot/npe-bug/bazel-out/darwin-fastbuild/bin
bazel-genfiles: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/execroot/npe-bug/bazel-out/darwin-fastbuild/bin
bazel-testlogs: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/execroot/npe-bug/bazel-out/darwin-fastbuild/testlogs
character-encoding: file.encoding = ISO-8859-1, defaultCharset = ISO-8859-1
command_log: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/command.log
committed-heap-size: 101MB
execution_root: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/execroot/npe-bug
gc-count: 41
gc-time: 690ms
install_base: /var/tmp/_bazel_yusufaran/install/612c94294bf5bb5d743864f93801f7fe
java-home: /private/var/tmp/_bazel_yusufaran/install/612c94294bf5bb5d743864f93801f7fe/embedded_tools/jdk
java-runtime: OpenJDK Runtime Environment (build 11.0.6+10-LTS) by Azul Systems, Inc.
java-vm: OpenJDK 64-Bit Server VM (build 11.0.6+10-LTS, mixed mode) by Azul Systems, Inc.
max-heap-size: 4294MB
output_base: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d
output_path: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/execroot/npe-bug/bazel-out
package_path: %workspace%
release: release 5.2.0
repository_cache: /var/tmp/_bazel_yusufaran/cache/repos/v1
server_log: /private/var/tmp/_bazel_yusufaran/6cb4a6b95e5e1b85b19a519aeefb8e4d/java.log.yusufs-macbook-pro.yusufaran.log.java.20220708-091635.99326
server_pid: 99326
used-heap-size: 54MB
workspace: /Users/yusufaran/Projects/tmp/bazel-npe-bug
```

</details>
