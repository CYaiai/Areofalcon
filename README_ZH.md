# 游隼 Aerofalcon v1.7.2

> 加密 Web 远程管理终端 —— 面向授权渗透测试与红队评估的加密通信管理工具

**版本**：1.7.2 · **作者**：CYAiAi· **环境要求**：JDK 17+

## 📦 发布包内容

本版本按平台分为**两个独立发布包**。JAR 内嵌 JavaFX 原生库（Windows 为 `.dll`，
Linux 为 `.so`）

```
Aerofalcon releases/
├─ Windows/
│  ├─ Aerofalcon-Windows1.7.2.jar   含 Windows 原生库的 fat JAR
│  ├─ Aerofalcon.bat                启动器
│  ├─ install.bat                   安装器（JDK 17+ 检测）
│  └─ README.md / README_ZH.md      平台说明（EN / 中文）
├─ Linux/
│  ├─ Aerofalcon-Linux1.7.2.jar     含 Linux 原生库的 fat JAR
│  ├─ Aerofalcon.sh                 启动器
│  ├─ install.sh                    安装器（多发行版适配）
│  └─ README.md / README_ZH.md      平台说明（EN / 中文）
├─ README.md                        英文文档
├─ README_ZH.md                     中文文档（本文件）
└─ RELEASE_NOTES.md                 发布说明
```

## 🚀 快速开始

### Windows

1. 进入 `Windows/` 目录（所有文件保持同一目录）
2. 双击 **`install.bat`** —— 依次检测 `JAVA_HOME`、`PATH`、常见 JDK 目录中的 Java 17+，
   **仅在缺失时才安装 JDK**（无需管理员权限）
3. 双击 **`Aerofalcon.bat`** 启动

### Linux

```bash
cd Linux/
chmod +x install.sh Aerofalcon.sh
./install.sh     # 检测 Java 17+（已安装则跳过）+ 按发行版安装图形库
./Aerofalcon.sh  # 启动
```

`install.sh` 自动适配主流包管理器：

| 发行版                 | 包管理器      | 仅在缺失时自动安装                                           |
| ---------------------- | ------------- | ------------------------------------------------------------ |
| Debian / Ubuntu / Kali | `apt`         | openjdk-21-jdk（回退 17 / default）、libgtk-3-0(t64)、libgl1、libxrender1、libxtst6、libxi6 |
| Fedora / RHEL / CentOS | `dnf` / `yum` | java-21-openjdk-devel（回退 17）、gtk3、mesa-libGL、libXrender、libXtst、libXi |
| Arch / Manjaro         | `pacman`      | jdk21-openjdk（回退 17）、gtk3、mesa、libxrender、libxtst、libxi |
| openSUSE               | `zypper`      | java-21-openjdk-devel（回退 17）、gtk3、Mesa-libGL1、libXrender1、libXtst6、libXi6 |
| Alpine                 | `apk`         | openjdk17-jdk、gtk+3.0、mesa-gl（musl 平台，JavaFX 支持有限） |

**系统已有 Java 17+ 时不会安装 JDK；图形库齐全时不会安装任何包。**

## ✨ v1.7.2 功能特性

### 核心能力

- **14 种独立加密体系** —— XYRC4、AES-256、RC4、DES、PPSR、RCCS、BDE 等，支持组合加密与深度混淆
- **8 种报文传输模式** —— KV、JSON、XML、二进制分片、乱序帧等，对抗流量审计
- **流量拟真** —— UA / Client-Hints / Referer / Origin 全链路伪装
- **TLS 指纹** —— xytls 转发器（Chrome 指纹 + HTTP/2）
- **SOCKS5 隧道** —— 站点级隧道与多级代理
- **多系统载荷** —— Windows / Linux / macOS 命令执行与自动识别

### 进阶能力

- **内存马装载** —— Filter / Servlet / Listener / Valve / Interceptor / Thread 一键装载
- **插件系统** —— 基于 ShellProtocolService API 的动态 Java 插件扩展
- **加密配置** —— 站点保险库，支持紧急清空
- **工具箱** —— AES / DES / RC4 / Base32 / JWT 加解密、端口速查、UA 库
- **完整审计** —— 流量历史与敏感操作日志

## 🛠️ 系统要求

- **JDK 17+**（仅在缺失时自动安装）
- **内存**：最低 2GB，建议 4GB
- **磁盘**：每个平台包约 200MB
- **Linux**：GTK3 + OpenGL + X11 图形库（缺失时由 `install.sh` 自动安装）

## 📬 联系方式

- **邮箱**：lorenwu024@gmail.com
- 问题反馈、功能建议或合作交流，欢迎随时联系。

