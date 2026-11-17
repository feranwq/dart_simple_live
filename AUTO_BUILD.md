# 自动同步与构建

此仓库每天北京时间 10:17 检查 `xiaoyaocz/dart_simple_live` 的 `dev` 分支。发现上游有新提交时，会合并到本仓库的 `main`，然后构建手机 Android、Android TV 和 iOS 产物。也可以在 GitHub 仓库的 **Actions → Sync upstream and build apps → Run workflow** 手动触发构建。

构建产物在对应 Actions 运行页的 **Artifacts** 中下载，保留 30 天：

- `simple-live-phone-debug-apks`：手机应用的 ARMv7、ARM64、x86_64 APK。
- `simple-live-tv-debug-apks`：TV 应用的 ARMv7、ARM64、x86_64 APK。
- `simple-live-ios-unsigned-ipa`：未签名 iOS IPA。

Android APK 使用临时 runner 的 debug 签名，适合个人侧载验证；不同次构建的签名可能不同，若覆盖安装提示签名冲突，需要先卸载旧版。iOS 产物没有 Apple 开发者证书和 provisioning profile 签名，不能直接安装到 iPhone；要安装需自行签名。此仓库不会保存个人证书或私钥。

自动同步直接合并上游 `dev` 到 `main`。如上游变更与本仓库自动化文件冲突，合并会失败，需解决冲突后再运行工作流。
