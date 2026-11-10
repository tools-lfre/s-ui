# s-ui 安装脚本（自托管版）

这是 [alireza0/s-ui](https://github.com/alireza0/s-ui) 的安装脚本，托管在 **tools-lfre/s-ui**，
安装源为 `1.3.10` 版本（取自 `bulianglin/demo` 的镜像发行版）。

## 一键安装

```bash
VERSION=1.3.10 && bash <(curl -Ls https://raw.githubusercontent.com/tools-lfre/s-ui/main/s-ui-install.sh) $VERSION
```

不指定版本则自动拉取本仓库最新 release：

```bash
bash <(curl -Ls https://raw.githubusercontent.com/tools-lfre/s-ui/main/s-ui-install.sh)
```

## 支持的架构

| 架构 | 安装包 |
|------|--------|
| x86_64 / amd64 | `s-ui-linux-amd64.tar.gz` |
| i386 / x86 | `s-ui-linux-386.tar.gz` |
| arm64 / aarch64 | `s-ui-linux-arm64.tar.gz` |
| armv7 | `s-ui-linux-armv7.tar.gz` |
| armv6 | `s-ui-linux-armv6.tar.gz` |
| armv5 | `s-ui-linux-armv5.tar.gz` |
| s390x | `s-ui-linux-s390x.tar.gz` |

Windows 版（`s-ui-windows-amd64.zip` / `s-ui-windows-arm64.zip`）同步存放在 release 中。

## 环境变量

| 变量 | 默认值 | 说明 |
|------|--------|------|
| `SUI_REPO` | `tools-lfre/s-ui` | 安装源仓库（脚本 + release 资产） |
| `SUI_UPSTREAM` | `bulianglin/demo` | 上游镜像，主源缺失资产时的备用源 |

示例：改用其他镜像仓库：

```bash
SUI_REPO=my-fork/s-ui VERSION=1.3.10 bash <(curl -Ls https://raw.githubusercontent.com/tools-lfre/s-ui/main/s-ui-install.sh) $VERSION
```

## 安装流程

1. 检测发行版并安装依赖（`wget curl tar tzdata`）
2. 按架构下载对应安装包，校验 SHA256
3. 解压至 `/usr/local/s-ui`，注册 systemd 服务 `s-ui`
4. 交互式设置面板端口、路径、订阅端口与管理员账号

安装完成后：

- 面板访问地址由脚本输出（`sui uri` 查看）
- 菜单命令：`s-ui`
- 服务管理：`systemctl status s-ui`

## 校验

`SHA256SUMS` 存放各安装包的校验值，脚本下载后会自动比对：

```bash
sha256sum -c SHA256SUMS
```

## 与上游差异

- 安装源指向本仓库 release，缺失资产时回退 `bulianglin/demo`
- 下载后增加压缩包完整性与 SHA256 校验
- 下载工具在 `wget` 失败时自动回退 `curl`
- 修复原脚本 `tar zxvf` 后删除归档的顺序问题（先解压再删除）

## 免责声明

本仓库仅托管安装脚本与发行版资产，s-ui 本体版权归 [alireza0](https://github.com/alireza0/s-ui) 所有。
请仅用于合规用途，遵守当地法律法规。
