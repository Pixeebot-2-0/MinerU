# 常见问题解答

#### 1.离线部署首次运行，报错urllib.error.URLError: <urlopen error [Errno 101] Network is unreachable>
    
首次运行需要在线下载一个小的语言检测模型，如果是离线部署需要手动下载该模型并放到指定目录。
参考：https://github.com/opendatalab/MinerU/issues/121

#### 2.在较新版本的mac上使用命令安装pip install magic-pdf[full-cpu] zsh: no matches found: magic-pdf[full-cpu]

在 macOS 上，默认的 shell 从 Bash 切换到了 Z shell，而 Z shell 对于某些类型的字符串匹配有特殊的处理逻辑，这可能导致no matches found错误。
可以通过在命令行禁用globbing特性，再尝试运行安装命令
```bash
setopt no_nomatch
pip install magic-pdf[full-cpu]
```

#### 3.在intel cpu 的mac上 安装最新版的 magic-pdf[full-cpu] (>=0.6.1) 不成功

完整功能包依赖的公式解析库unimernet限制了pytorch的最低版本为2.3.0，而pytorch官方没有为intel cpu的macOS 提供2.3.0版本的预编译包，所以会产生依赖不兼容的问题。
可以先尝试安装unimernet的老版本之后再尝试安装完整功能包的其他依赖。（为避免依赖冲突，请激活一个全新的虚拟环境）
```bash
pip install magic-pdf
pip install unimernet==0.1.0
pip install matplotlib ultralytics paddleocr==2.7.3 paddlepaddle
```

#### 4.在部分较新的M芯片macOS设备上，MPS加速开启失败
卸载torch和torchvision，重新安装nightly构建版torch和torchvision
```bash
pip uninstall torch torchvision
pip install --pre torch torchvision --index-url https://download.pytorch.org/whl/nightly/cpu
```
参考: https://github.com/opendatalab/PDF-Extract-Kit/issues/23