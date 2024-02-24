# 在Openwrt上运行TShock 

## 第一步：下载.NET 6 SDK

[Download .NET 6.0](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)

下载里面的[Arm64 Alpine](https://dotnet.microsoft.com/en-us/download/dotnet/thank-you/sdk-6.0.419-linux-arm64-alpine-binaries)，因为我的机器是ARM64架构的..`uname -a`显示`aarch64`

解压它

安装dotnet依赖项：

```bash
opkg update
opkg install icu-full-data
```

给它设置环境变量

编辑`~/.profile`添加如下内容：

```bash
export DOTNET_ROOT=/opt/dotnet
export PATH=$PATH:/opt/dotnet
```

## 第二步：编译TShock

因为TShock官网上没有linux-musl-arm64的已编译版本，只能自己编译

按官方指南

1. `opkg update && opkg install git-http`
  
2. `git clone https://github.com/Pryaxis/TShock.git --recurse-submodules`
  
3. `cd TShock`
  
4. `dotnet build`
  
5. `cd TShockLauncher`
  
6. `dotnet add package SQLitePCLRaw.bundle_e_sqlite3 --version 2.1.8`
  
7. `dotnet publish -r linux-musl-arm64 -f net6.0 -c Release -p:PublishSingleFile=true --self-contained false`
  

如果少了6这个补丁，编译后的TShock无法正常运行