## ⭐ 如果觉得不错，请点个 Star

如果 Aerofalcon 对你有帮助，欢迎给项目点个 **Star** ⭐ ——
这是对作者最大的鼓励，也能让项目持续更新。感谢支持！

## ⚠️ 免责声明

本工具**仅供已授权的渗透测试与安全研究**使用。未经授权访问计算机系统属于违法行为。使用者必须：

1. Aerofalcon v1.7.2 仅可用于已经取得目标信息系统所有者正式、书面、有效授权的安全研究、安全防御教学、渗透评估工作。
2. 本工具内置加密通信、内存 Shell 注入、多平台载荷生成、流量伪装等能力，该类能力仅限授权测试场景使用，未经授权使用属于违反网络安全相关法律法规的行为。
3. 作者不为使用者的非法使用提供任何技术指导，不参与使用者的任何攻击行为；对于使用者的操作行为，作者无法事前知悉、无法管控，不对由此引发的一切法律后果承担责任。
4. 严禁利用本工具对任意第三方系统实施未授权扫描、入侵、远程控制、窃取数据、破坏业务、植入后门、内网横向、隐秘通信等危害行为。
5. 您一旦下载、安装、运行、调用本软件任意功能，即代表已完整阅读、理解并自愿接受本免责全部条款；如不接受，请立即删除全部相关程序文件。
6. 若用户违反法律法规，给个人、企业、机构造成损失的，全部法律责任与赔偿责任由使用者自行独立承担。

## 📝 安装说明

安装脚本只做一次性的环境检查：

1. 检测 Java 17+
2. **仅在未找到 JDK 时**下载 Temurin JDK 17（存放到用户目录）
3. Linux 下**仅在缺失时**安装 GTK3/OpenGL/X11 图形库
4. 校验 JAR 是否存在（Linux 还会校验 JAR 是否含 Linux 原生库）

之后直接使用 `Aerofalcon.bat` / `Aerofalcon.sh` 启动即可。
启动器不做任何安装；若 GPU 渲染管道失败，会自动改用软件渲染
（`-Dprism.order=sw`）重试，并输出诊断信息。

日志：Windows 为 `logs\app-out.log` / `logs\app-err.log`；Linux 为 `logs/stdout.log`。

## 🔧 构建信息

- **基础语言**：Java 17
- **UI 框架**：JavaFX 17.0.13
- **构建系统**：Maven（含 Wrapper）
- **主要依赖**：
  - OkHttp 4.12.0（HTTP 客户端）
  - Jackson 2.15.2（JSON 处理）
  - Logback 1.4.8（日志）
  - AtlantaFX 2.0.1（UI 主题）

## 📖 文档

- **英文**：`README.md`
- **中文**：`README_ZH.md`（本文件）
- **平台说明**：`Windows/README.md`、`Linux/README.md`（及对应 `*_ZH.md`）

## 🐛 故障排查

### 应用无法启动

- 查看日志（Windows：`logs\app-out.log`；Linux：`logs/stdout.log`）
- 确认 Java 版本：`java -version`（需 17+）

### Linux 报 `no suitable pipeline found`

- 运行 `./install.sh` 安装对应发行版的 GTK3/OpenGL/X11 图形库
- 启动器会自动用 `-Dprism.order=sw` 重试；也可手动运行：
  `java -Dprism.order=sw -jar Aerofalcon-Linux1.7.2.jar`
- 虚拟机无 3D 加速：开启 3D 加速，或使用软件渲染
- SSH / 无桌面环境：GUI 需要显示环境（仅冒烟测试可用 `xvfb-run -a ./Aerofalcon.sh`）

### 提示 "This JAR has no Linux JavaFX natives"

- 在 Linux 上误用了 Windows 版 JAR —— 请使用 `Linux/` 发布包

### 内存不足

- 在 java 命令行中增加 `-Xmx2G` 提升 JVM 堆内存

## 🔗 运行时目录

首次启动后自动创建：

```
config/     站点凭据与配置（加密存储）
logs/       运行与审计日志
plugins/    用户插件目录
shells/     生成的服务端脚本
```

**重要**：`config/` 内含加密的站点凭据，请妥善保管并备份。

## ⚖️ 许可与授权

本软件仅供教育与已授权的渗透测试使用。使用本软件即表示你同意：
仅对拥有所有权或已获明确授权的系统进行测试，遵守所有适用法律法规，
并对自身行为承担全部责任。

**任何滥用行为均由使用者自行承担全部责任。**

---

**版本**：1.7.2 · **发布日期**：2026-10-28 · **构建环境**：Java 17、JavaFX、Maven
