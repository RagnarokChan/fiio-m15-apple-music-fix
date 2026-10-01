# Apple Music 4.9.7.2 登录补丁使用教程

适用：Windows 10/11、FiiO M15 固件 1.0.4 / Android 7、Apple Music 4.9.7.2（1472），arm64 + xhdpi 三分包。

本包只含差分补丁、运行脚本和 ADB，不含原版或完整修改 APK。用户自行取得对应原版，Windows 本地生成之前实机验收通过的安装文件。不需要安装 Python、Java 或签名工具。

## 1. 先安装系统修复

按仓库 README 将系统 kit 内 install、restore 两个 ZIP 复制到 SD 卡，在原厂 Recovery 安装 install，再重启正常系统。已安装 V1 系统修复的用户无需重复刷写：V2 的系统包与 V1 完全相同。

## 2. 准备对应原版

可参考 [Apple Music 4.9.7.2 原版下载页面](https://apkpure.net/apple-music-app/com.apple.android.music/download/4.9.7.2)。本项目不托管原版，也不保证第三方下载页面以后仍提供相同分包。必须是 **arm64 + xhdpi** 的以下三分包；其它版本、DPI 或签名即使名称相同，也会被拒绝。

| 原版文件 | SHA-256 |
| --- | --- |
| com.apple.android.music.apk | c0e439c6df9028432ef9b83a7e80d2c1f11616e7a3bf052d08b82103186fb157 |
| config.xhdpi.apk | b115b508f910e68a9a26bf13f9870f4703b4f361ed06c9ee7df0808b27cc2cfa |
| config.arm64_v8a.apk | 96053ae0d9564373200497df8963491498553548bef527e29a81a607d3216a61 |

## 3. 本地生成

1. 下载并完整解压 `AppleMusic-4.9.7.2-M15-login-patch-V2-Windows.zip`，不要在压缩包里运行。
2. 将含三个原版分包的 `.xapk` / `.apkm` / `.zip` 文件，或原版分包文件夹，拖到 `Generate login repair.cmd` 上。也可将三个文件放进 `original` 文件夹，再双击此 CMD。
3. 看到 `LOGIN_PATCH_PASS`，说明 `apks` 文件夹内三个结果的校验值已全部与验收版一致。生成步骤不连接设备、不安装 APP，也不覆盖原版输入。

如果提示 Missing exact original，先检查版本、架构、DPI 和上表校验值；不要修改 manifest 或关闭校验。Windows 包只适用于电脑，不能在手机内直接运行。

## 4. 安装到 M15

1. 正常开机，开启并授权 USB 调试，只连接一台 M15。
2. 双击 `Install generated APKs.cmd`。工具先核对设备、系统修复文件和三个生成文件，再安装并读回验证。
3. 看到 `INSTALL_PASS` 后打开 Apple Music，由用户自行登录并播放。

**原版 Apple 签名与补丁结果的项目测试签名不同。** 从官方版切换时通常必须手动卸载旧版；卸载会清除账号、设置和已下载内容，请先确认。工具不会自动卸载、清数据或替用户登录。同项目签名的旧修复版可尝试覆盖。若显示 `ALREADY_INSTALLED_VERIFIED`，已有完全相同版本，无需再装。

安装工具会拒绝未安装对应系统修复的 M15、其它固件和其它机型。失败时先按错误提示处理，不要反复刷系统或执行恢复出厂设置。

## 回退与边界

APP 回退：自行卸载项目签名版，重新安装合法取得的官方原版；不能恢复卸载时已经丢失的数据。系统回退：在 Recovery 使用对应 restore ZIP，系统还原与 APP 回退是两件事。

只修登录初始化，播放器与 Root 检测代码保持原版；重新签名不是 Apple 官方签名，也不保证官方更新可覆盖安装。保留原始输入，以便回退。补丁不提供账号、订阅、音乐或付费服务访问权。

本轮差分工具已验证原版文件夹与归档输入、全部输出字节一致、错误输入拒绝。本轮没有再次安装设备；生成结果就是此前已在 M15 完成登录和听音验收的同一组文件。见 [版权与使用声明](../NOTICES.md)。
