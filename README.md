# AI Browser

A simple yet powerful Android web browser application built with Java and Android SDK.

## Features

- Basic browsing functionality (back, forward, refresh)
- URL navigation
- Home button to return to default page
- Modern UI with Material Design components
- WebView-based browsing experience

## Technical Details

- Minimum SDK: 24 (Android 7.0)
- Target SDK: 34 (Android 14)
- Built with Android Gradle Plugin 8.1.4
- Uses AndroidX libraries
- WebView component for web rendering

## Quick Start

由于本地环境限制，推荐使用GitHub Actions进行云端构建：

1. 将项目推送至GitHub仓库
2. GitHub Actions将自动构建项目并生成APK文件
3. 在Actions的Artifacts中下载生成的APK

详细部署指南请参见 [DEPLOYMENT_GUIDE.md](DEPLOYMENT_GUIDE.md)

## Project Structure

- `MainActivity.java` - Main activity with browser functionality
- `activity_main.xml` - Layout with navigation controls and WebView
- `AndroidManifest.xml` - Application configuration and permissions
- `res/values/` - String, color and style resources

## Permissions

- `INTERNET` - Required for web browsing
- `ACCESS_NETWORK_STATE` - To check network connectivity

## GitHub Actions Build

项目包含完整的GitHub Actions配置，可自动构建debug和release版本的APK：

```yaml
name: Android Build CI

on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v4
    - name: Set up JDK 17
      uses: actions/setup-java@v4
      with:
        java-version: '17'
        distribution: 'temurin'
        cache: gradle

    - name: Grant execute permission for gradlew
      run: chmod +x gradlew
      
    - name: Set up Android SDK
      uses: android-actions/setup-android@v3
      with:
        packages: 'build-tools;34.0.0, platforms;android-34, cmdline-tools;latest'

    - name: Accept SDK Licenses
      run: yes | sdkmanager --licenses

    - name: Build with Gradle
      run: ./gradlew build

    - name: Build Debug APK
      run: ./gradlew assembleDebug

    - name: Upload APK
      uses: actions/upload-artifact@v4
      with:
        name: app-debug-apk
        path: app/build/outputs/apk/debug/app-debug.apk

    - name: Build Release APK
      run: ./gradlew assembleRelease
      env:
        SIGNING_KEY: ${{ secrets.SIGNING_KEY }}
        SIGNING_PASSWORD: ${{ secrets.SIGNING_PASSWORD }}
        KEYSTORE_PASSWORD: ${{ secrets.KEYSTORE_PASSWORD }}
        KEY_ALIAS: ${{ secrets.KEY_ALIAS }}

    - name: Upload Release APK
      uses: actions/upload-artifact@v4
      with:
        name: app-release-apk
        path: app/build/outputs/apk/release/app-release.apk
```