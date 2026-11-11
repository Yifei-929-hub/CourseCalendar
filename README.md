# 课程日历 CourseCalendar

一个基于 Android 原生开发（Java）的课程表应用，支持用户注册登录，按周一至周五查看课程，并可对每天的课程进行新增、修改、删除和撤销操作。数据使用 SQLite 本地存储。

## 功能

- **注册 / 登录**：本地 SQLite 保存账号，登录成功后进入课程表
- **按天查看课程**：点击「周一」~「周五」显示当天课程（课程名、时间、教室），按上课时间自动排序
- **编辑课程**：选中某一天后点击「编辑」进入编辑页
  - **新增**：填写课程名、时间、教室后添加（每天最多 5 门）
  - **修改**：在列表中选中一节课，填写要修改的字段后点击「保存」，留空的字段保持不变
  - **删除**：选中一节课后点击「删除」
  - **撤销**：撤回上一次新增 / 修改 / 删除操作
- 首次启动会自动写入一组示例课程数据

## 技术栈

| 项目 | 说明 |
| --- | --- |
| 语言 | Java 8 |
| 构建 | Gradle 8.7（Kotlin DSL）、Android Gradle Plugin 8.6.0 |
| SDK | minSdk 24 / targetSdk 34 / compileSdk 34 |
| 存储 | SQLite（`SQLiteOpenHelper`） |
| UI | AppCompat、Material Components、ConstraintLayout、ListView |

## 项目结构

```
app/src/main/
├── java/com/example/myapplication/
│   ├── LoginActivity.java      # 登录页（启动页）
│   ├── RegisterActivity.java   # 注册页
│   ├── MainActivity.java       # 课程表主页，按天查询课程
│   ├── EditActivity.java       # 课程编辑页：新增 / 修改 / 删除 / 撤销
│   ├── Class.java              # 课程实体类（Parcelable，用于 Activity 间传递）
│   ├── MyHelper.java           # 课程数据库 class.db，含初始示例数据
│   └── UserHelper.java         # 用户数据库 user.db
├── res/layout/                 # 各页面布局
└── AndroidManifest.xml
```

## 运行方式

### 环境要求

- Android Studio（Koala 2024.1 或更新版本）
- JDK 17（Android Studio 自带的 JBR 即可）
- Android SDK Platform 34

### 使用 Android Studio

1. 克隆仓库：
   ```bash
   git clone https://github.com/<your-username>/CourseCalendar.git
   ```
2. 用 Android Studio 打开项目根目录，等待 Gradle 同步完成（会自动生成 `local.properties` 并下载依赖）
3. 连接真机或启动模拟器（Android 7.0 / API 24 及以上），点击 **Run ▶**

### 使用命令行

需先在 `local.properties` 中配置 SDK 路径（或设置 `ANDROID_HOME` 环境变量）：

```properties
sdk.dir=C\:\\Users\\<you>\\AppData\\Local\\Android\\Sdk
```

然后执行：

```bash
# Windows
gradlew.bat assembleDebug

# macOS / Linux
./gradlew assembleDebug
```

生成的 APK 位于 `app/build/outputs/apk/debug/app-debug.apk`。

## 使用说明

1. 首次打开先点击 **Register** 注册账号，然后返回登录
2. 登录后点击「周一」~「周五」查看当天课程
3. 选中某一天后点击「编辑」进入编辑页进行增删改，点击「返回」回到课程表

## 说明

本项目为课程作业，账号密码以明文形式保存在本地 SQLite 中，仅用于学习演示，请勿用于实际场景。
