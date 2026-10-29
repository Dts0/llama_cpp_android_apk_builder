# llama.cpp 官方 Android 示例 APK 构建配置

## 内容

这是一个 **GitHub Actions 构建配置**，不是已经编译完成的 APK。它从官方 `ggml-org/llama.cpp` 获取源码，不修改官方 `examples/llama.android` 工程，默认检出 `b11960`（llama.cpp v0.8.0）并编译 **Debug APK**。当前官方示例主要使用 CPU；此配置不会自动增加 Vulkan 后端或 GPU 切换。

## 操作

1. 在 GitHub 上创建一个仓库（可以是私人仓库）。
2. 在仓库根目录创建 `.github/workflows/build-llama-android.yml`，复制本压缩包中同名文件的全部内容并提交。GitHub 网页编辑器可以直接粘贴 YAML，不需要本地安装 Android Studio。
3. 进入新仓库的 **Actions** → **Build official llama.cpp Android APK** → **Run workflow**；`llama_ref` 默认填写 `b11960`，想用上游主分支可改为 `master`。
4. 等工作流执行成功，打开该运行记录，在 **Artifacts** 中点击 `llama-android-b11960-official-debug` 下载 ZIP。
5. 解压后得到 `app-debug.apk`。把 APK 传到 Android 13（API 33）或更新的 ARM64 手机上，按 Android 系统提示进行安装。Debug APK 是测试构建，不适合直接发布到应用商店。

## 产物与注意事项

- APK 名称：`app-debug.apk`（附带 `SOURCE_REVISION.txt` 和 `SHA256SUMS.txt`）。
- 源码： https://github.com/ggml-org/llama.cpp/tree/master/examples/llama.android
- 参考官方 CI： https://github.com/ggml-org/llama.cpp/blob/master/.github/workflows/build-android.yml
- `b11960`： https://github.com/ggml-org/llama.cpp/releases/tag/b11960
- 应用最低 Android 版本可能随所选上游版本变化；当前 `master` 的 `app/build.gradle.kts` 标注 `minSdk = 33`。
- 如果 Android SDK/NDK 自动安装或编译失败，请查看该 Actions 运行日志。此工作流未在实际 GitHub Runner 上验证。
