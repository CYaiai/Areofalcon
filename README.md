# Aerofalcon v1.7.2

> Modern Encrypted WebShell Remote Management Terminal — for authorized penetration testing and red team assessments

**Version**: 1.7.2 · **Author**: CYAiAi · **Requires**: JDK 17+

## 📦 Package Contents

This release ships as **two platform packages**. The JAR embeds JavaFX native
libraries (`.dll` on Windows, `.so` on Linux)

```
Aerofalcon releases/
├─ Windows/
│  ├─ Aerofalcon-Windows1.7.2.jar   Fat JAR with Windows natives
│  ├─ Aerofalcon.bat                Launcher
│  ├─ install.bat                   Installer (JDK 17+ check)
│  └─ README.md / README_ZH.md      Platform guide (EN / 中文)
├─ Linux/
│  ├─ Aerofalcon-Linux1.7.2.jar     Fat JAR with Linux natives
│  ├─ Aerofalcon.sh                 Launcher
│  ├─ install.sh                    Installer (multi-distro)
│  └─ README.md / README_ZH.md      Platform guide (EN / 中文)
├─ README.md                        English documentation (this file)
├─ README_ZH.md                     Chinese (Simplified) documentation
└─ RELEASE_NOTES.md                 Release notes
```

## 🚀 Quick Start

### Windows

1. Open the `Windows/` folder (keep all files together)
2. Double-click **`install.bat`** — finds Java 17+ in `JAVA_HOME` / `PATH` / common JDK
   folders and installs a JDK **only if missing** (no admin rights needed)
3. Double-click **`Aerofalcon.bat`** to launch

### Linux

```bash
cd Linux/
chmod +x install.sh Aerofalcon.sh
./install.sh     # Java 17+ check (skipped when present) + graphics libs per distro
./Aerofalcon.sh  # launch
```

`install.sh` is portable across package managers:

| Distro family          | Manager       | Auto-installed only when missing                             |
| ---------------------- | ------------- | ------------------------------------------------------------ |
| Debian / Ubuntu / Kali | `apt`         | openjdk-21-jdk (fallback 17 / default), libgtk-3-0(t64), libgl1, libxrender1, libxtst6, libxi6 |
| Fedora / RHEL / CentOS | `dnf` / `yum` | java-21-openjdk-devel (fallback 17), gtk3, mesa-libGL, libXrender, libXtst, libXi |
| Arch / Manjaro         | `pacman`      | jdk21-openjdk (fallback 17), gtk3, mesa, libxrender, libxtst, libxi |
| openSUSE               | `zypper`      | java-21-openjdk-devel (fallback 17), gtk3, Mesa-libGL1, libXrender1, libXtst6, libXi6 |
| Alpine                 | `apk`         | openjdk17-jdk, gtk+3.0, mesa-gl (musl — JavaFX support limited) |

**Already have Java 17+? No JDK will be installed. Graphics libs present? Nothing is installed.**

## ✨ Features in v1.7.2

### Core Capabilities

- **14 Independent Encryption Systems** — XYRC4, AES-256, RC4, DES, PPSR, RCCS, BDE, and more
- **8 Transmission Modes** — KV, JSON, XML, Binary Fragmentation, Random Frame Ordering
- **Traffic Mimicking** — Full-chain UA/Client-Hints/Referer/Origin spoofing
- **TLS Fingerprinting** — xytls forwarder with Chrome fingerprint + HTTP/2
- **SOCKS5 Tunneling** — Multi-level proxy and site-level tunnel support
- **Multi-OS Payload** — Windows/Linux/macOS command execution with auto-detection

### Advanced Features

- **In-Memory Shell Injection** — One-click Filter/Servlet/Listener/Valve/Interceptor/Thread point loading
- **Plugin System** — Dynamic Java plugin extension with ShellProtocolService API
- **Encrypted Configuration** — Site vault with panic wipe for emergency cleanup
- **Comprehensive Toolbox** — AES/DES/RC4/Base32/JWT encryption, port lookup, UA database
- **Full Audit Trail** — Traffic history and sensitive operation logging

