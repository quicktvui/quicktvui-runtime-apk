# QuickTVUI Runtime APK Repository

这个仓库用于分发 QuickTVUI Runtime APK，并同时支持 `debug` 和 `release` 两个通道，目标是：
- 人和 AI 都能快速检索到最新可用包
- 有可直接下载链接和校验值
- 保留版本历史，方便自动化升级

推荐仓库名：`quicktvui-runtime-apk`

## 目录结构

```text
.
├── apks/
│   ├── debug/
│   │   └── quicktvui-runtime-debug-v2.9.1524.apk
│   └── release/
│       └── quicktvui-runtime-release-v2.9.1584.apk
├── checksums/
│   └── sha256.txt
└── manifests/
    ├── history.json
    ├── latest.json
    ├── latest-debug.json
    └── latest-release.json
```

## 通道约定

- `debug`：开发联调用，当前已有 `2.9.1524`
- `release`：正式发布用，当前已有 `2.9.1584`

## AI/自动化读取入口

- 总入口：`manifests/latest.json`
- Debug 最新：`manifests/latest-debug.json`
- Release 最新：`manifests/latest-release.json`
- 历史版本：`manifests/history.json`
- 完整性校验：`checksums/sha256.txt`

建议 AI 读取流程：
1. 先读 `manifests/latest.json`
2. 再按通道读 `latest-debug.json` 或 `latest-release.json`
3. 下载后用 `checksums/sha256.txt` 校验

## 下载链接规范（GitHub Releases）

Debug 版本：
`https://github.com/quicktvui/quicktvui-runtime-apk/releases/download/v2.9.1524-debug/quicktvui-runtime-debug-v2.9.1524.apk`

Release 版本（示例）：
`https://github.com/quicktvui/quicktvui-runtime-apk/releases/download/v2.9.1524/quicktvui-runtime-release-v2.9.1524.apk`

## 安装示例

```bash
adb install -r apks/debug/quicktvui-runtime-debug-v2.9.1524.apk
```

## 发布流程

1. 生成 APK（debug 或 release）
2. 文件命名统一为：
   - `quicktvui-runtime-debug-v<version>.apk`
   - `quicktvui-runtime-release-v<version>.apk`
3. 更新 `checksums/sha256.txt`
4. 更新 `manifests/latest-*.json` 与 `manifests/history.json`
5. 创建对应 Tag 并上传到 GitHub Releases

完成后，这个仓库可以同时服务人类下载和 AI 自动化分发。
