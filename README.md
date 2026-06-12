# Study with Anki / DStudy

一款基于 **Qt + C++ + SQLite** 开发的桌面学习计划软件，集成了任务管理、日历筛选、AI 学习计划分析和 Anki 风格记忆卡片复习功能。

本项目主要面向个人学习场景，适合用于课程复习、考试备考、每日任务安排、知识点卡片整理和间隔重复记忆训练。

---

## 一、软件简介

**Study with Anki** 是一个将“学习计划管理”和“记忆卡片复习”结合在一起的桌面软件。

软件主要包含两个核心部分：

1. **学习任务管理**

   * 添加每日学习任务
   * 设置任务日期、类型、优先级、预计耗时
   * 标记任务完成或未完成
   * 按日期查看当天任务
   * 查看任务完成进度

2. **Anki 风格卡片复习**

   * 创建卡片分组和牌组
   * 添加正反面记忆卡片
   * 按到期时间进行复习
   * 根据复习情况选择“忘了 / 模糊 / 记住了 / 很熟”
   * 根据评分自动调整下次复习时间
   * 支持导入 Anki 卡片数据

此外，软件还提供了 **AI 计划助手** 功能，可以调用 DeepSeek API，根据当前任务列表给出学习计划分析和调整建议。

---

## 二、主要功能

### 1. 任务管理

软件支持创建和管理学习任务，适合安排日常学习计划。

支持的功能包括：

* 添加任务
* 修改任务
* 删除任务
* 标记完成 / 未完成
* 按日期筛选任务
* 查看任务详情
* 显示任务完成进度
* 按优先级和日期管理任务

任务信息通常包括：

* 任务标题
* 任务类型
* 日期
* 总课时
* 完成课时
* 优先级
* 完成状态
* 任务描述

---

### 2. 日历筛选

主界面左侧提供日历组件，可以按日期查看对应任务。

使用方式：

1. 在左侧日历中点击某一天
2. 右侧任务列表会显示当天任务
3. 点击任务后，下方会显示任务详情
4. 可以对任务进行修改、删除或标记完成

---

### 3. AI 计划助手

软件内置 AI 计划分析区域，可以输入 DeepSeek API Key，让 AI 根据当前任务列表生成学习安排建议。

使用方式：

1. 在主界面右侧找到“AI 计划助手”
2. 输入 DeepSeek API Key
3. 点击“AI 分析计划”
4. 等待 AI 返回分析结果
5. 根据建议自行调整学习任务

注意：

* AI 只提供参考建议，不会自动修改任务
* API Key 仅用于本次运行
* 请自行保管好自己的 API Key

---

### 4. Anki 牌库

软件提供类似 Anki 的卡片复习功能。

支持：

* 新建分组
* 删除分组
* 新建牌组
* 删除牌组
* 添加卡片
* 查看卡片
* 开始复习
* 导入 Anki 卡片
* 根据复习结果调整下次复习时间

卡片复习采用简化的间隔重复逻辑：

* “忘了”：较短时间后重新复习
* “模糊”：保持或缩短复习间隔
* “记住了”：延长复习间隔
* “很熟”：进一步延长复习间隔

---

## 三、运行环境

### Windows 用户

推荐环境：

* Windows 10 / Windows 11
* 64 位系统

如果你只是使用软件，不需要安装 Qt、CMake 或编译环境，直接下载发行版安装包即可。

安装包名称示例：

```text
DStudy-1.0-win64.exe
```

---

### 开发环境

如果需要从源码编译，推荐环境如下：

* Qt 6.x
* Qt Widgets
* Qt SQL
* Qt Network
* CMake
* Ninja
* MinGW 64-bit
* SQLite
* ZLIB
* NSIS

本项目使用 CMake 管理构建流程。

---

## 四、安装教程

### 方法一：使用 Windows 安装包

1. 下载 `DStudy-1.0-win64.exe`
2. 双击安装包
3. 按照安装向导完成安装
4. 在开始菜单中搜索 `DStudy`
5. 打开软件即可使用

安装完成后，软件会自动创建快捷方式。

---

### 方法二：从源码编译

#### 1. 克隆仓库

```bash
git clone https://github.com/dmouD/Study_with_anki.git
cd Study_with_anki
```

#### 2. 准备依赖

需要安装：

* Qt 6
* CMake
* Ninja
* MinGW 64-bit
* vcpkg
* zlib

使用 vcpkg 安装 zlib：

```bat
cd /d C:\vcpkg
.\vcpkg.exe install zlib:x64-mingw-dynamic
```

#### 3. 配置 CMake

Windows + Qt MinGW 示例：

```bat
set PATH=D:\Qt\Tools\mingw1310_64\bin;D:\Qt\Tools\CMake_64\bin;D:\Qt\Tools\Ninja;%PATH%

cmake -S . -B build-win -G Ninja ^
  -DCMAKE_BUILD_TYPE=Release ^
  -DCMAKE_PREFIX_PATH=D:/Qt/6.11.1/mingw_64 ^
  -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake ^
  -DVCPKG_TARGET_TRIPLET=x64-mingw-dynamic
```

