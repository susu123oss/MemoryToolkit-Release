
<h1 align="center">MemoryToolkit</h1>

<p align="center">
  <strong>MT 内存工具 · iOS 内存搜索、调试与自动化工作台</strong>
</p>

<p align="center">
  独立 App + 系统级悬浮窗，把地址搜索、稳定定位、硬件断点、ARM64 汇编、插件自动化以及 AI / CE / MCP 集成到同一条工作流中。
</p>

<p align="center">
  <img alt="iOS 14+" src="https://img.shields.io/badge/iOS-14%2B-111111?style=flat-square&logo=apple">
  <img alt="arm64" src="https://img.shields.io/badge/Architecture-arm64-5E5CE6?style=flat-square">
  <img alt="TrollStore and DEB" src="https://img.shields.io/badge/Install-TrollStore%20%7C%20DEB-0A84FF?style=flat-square">
  <img alt="Chinese and English" src="https://img.shields.io/badge/Language-中文%20%7C%20English-34C759?style=flat-square">
</p>

<p align="center">
  <a href="#核心能力">核心能力</a> ·
  <a href="#典型工作流">典型工作流</a> ·
  <a href="#安装">安装</a> ·
  <a href="#本地构建">本地构建</a> ·
  <a href="#兼容性与边界">兼容性与边界</a>
</p>

> MemoryToolkit 是通用技术调试工具，仅用于安全研究、逆向工程学习和合规范围内的技术测试，不针对任何特定应用。

## 不只是“搜到一个地址”

很多内存工具停留在“搜索数值 → 修改数值”。MemoryToolkit 更关注完整的分析闭环：

1. **发现**：通过精确、模糊、联合、临近或字符串搜索定位候选地址。
2. **稳定**：利用指针链、PointerMap、特征码与交叉验证抵抗地址漂移。
3. **解释**：通过读写硬件断点、寄存器现场和 ARM64 反汇编理解数据为何变化。
4. **固化**：将内存修改、指针链、特征码和汇编补丁整理为可复用插件或自动化流程。
5. **协作**：使用可配置 AI Agent、MCP Server 或 CE 协议服务扩展分析方式。

## 产品预览

## 典型工作流

```mermaid
flowchart LR
    A["附加目标进程"] --> B["搜索内存<br/>精确 · 模糊 · 联合"]
    B --> C["稳定定位<br/>指针链 · 特征码 · 交叉验证"]
    C --> D["观察现场<br/>硬件断点 · 寄存器 · 反汇编"]
    D --> E["修改验证<br/>写入 · 冻结 · ARM64 补丁"]
    E --> F["沉淀方案<br/>插件 · 流程脚本 · AI / MCP"]
```

## 核心能力

| 能力 | 解决的问题 | 主要功能 |
| --- | --- | --- |
| **内存搜索与查看** | 从大量地址中快速找到目标数据 | 精确/模糊/联合/临近/范围/字符串搜索，I8～I64、U8～U64、F32/F64、字符串与十六进制查看，批量修改、递增、冻结与 XOR 修改 |
| **指针与特征码** | 地址在重启或版本变化后发生漂移 | 多级指针链、正负偏移、PointerMap 快照、跨快照验证、上下/下上双向特征扫描、质量评分与交叉验证 |
| **硬件断点调试** | 找到谁在读取或写入某块内存 | ARM64 读/写/读写断点，命中日志、旧值/新值、寄存器、调用栈与现场汇编 |
| **反汇编与补丁** | 从数据变化继续追到代码逻辑 | ARM64 单条/函数反汇编、分支目标、汇编生成、机器码校验、NOP/指令补丁、冲突检测与原始字节恢复 |
| **插件与自动化** | 把一次分析变成可重复执行的方案 | 指针、特征码、规则锚点、流程脚本和汇编补丁配置，插件组装、加载、测试与恢复 |
| **外部工具集成** | 让手机端能力接入现有分析环境 | 内置 CE 协议远程服务、MCP HTTP/SSE 服务、H5 页面桥接、可配置 AI Provider 与工具调用循环 |

### 搜索与内存操作

- 精确搜索、改善搜索、模糊搜索、联合搜索、临近搜索、字符串搜索与撤销。
- 支持常见整数、浮点、无符号整数、字符串和十六进制视图。
- 搜索结果可批量偏移、修改、冻结、解冻或递增处理。
- 内存查看器可在数值视图和 ARM64 汇编视图之间切换。

### 稳定地址定位

- 多级指针搜索支持深度、偏移范围、循环检测和地址有效性验证。
- PointerMap 快照与跨轮次验证用于筛选跨重启仍稳定的指针链。
- 特征码扫描支持上下方向、双向采样、二次对比、质量评分与持久化测试。
- 指针、特征与汇编补丁可以组合成后续可复用的配置。

