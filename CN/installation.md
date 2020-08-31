# Hashgard 安装文档

Hashgard 公链采用 Go 语言编写，它可以在任何能够编译并运行 Go 语言程序的平台上工作。

根据本文档，您将安装两个可执行程序：

1. hashgard，这是 Hashgard 节点的主程序，它将作为系统服务运行并接入 Hashgard 网络。
2. hashgardcli，这是 Hashgard 命令行客户端，用来执行大部分命令，如创建钱包、发送交易等。

## 配置您的服务器

Hashgard 公链基于 Cosmos-SDK 开发，Cosmos SDK 是使用 Go 语言开发的区块链应用程序的框架。

建议在 Linux 服务器中运行验证人节点，如果您在本地电脑上运行，那么当您的电脑休眠或关机时，您的验证人节点将会进入离线 jailed 状态。

### 推荐配置

- CPU：2Core
- 内存：8GB
- 磁盘：100GB SSD
- 操作系统：Ubuntu 16.04+ ；CentOS 7.5+

## 下载可执行文件

从 github [下载](https://github.com/hashgard/hashgard/releases) 您的操作系统所对应的版本，
并将可执行程序 hashgard、hashgardcli 解压到对应的目录下：

- Linux / MacOS: /usr/local/bin

当完成解压之后，可在 Terminal / CMD 中检查是否安装成功：

```bash
hashgardd help --home <path>
hashgardcli help --home <path>
```

如果出现

```plain
Hashgard Daemon (server)

Usage:
  hashgardd [command]

Available Commands:
  init                Initialize private validator, p2p, genesis, and application configuration files
  collect-gentxs      Collect genesis txs and output a genesis.json file
  migrate             Migrate genesis to a specified target version
  gentx               Generate a genesis tx carrying a self delegation
  validate-genesis    validates the genesis file at the default location or at the location passed as an arg
  add-genesis-account Add genesis account to genesis.json
  testnet             Initialize files for a Gaiad testnet
  replay              Replay hashgard transactions
  start               Run the full node
  unsafe-reset-all    Resets the blockchain database, removes address book files, and resets priv_validator.json to the genesis state
                      
  tendermint          Tendermint subcommands
  export              Export state to JSON
                      
  version             Print the app version
  help                Help about any command

Flags:
  -h, --help                    help for hashgardd
      --home string             directory for config and data (default "/root/.hashgardd")
      --inv-check-period uint   Assert registered invariants every N blocks
      --log_level string        Log level (default "main:info,state:info,*:error")
      --trace                   print out full stack trace on errors

Use "hashgardd [command] --help" for more information about a command.
[root@instance-41vkh4rr ~]# hashgardcli help
Command line interface for interacting with hashgardd
```

则表示安装成功