#### 4. 编译项目

```bat
cmake --build build-win
```

编译成功后会生成：

```text
build-win/DStudy.exe
```

#### 5. 部署 Qt 依赖

```bat
D:\Qt\6.11.1\mingw_64\bin\windeployqt.exe --release build-win\DStudy.exe
```

如果运行时提示缺少 `libz.dll`，需要将 vcpkg 中的 `libz.dll` 复制到程序目录：

```bat
copy C:\vcpkg\installed\x64-mingw-dynamic\bin\libz.dll build-win\
```

---

## 五、使用教程

### 1. 添加学习任务

1. 打开软件
2. 点击底部的“添加任务”
3. 输入任务标题、任务类型、日期、优先级等信息
4. 点击确认
5. 任务会显示在任务列表中

建议按照学习内容建立任务，例如：

* 高等数学复习
* 英语四级阅读训练
* 数据结构刷题
* Qt 项目开发
* 物理实验预习

---

### 2. 查看某天任务

1. 在左侧日历中选择日期
2. 右侧任务列表会显示该日期下的任务
3. 点击某个任务
4. 下方“任务详情”区域会显示任务详细内容

---

### 3. 修改任务

1. 在任务列表中选择一个任务
2. 点击“修改任务”
3. 修改任务内容
4. 保存修改

---

### 4. 删除任务

1. 在任务列表中选择一个任务
2. 点击“删除任务”
3. 确认删除

删除后任务将从数据库中移除，请谨慎操作。

---

### 5. 标记任务完成 / 未完成

1. 选择一个任务
2. 点击“标记完成/未完成”
3. 软件会切换任务状态
4. 完成进度会同步更新

---

### 6. 使用 AI 计划助手

1. 在主界面右侧找到“AI 计划助手”
2. 输入 DeepSeek API Key
3. 点击“AI 分析计划”
4. 等待 AI 返回结果
5. 根据 AI 建议手动调整自己的任务安排

AI 适合用于：

* 分析任务是否过多
* 判断学习计划是否合理
* 给出复习顺序建议
* 给出时间安排建议

---

## 六、Anki 复习功能使用教程

### 1. 进入 Anki 复习页面

在主界面右下角点击：

```text
Anki复习
```

进入 Anki 牌库页面。

---

### 2. 新建分组

分组用于管理不同类别的学习内容。

例如：

* 默认分组
* 英语
* 高等数学
* 数据结构
* Qt 开发
* 物理

操作步骤：

1. 点击“新建牌组”或分组相关按钮
2. 输入分组名称
3. 创建成功后左侧会显示新的分组

---

### 3. 新建牌组

牌组用于保存一组相关卡片。

例如：

英语分组下可以建立：

* 四级词汇
* 阅读长难句
* 翻译句型

数据结构分组下可以建立：

* 树
* 图
* 排序
* 查找

---

### 4. 添加卡片

1. 进入 Anki 牌库页面
2. 选择目标分组和牌组
3. 点击“添加卡片”
4. 输入卡片正面和背面
5. 保存卡片

示例：

正面：

```text
什么是二叉树？
```

背面：

```text
二叉树是每个节点最多有两个孩子的树结构，两个孩子通常称为左孩子和右孩子。
```

---

### 5. 开始复习

1. 选择一个牌组
2. 点击“开始复习”
3. 软件显示卡片正面
4. 点击“显示答案”
5. 根据掌握情况选择评分

评分含义：

* 忘了：完全不会，需要尽快重新复习
* 模糊：有印象但不熟，需要较短时间后复习
* 记住了：基本掌握，可以延长复习间隔
* 很熟：非常熟练，可以更久之后再复习

软件会根据评分自动更新卡片的下次复习时间。

---

### 6. 导入 Anki 卡片

软件支持导入 Anki 卡片数据，方便复用已有 Anki 学习资料。

使用方式：

1. 进入 Anki 牌库页面
2. 点击“导入 Anki 卡片”
3. 选择 Anki 导出的 `.apkg` 文件
4. 等待导入完成
5. 导入成功后，可以在对应牌组中查看和复习卡片

注意：

* `.apkg` 文件本质上是 Anki 的卡片包
* 如果卡片中包含图片、音频等媒体文件，需要确保导入过程完整
* 如果运行时提示缺少 `libz.dll`，请确认安装包或程序目录中包含该文件

---

## 七、打包说明

本项目支持使用 CPack + NSIS 生成 Windows 安装包。

### 1. 生成安装包

进入构建目录：

```bat
cd /d F:\test_qt\StudyPlanner\build-win
```

执行：

```bat
cpack -G NSIS
```

成功后会生成：

```text
DStudy-1.0-win64.exe
```

