# Android Automotive 车辆信息读取应用

> 目标是从**应用侧**理解 Car API 如何读取车辆属性，并与我之前的 VHAL 项目形成完整的数据流闭环。

---

## 总结

通过 `CarInfoManager` 和 `CarPropertyManager` 读取车速、挡位、点火状态等车辆属性，使“VHAL 系统侧”和“Car API 应用侧”产生联动。

---

## 为什么做这个项目？

我之前做过一个 AOSP VHAL 的学习项目，理解了车辆信号从 CAN Bus → VHAL → Car Service → CarPropertyManager → UI 的完整链路。
但那个项目偏系统侧，我并没有亲手写过一个**真实运行的车载 Android 应用**。

为了补上“应用侧”的动手经验，我找到了这个 Kotlin Android Automotive 示例项目，在 AAOS 模拟器上跑通，并重点研究了：

- `CarInfoManager` 和 `CarPropertyManager` 的区别
- 应用层如何订阅车辆属性变化
- 车载应用与手机应用在权限、硬件特性声明上的差异

---

## 项目功能

这个示例应用主要用于探索 Android Car API，包含以下功能：

### 1. 显示 Android Automotive 设备信息

- 品牌（Brand）
- 制造商（Manufacturer）
- 型号（Model）
- Android SDK 版本
- Android ID

### 2. 通过 `CarInfoManager` 读取车辆信息

- 车辆制造商与型号
- 燃料容量与燃料类型
- 电动车电池容量
- 电动车充电接口类型

### 3. 通过 `CarPropertyManager` 观察车辆属性

- 车速（Vehicle Speed）
- 挡位（Gear Selection）
- 点火状态（Ignition State）

### 4. 其他功能

- 在获得位置权限时，显示最后一次已知的 GPS 位置
- 列出已安装应用，并区分系统应用与用户应用
- 包含一个次级应用 Activity，用于示例 UI

---

## 技术栈与构建配置

- **语言**：Kotlin
- **构建工具**：Android Studio + Gradle
- **Kotlin 版本**：`1.4.31`
- **Android Gradle Plugin**：`4.1.2`
- **Compile SDK**：`30`
- **Target SDK**：`30`
- **Minimum SDK**：`28`

> 注意：该应用声明了 Automotive 硬件特性为必需，因此它面向 Android Automotive OS，而不是普通 Android 手机或平板。

---

## 运行环境要求

- 安装 Android Studio，并配置 Android SDK 与 Gradle
- 一台 Android Automotive OS 设备，或 AAOS 模拟器
- Android SDK Platform 30
- 设备或模拟器运行 Android API 28 或更高版本

---