### 断点、寄存器与 ARM64

- 支持读、写、读写硬件断点以及代码断点命中现场。
- 查看触发指令、寄存器、调用栈、模块信息和附近反汇编。
- 内置 ARM64 汇编与反汇编能力，支持条件分支及远距离分支处理。
- 补丁记录保存原始字节与修改字节，可停用、恢复并检查第三方修改冲突。

### AI、MCP 与 CE

- **AI Agent**：配置 Provider、Base URL、API Key 与模型后，可结合断点现场调用内存、寄存器、反汇编和补丁工具。
- **MCP Server**：提供 HTTP/SSE 与 JSON-RPC 工具入口，可通过 Wi-Fi 或 USB 端口转发连接支持 MCP 的客户端。
- **CE Server**：提供 CE 协议远程服务，支持 PC 端通过 Wi-Fi 或 USB/iproxy 连接。
- **H5 Bridge**：为浮动 H5 页面提供部分进程、搜索、读写和窗口控制接口。

### 为手机操作优化

- 系统级悬浮窗跟随前台应用方向调整布局，兼顾竖屏与横屏场景。
- 中文 / English、浅色 / 深色 / 跟随系统主题。
- 内置中文拼音与英文输入模式，覆盖搜索、汇编编辑、插件配置和 AI 设置等输入场景。
- 断点、汇编和 AI 分析均以可见状态卡片呈现关键过程。

## 安装

| 设备环境 | 安装包 | 说明 |
| --- | --- | --- |
| TrollStore | `MemoryToolkitApp-vX.Y.Z.tipa` | 独立 App，包内为 `Payload/MemoryToolkitApp.app` |
| rootful 越狱 | `MemoryToolkitApp-vX.Y.Z-rootful.deb` | 安装到 `/Applications/MemoryToolkitApp.app` |
| rootless 越狱 | `MemoryToolkitApp-vX.Y.Z-rootless.deb` | 安装到 `/var/jb/Applications/MemoryToolkitApp.app` |
| RootHide | `MemoryToolkitApp-vX.Y.Z-roothide.deb` | 使用 RootHide 对应包管理环境 |

> TIPA 与三种 DEB 面向不同安装环境，请只选择与设备环境匹配的包。跨进程读取、写入和调试能力仍取决于设备权限与当前运行环境。

## 兼容性与边界

| 项目 | 当前范围 |
| --- | --- |
| 系统 | iOS 14.0+ |
| 架构 | iPhoneOS arm64；RootHide DEB 使用对应 arm64e 打包环境 |
| 主 App 方向 | 主界面为竖屏；系统级悬浮窗会跟随前台应用方向适配 |
| 安装方式 | TrollStore TIPA、rootful/rootless/RootHide DEB |
| 硬件断点 | 受 ARM64 硬件槽位与目标进程状态限制，当前实现最多管理 4 个 |
| Cheat Engine | 提供 CE 协议远程服务；建议 CE 7.5+，推荐 7.6 |
| AI | 需要自行配置可访问的 Provider、Base URL、API Key 与模型 |
| MCP | 提供 HTTP/SSE 工具服务；应只在可信网络或 USB 转发环境中启用 |
| H5 | 提供部分兼容映射，不承诺完整 H5GG API |


## 项目结构

```text
MemoryToolkitApp/
├── Sources/
│   ├── Agent/          # AI Agent 与工具调用
│   ├── Breakpoint/     # 硬件断点、现场与日志
│   ├── CEServer/       # CE 协议服务
│   ├── Core/           # 进程附加与内存访问
│   ├── Disassembler/   # ARM64 汇编、反汇编与补丁
│   ├── Engine/         # 搜索、指针与特征码引擎
│   ├── MCP/            # MCP HTTP/SSE 服务
│   ├── Plugin/         # 插件配置、合成与加载
│   └── UI/             # 主面板、悬浮窗与拼音键盘
├── Resources/
├── Makefile
└── control

PluginTemplate/         # 可嵌入的插件模板
scripts/                # 构建、审计、上传与日志工具
```

## 使用边界

- 仅在您拥有、开发或已获得明确测试许可的目标上使用。
- 不得用于非法侵入、数据窃取、破坏服务公平性或其他违反法律法规的行为。
- 内存写入、进程冻结、断点和汇编补丁均可能造成目标进程崩溃或数据损坏，请保留回滚方案。
- AI 输出与自动化方案必须结合真实寄存器、内存和汇编现场人工复核。

---

<p align="center">
  <strong>MemoryToolkit</strong><br>
  从发现地址，到解释现场，再到沉淀可复用方案。
</p>