### 2. 卸载软件

安装包会自动生成卸载程序。

可以通过以下方式卸载：

方式一：

```text
Windows 设置
→ 应用
→ 已安装的应用
→ DStudy
→ 卸载
```

方式二：

```text
安装目录
→ Uninstall.exe
```

---

## 八、常见问题

### 1. 运行时提示缺少 libz.dll

原因：

项目使用了 ZLIB 动态库，但打包时没有把 `libz.dll` 一起放入安装目录。

解决方法：

将文件：

```text
C:\vcpkg\installed\x64-mingw-dynamic\bin\libz.dll
```

复制到程序目录，和 `DStudy.exe` 放在一起。

如果是开发者，需要在 `CMakeLists.txt` 中加入：

```cmake
if(WIN32)
    install(FILES "C:/vcpkg/installed/x64-mingw-dynamic/bin/libz.dll"
        DESTINATION bin
    )
endif()
```

然后重新打包。

---

### 2. cpack 提示找不到 NSIS

错误信息：

```text
Cannot find NSIS compiler makensis
```

解决方法：

1. 安装 NSIS
2. 将 NSIS 路径加入 PATH

示例：

```bat
set PATH=C:\Program Files (x86)\NSIS;%PATH%
```

然后重新执行：

```bat
cpack -G NSIS
```

---

### 3. cpack 不是内部或外部命令

原因：

CMake 的 bin 目录没有加入 PATH。

解决方法：

```bat
set PATH=D:\Qt\Tools\CMake_64\bin;%PATH%
```

然后检查：

```bat
where cpack
```

---

### 4. CMake 找不到 ZLIB

错误信息类似：

```text
Could NOT find ZLIB
```

解决方法：

使用 vcpkg 安装 zlib：

```bat
cd /d C:\vcpkg
.\vcpkg.exe install zlib:x64-mingw-dynamic
```

重新配置 CMake：

```bat
cmake -S . -B build-win -G Ninja ^
  -DCMAKE_BUILD_TYPE=Release ^
  -DCMAKE_PREFIX_PATH=D:/Qt/6.11.1/mingw_64 ^
  -DCMAKE_TOOLCHAIN_FILE=C:/vcpkg/scripts/buildsystems/vcpkg.cmake ^
  -DVCPKG_TARGET_TRIPLET=x64-mingw-dynamic
```

---

### 5. 安装后界面和开发环境不完全一样

原因：

Windows、Linux、Qt Creator 运行环境的默认控件样式可能不同。打包后的软件会使用 Windows 当前系统主题。

如果希望界面保持统一，可以在程序中设置统一的 Qt Fusion 样式和浅色调色板。

---

## 九、项目结构说明

项目主要文件说明：

```text
Study_with_anki/
├── main.cpp                  程序入口
├── mainwindow.h/.cpp         主窗口和任务管理界面
├── task.h/.cpp               学习任务数据结构
├── taskdialog.h/.cpp         添加/修改任务对话框
├── flashcard.h               记忆卡片数据结构
├── reviewwidget.h/.cpp       Anki 牌库和复习界面
├── carddialog.h/.cpp         添加/编辑卡片对话框
├── databasemanager.h/.cpp    SQLite 数据库管理
├── deepseekclient.h/.cpp     DeepSeek API 调用
├── ankipackageimporter.h/.cpp Anki 卡片导入逻辑
├── resources/                图标和资源文件
├── packaging/                打包相关文件
├── CMakeLists.txt            CMake 构建配置
└── README.md                 项目说明文档
```

---

## 十、技术栈

本项目主要使用：

* C++
* Qt Widgets
* Qt SQL
* Qt Network
* SQLite
* CMake
* Ninja
* ZLIB
* NSIS
* DeepSeek API

---

## 十一、适用场景

本软件适合：

* 学生制定学习计划
* 考试复习
* 课程任务管理
* 编程学习记录
* 英语单词和知识点记忆
* 使用 Anki 思路进行间隔重复复习
* 个人 Qt/C++ 桌面软件开发学习

---

## 十二、免责声明

本项目为个人学习与技术交流项目，主要用于 Qt/C++、数据库、计划软件以及 AI 接口调用等相关技术的学习和实践。

本项目中涉及的 AI 分析功能仅用于辅助学习计划整理与参考，不保证生成内容的准确性、完整性和适用性。用户应根据自身实际情况进行判断和调整，因使用本项目或参考 AI 生成内容所产生的任何后果，由使用者自行承担。

本项目不会在代码中主动保存用户的 API Key。用户在使用第三方 AI 接口时，应自行妥善保管相关密钥，并遵守对应平台的服务条款、隐私政策和使用规范。

本项目仅供学习、研究和非商业用途。如需用于实际生产环境或商业场景，请自行进行充分测试、安全审查和合法合规评估。

项目作者不对因使用、修改、分发本项目代码而产生的任何直接或间接损失承担责任。

