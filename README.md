# Google服务开关 App

一个利用 Shizuku，通过创建磁贴来开关谷歌基础服务管理的开关，适用于vivo手机。

## 功能特点

- **磁贴控件**：支持在桌面添加小部件，一键开关 Google 服务
- **Shizuku 集成**：利用 Shizuku 实现系统级权限，无需 root
- **vivo 优化**：针对 vivo 手机的系统特性进行优化

## 安装步骤

### 1. 准备工作

在 vivo 手机上：

1. 安装 [Shizuku](https://github.com/topjohnwu/Shizuku) 应用
2. 启动 Shizuku 并授予系统权限
3. 在系统设置中启用 "开发者选项"

### 2. 构建 APK

```bash
# 进入项目目录
cd GoogleServiceToggleApp

# 使用 Android Studio 构建
# 或者使用命令行：
./gradlew assembleDebug

# 生成的 APK 位于：
# app/build/outputs/apk/debug/app-debug.apk
```

### 3. 安装到 vivo 手机

将生成的 apk 传输到手机并安装：

```bash
adb install app/build/outputs/apk/debug/app-debug.apk
```

## 使用说明

1. **添加磁贴**：
   - 在桌面长按空白区域
   - 选择 "小部件" 或 "添加小部件"
   - 找到 "Google服务管理" 小部件
   - 拖拽到桌面

2. **添加小部件时**：
   - 系统会弹出 Shizuku 权限请求
   - 确认授予权限

3. **使用**：
   - 点击磁贴上的开关即可切换 Google 服务状态
   - 开启后显示绿色，关闭后显示红色

## 技术原理

### Shizuku 工作原理

Shizuku 通过 Android 的 AccessibilityService 或系统服务获取 root 权限，允许非 root 用户执行部分系统命令。

### 主要功能模块

- `MainActivity.kt`：主界面，处理 Shizuku 权限请求
- `GoogleServiceWidgetProvider.kt`：磁贴提供器，处理点击事件
- `ShizukuUtil.kt`：Shizuku 工具类，封装系统命令调用
- `WidgetConfigureActivity.kt`：磁贴配置活动

### 可控的 Google 服务

- `com.google.android.gms` - Google Play Services
- `com.google.android.gsf` - Google Services Framework
- `com.google.android.gsf.login` - Google 登录服务
- `com.google.android.music` - Google 播放音乐
- `com.google.android.videos` - Google 视频

## 注意事项

⚠️ **警告**：
- 关闭 Google Play Services 可能会影响部分应用的正常运行
- 某些系统 app 可能无法被禁用
- 需要在 vivo 手机上安装 Shizuku 才能正常工作

## 许可证

本项目仅用于学习和个人使用，禁止用于任何商业或非法用途。

## 自动构建（GitHub Actions）

本项目配置了 GitHub Actions 自动构建功能：

### 如何自动构建 APK

1. ** fork 本项目到您的 GitHub 账户 **
2. ** 上传源码 **

### 手动构建步骤

#### 步骤 1：创建 GitHub 仓库

在 GitHub 上创建一个新的空仓库，例如命名为 `GoogleServiceToggleApp`

#### 步骤 2：克隆仓库到本地

```bash
git clone https://github.com/YOUR_USERNAME/GoogleServiceToggleApp.git
```

#### 步骤 3：复制项目文件

将项目中所有文件复制到克隆的仓库目录中：

```bash
cp -r /sdcard/Download/GoogleServiceToggleApp/* /path/to/GitHub/repo/
```

#### 步骤 4：提交并推送

```bash
cd GoogleServiceToggleApp
git add .
git commit -m "Initial commit"
git push origin main
```

#### 步骤 5：查看构建结果

访问仓库的 "Actions" 选项卡，等待构建完成。构建成功后，您可以在 "Artifacts" 中下载生成的 APK 文件。

### 手动构建（Android Studio）

1. 打开 Android Studio
2. File → Open → 选择项目目录
3. 等待 Gradle 同步完成
4. 运行 Build → Build Bundle(s)/APK(s) → Build APK(s)
5. 构建完成后，点击 "locate output" 找到 APK 文件