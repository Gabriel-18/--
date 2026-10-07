# 校园网一键登录 Android

这是根据当前校园网 EPortal 页面流程制作的 Android 客户端示例。

功能：
- 默认账号预填为 `202604133`
- 默认选择“教职工移动终端登录”
- 自动访问 HTTP 页面触发校园网 Portal
- 使用当前手机由网关生成的 queryString
- 直接调用认证页面现有的 `encryptedPassword()` / `RSAUtils` 完成密码加密
- 密码不持久化保存
- 不修改或伪造 MAC 地址

## 编译 APK

1. 用 Android Studio 打开本项目目录。
2. 等待 Gradle Sync 完成。
3. 点击 `Build > Build Bundle(s) / APK(s) > Build APK(s)`。
4. 调试 APK 通常生成在：
   `app/build/outputs/apk/debug/app-debug.apk`

## 手机使用

1. 安装 APK。
2. 连接校园 Wi-Fi。
3. 打开“校园网一键登录”。
4. 输入校园网密码。
5. 默认保持“教职工移动终端登录”。
6. 点击“一键登录”。

如果校园网已经认证，探测页可能不会跳转到 Portal，此时应用会提示“当前可能已经联网”。

## 注意

校园网认证地址使用 HTTP，因此 Manifest 中开启了 cleartext traffic。该项目只针对你提供的内网 Portal `192.168.254.71/eportal/`。

## No Android Studio: build in GitHub Actions

1. Create a new GitHub repository.
2. Upload the contents of this `CampusLoginAndroid` folder to the repository root.
3. Open the repository's **Actions** tab.
4. Choose **Build APK** and click **Run workflow**. A push to `main`/`master` will also trigger a build.
5. After the job finishes, open the completed run and download the artifact named `campus-login-debug-apk`.
6. Unzip the artifact on your phone. The APK inside is `app-debug.apk`.

The workflow builds on GitHub's runner, so Android Studio is not required on your computer or phone.
