# Winscope 构建产物

按 Android 版本归档的 Winscope 网页构建产物，用于在 macOS 等系统上本地分析 Android trace。

无需 Android 源码、Node.js 或 npm。需要 Python 3 和支持 WebAssembly 的浏览器；建议使用 Chrome。

| Android 版本 | 使用说明 | 构建产物 |
| --- | --- | --- |
| Android-16.0.0_r4 | [Mac 操作说明](Android-16.0.0_r4/README.md) | [winscope-web.tar.gz](Android-16.0.0_r4/winscope-web.tar.gz) |

点击 GitHub 的 **Code → Download ZIP** 下载仓库，解压后按对应版本的文档启动。也可以通过 `git clone https://github.com/maoqb/winscope.git` 下载。

## 目录约定

每个 Android 版本使用独立的顶层目录，例如 `Android-16.0.0_r4/`。后续版本沿用相同布局，包含操作说明、网页压缩包、校验文件和构建来源记录。

这是个人整理的构建产物仓库。Winscope 来源于 Android Open Source Project；各第三方组件遵循各自许可证，参见 LICENSE 和版本目录中的 THIRD_PARTY_NOTICES.txt。
