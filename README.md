# 在 WSL2 Ubuntu 中使用 clang++ 交叉编译 C++ 代码到 Windows 可执行程序

## 安装 rust
```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

配置镜像`~/.cargo/config.toml`
```
[source.crates-io]
replace-with = 'mirror'

[source.mirror]
registry = "sparse+https://mirrors.tuna.tsinghua.edu.cn/crates.io-index/"
```

## 安装 [xwin](https://github.com/Jake-Shadle/xwin)
```
cargo install xwin --locked
```

## 下载Windows相关头文件和库
```
xwin --accept-license splat --output ./xwin
```

## 编译程序
```
clang++ --target=x86_64-pc-windows-msvc -isystem xwin/crt/include -isystem xwin/sdk/include/ucrt -isystem xwin/sdk/include/um -isystem xwin/sdk/include/shared -fuse-ld=lld-link -L xwin/crt/lib/x86_64 -L xwin/sdk/lib/ucrt/x86_64 -L xwin/sdk/lib/um/x86_64 main.cpp -o /mnt/c/Users/icuxika/Desktop/CrossCompilationDemo.exe -luser32
```