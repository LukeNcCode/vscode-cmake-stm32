
## ⚙️ 环境要求

- [VSCode](https://code.visualstudio.com/)
- [CMake](https://cmake.org/) + 交叉编译工具链（如 `arm-none-eabi-gcc`）
- [SEGGER JLink](https://www.segger.com/downloads/jlink/) 驱动
- VSCode 扩展：
  - [Cortex-Debug](https://marketplace.visualstudio.com/items?itemName=marus25.cortex-debug) — 用于 JLink 调试
  - [Tasks](https://marketplace.visualstudio.com/items?itemName=actboy168.tasks) — 在状态栏自动显示 `Build` / `Flash` 按钮
  - 其他扩展详见加载STM32.code-profile
  
## 🚀 快速开始

1. 安装上述 VSCode 扩展。
2. 将本仓库的 `.vscode` 文件夹复制到你的 STM32 项目根目录（或直接使用本仓库作为模板）。
3. 根据实际环境修改配置项（见下方“需要自定义的配置项”）。
4. 用 VSCode 打开该项目工作区。
5. 左下角状态栏会自动出现 **Build** 和 **Flash** 按钮：
   - 点击 **Build** → 编译项目
   - 点击 **Flash** → 通过 JLink 烧录固件
6. 按 `F5` 启动 JLink 调试，程序会运行至 `main` 并停在断点处。

## 🔧 需要自定义的配置项

使用前请根据实际情况修改以下路径与参数：

### `tasks.json`
| 配置项 | 说明 |
|--------|------|
| `command` | JLink.exe 实际安装路径 |
| `-device` | 目标芯片型号（如 `STM32F407ZG`） |
| `-CommanderScript` | `flash.jlink` 脚本路径 |

### `launch.json`
| 配置项 | 说明 |
|--------|------|
| `executable` | 编译生成的 `.elf` 文件路径 |
| `serverpath` | `JLinkGDBServerCL.exe` 实际路径 |
| `device` | 目标芯片型号 |

### `flash.jlink`
```text
loadfile ./build/Debug/your_project.elf   # 替换为实际 elf 文件
r                                          # 复位
g                                          # 运行
exit                                       # 退出