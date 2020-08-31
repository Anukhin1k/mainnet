# README_CN

Hashgard 公链采用 Go 语言编写，它可以在任何能够编译并运行 Go 语言程序的平台上工作。

根据本文档，您将安装两个可执行程序：

1. hashgardd，这是 Hashgard 节点的主程序，它将作为系统服务运行并接入 Hashgard 网络。
2. hashgardcli，这是 Hashgard 命令行客户端，用来执行大部分命令，如创建钱包、发送交易等。

## 配置您的服务器

Hashgard 公链基于 Cosmos-SDK 开发，Cosmos SDK 是使用 Go 语言开发的区块链应用程序的框架。

建议在 Linux 服务器中运行验证人节点，如果您在本地电脑上运行，那么当您的电脑休眠或关机时，您的验证人节点将会进入离线 jailed 状态。

### 推荐配置

- CPU：2Core
- 内存：8GB
- 磁盘：100GB SSD
- 操作系统：Ubuntu 16.04+ ；CentOS 7.5+

## 加入主网

### 安装hashgard

从 github [下载](https://github.com/hashgard/hashgard/releases) 您的操作系统所对应的版本，并将可执行程序 hashgardd、hashgardcli 解压到对应的目录下：

- Linux: /usr/local/bin

当完成解压之后，可在 Terminal / CMD 中检查是否安装成功：

```bash
hashgardd help
hashgardcli help
```

如果出现

```plain
Command line interface for interacting with hashgardd

Usage:
  hashgardcli [command]

Available Commands:
  status      Query remote node for status
  config      Create or query an application CLI configuration file
  query       Querying subcommands
  tx          Transactions subcommands
              
  rest-server Start LCD (light-client daemon), a local REST server
              
  keys        Add or view local private keys
              
  version     Print the app version
  help        Help about any command

Flags:
      --chain-id string   Chain ID of tendermint node
  -e, --encoding string   Binary encoding (hex|b64|btc) (default "hex")
  -h, --help              help for hashgardcli
      --home string       directory for config and data (default "/root/.hashgardcli")
  -o, --output string     Output format (text|json) (default "text")
      --trace             print out full stack trace on errors

Use "hashgardcli [command] --help" for more information about a command.
```

则表示安装成功

### 本地初始化

首先，初始化节点并创建必要的配置文件：

```bash
hashgardd init <your moniker name> --home <path>
```

::: 注意

<path>为节点数据目录

moniker只能包含ASCII字符。使用Unicode字符会使得你的节点不可访问
:::

从[latest](https://github.com/hashgard/mainnet/tree/master/latest)中获取主网信息，包含了主网最新版本配置文件和genesis文件，将[config.toml](https://github.com/hashgard/mainnet/blob/master/latest/config.toml)、[genesis.json](https://github.com/hashgard/mainnet/blob/master/latest/genesis.json)以及[hashgardd.toml](https://github.com/hashgard/mainnet/blob/master/latest/hashgardd.toml)放至`<path>/.hashgardd/config/`目录下。

你可以在`<path>/.hashgardd/config/config.toml`文件中编辑`moniker`:

```toml
# A custom human readable name for this node
moniker = "<your moniker name>"
```

你的全节点已经初始化成功！

运行命令验证配置的正确性:

```bash
hashgardd start --home <path>
```

检查一切是否平稳运行中:

```bash
hashgardcli status
```



## 创建你的验证人

你可以通过抵押token来创建一个新的验证人。你可以通过运行下面的命令来查看你的验证人公钥：

```bash
hashgardd tendermint show-validator --home <path>
```

使用下面的命令创建你的验证人：

::: 注意
不要使用多于你所拥有的`ugard`!
:::

```bash
hashgardcli tx staking create-validator \
  --amount=1000000ugard \
  --pubkey=$(gaiad tendermint show-validator --home <path>) \
  --moniker="choose a moniker" \
  --chain-id=hashgard \
  --commission-rate="0.10" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --gas="auto" \
  --fees="1000ugard" \
  --from=<key_name>
```

::: 提示
在指定commission参数时，`commission-max-change-rate`用于度量`commission-rate`的百分比点数的变化。比如，1%到2%增长了100%，但反映到`commission-rate`上只有1个百分点。
:::

::: 提示
如果没有指定，`consensus_pubkey`将默认为`hashgardd tendermint show-validator`命令的输出。`key_name`是将用于对交易进行签名的私钥的名称。
:::

你可以在第三方区块链浏览器上确定你是否处于验证人行列。



