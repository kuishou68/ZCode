# third-party 目录说明

本目录存放第三方 license 盘点数据与上游声明原文，供声明生成与许可门禁使用。整体流程见根目录 [THIRD-PARTY-NOTICES.md](../THIRD-PARTY-NOTICES.md) 与 [NOTICE.md](../NOTICE.md)。

## 数据文件

- `inventory.json`：全 workspace 生产依赖的精确版本、来源引用与哈希。
- `upstream/`：按 sha256 命名的上游 license 原文文本。
- `runtime/`：随发行物内置的 Node 运行时 LICENSE 与来源清单（`sources.json`）。
- `native-search/`：原生搜索工具的来源清单与 license 文本。
- `copied-components.json`：复制进仓库的源码/素材组件及其来源修订版。
- `embedded-components.json`：嵌入二进制内的第三方组件（如 Skia）。
- `npm-overrides.json`：构建期以本地 license 文本覆盖声明的 npm 包清单。

## 声明生成与校验

在仓库根目录执行：

```bash
node scripts/licenses.mjs notices   # 按当前生产依赖图重新生成 THIRD-PARTY-NOTICES.md
node scripts/licenses.mjs check     # 许可门禁：allowlist 之外或许可未知的包导致退出码 1
```

## 声明在发行物中的位置

- CLI 发行包：构建时复制为包内 `agent/THIRD-PARTY-NOTICES.md`（见 `scripts/build-zcode.mjs`）。
- 预编译产物：server、node-pty、glm 各平台包随 `scripts/prepare-prebuilds.mjs` 打入声明，Node 运行时另附对应 LICENSE。
- 原生搜索工具：`scripts/package-native-search-tools.mjs` 依据本目录数据，在每个工具二进制旁写入 `THIRD-PARTY-NOTICES.txt` 与 `SOURCES.json`。