## 🛠️ System Requirements

- **JDK 17+** (installed automatically only if missing)
- **RAM**: 2GB minimum, 4GB recommended
- **Disk**: ~200MB per platform package
- **Linux**: GTK3 + OpenGL + X11 libraries (installed by `install.sh` when missing)

## 📬 Contact

- **Email**: lorenwu024@gmail.com
- Feedback, bug reports, suggestions or collaboration — feel free to reach out.

## ⭐ Like it? Give it a Star

If you find Aerofalcon useful, please give the project a **Star** ⭐ —
it really helps and keeps development going. Thank you!

## ⚠️ Legal Disclaimer

This tool is **strictly for authorized penetration testing and security research only**.
Unauthorized access to computer systems is illegal. Users must:

1. Obtain explicit written authorization from system owners
2. Comply with all local laws and regulations
3. Use only on authorized targets
4. Accept full legal responsibility for their actions

## 📝 Installation Notes

The installer is a one-time environment check:

1. Detects Java 17+
2. Downloads Temurin JDK 17 **only when no JDK is found** (to the user home directory)
3. On Linux: installs GTK3/OpenGL/X11 libraries **only when missing**
4. Verifies the JAR is present (and on Linux, that it contains Linux natives)

After that, start the app directly with `Aerofalcon.bat` / `Aerofalcon.sh`.
The launcher never installs anything; on a GPU pipeline failure it automatically
retries with the software renderer (`-Dprism.order=sw`) and prints diagnostics.

Logs: `logs\app-out.log` / `logs\app-err.log` (Windows), `logs/stdout.log` (Linux).

## 🔧 Build Information

- **Base Language**: Java 17
- **UI Framework**: JavaFX 17.0.13
- **Build System**: Maven (with Wrapper)
- **Key Dependencies**:
  - OkHttp 4.12.0 (HTTP client)
  - Jackson 2.15.2 (JSON processing)
  - Logback 1.4.8 (Logging)
  - AtlantaFX 2.0.1 (UI theming)

## 📖 Documentation

- **English**: `README.md` (this file)
- **中文**: `README_ZH.md`
- **Platform guides**: `Windows/README.md`, `Linux/README.md` (and `*_ZH.md`)

## 🐛 Troubleshooting

### Application won't start

- Check the log file (`logs\app-out.log` on Windows, `logs/stdout.log` on Linux)
- Verify Java: `java -version` (must be 17+)

### Linux: `no suitable pipeline found`

- Run `./install.sh` to install GTK3/OpenGL/X11 libraries for your distro
- The launcher retries automatically with `-Dprism.order=sw`; you can also run:
  `java -Dprism.order=sw -jar Aerofalcon-Linux1.7.2.jar`
- VM without 3D acceleration: enable 3D, or use the software renderer
- SSH / headless: GUI requires a display (`xvfb-run -a ./Aerofalcon.sh` for smoke tests only)

### "This JAR has no Linux JavaFX natives"

- You are running the Windows JAR on Linux — use the `Linux/` package

### Out of memory

- Increase JVM heap by adding `-Xmx2G` to the java command line

## 🔗 Runtime Directories

Created on first launch:

```
config/     Site credentials & settings (encrypted)
logs/       Runtime & audit logs
plugins/    User plugins
shells/     Generated server-side scripts
```

**Important**: `config/` contains encrypted site credentials. Keep it secure and backed up.

## ⚖️ License & Authorization

Provided for educational and authorized penetration testing purposes only.
By using this software you agree to use it only on systems you own or have
explicit permission to test, comply with all applicable laws, and accept full
responsibility for your actions.

**Any misuse is the user's sole responsibility.**

---

**Version**: 1.7.2 · **Release Date**: 2026-10-28 · **Built with**: Java 17, JavaFX, Maven
