# Android-16.0.0_r4：在 Mac 上使用 Winscope

本目录提供在 Deepin 上构建的 Winscope 网页产物，用于打开和分析已有 trace。Mac 不需要 Android 源码、Android SDK、ADB、Node.js 或 npm。网页 JavaScript 和 WebAssembly 不绑定 Linux CPU 架构，可供 Intel Mac 和 Apple 芯片 Mac 的兼容浏览器运行。

## 1. 下载

在仓库首页选择 **Code → Download ZIP**，解压后进入 `Android-16.0.0_r4` 目录。也可以单独下载本目录的 `winscope-web.tar.gz` 和 `SHA256SUMS`。

## 2. 检查运行环境

在 Mac 的终端中执行：

```bash
python3 --version
```

若没有 Python 3，请从 https://www.python.org/downloads/macos/ 安装 Python 3，安装后重新打开终端。浏览器建议使用 Chrome。

## 3. 校验并解压

打开终端，输入 `cd `（末尾保留空格），将 Finder 中的 `Android-16.0.0_r4` 文件夹拖入终端，按回车。然后执行：

```bash
shasum -a 256 -c SHA256SUMS
mkdir -p web
tar -xzf winscope-web.tar.gz -C web
```

校验应显示 `winscope-web.tar.gz: OK`。解压后的 `web/` 内包含 `index.html`、`js/`、两个 `.wasm` 文件及其他资源。请保留完整目录结构。

## 4. 启动

仍在 `Android-16.0.0_r4` 目录执行：

```bash
python3 -m http.server 8080 --bind 127.0.0.1 --directory web
```

保持终端运行，在浏览器地址栏打开：

http://127.0.0.1:8080

通过 Winscope 页面选择或拖入已有 trace 文件进行分析。不要双击 `index.html`，Web Worker 等资源应通过 HTTP 加载。

服务只监听本机。停止时回到终端按 `Control+C`。下次使用不必重新解压，直接再次执行启动命令即可。

## 常见问题

- **8080 端口被占用**：将启动命令中的 `8080` 改成 `8081`，浏览器同步打开 `http://127.0.0.1:8081`。
- **打开的是文件列表或资源 404**：确认运行命令时位于本版本目录，并确认 `web/index.html` 存在。
- **空白页面或解析失败**：使用 Chrome，检查解压是否完整；打开浏览器开发者工具查看 Console 和 Network 错误。不要遗漏 `engine_bundle.js`、`.wasm` 或 `js/`。
- **是否需要运行 winscope_proxy.py**：分析已有文件不需要。压缩包保留了原构建输出中的代理脚本，但本方案不涉及设备采集。
- **是否需要联网**：网页和解析引擎从本地目录加载。原始生产页面保留了 Google Analytics 脚本引用，因此可能发出外网请求；本包未修改页面，不承诺完全离线或完全无外网请求。

## 产物说明

网页包直接来自本地 Android-16.0.0_r4 源码树的 `development/tools/winscope/dist/prod/`，未重新编译或删改。它包含原构建的内联源码映射，因此体积较大。具体来源、文件哈希及依赖锁文件哈希见 `BUILD_INFO.json`。

已在 Deepin 上验证原部署可用，并检查本分发包的文件一致性和静态 HTTP 资源访问；尚未在实际 Mac 上实测。
