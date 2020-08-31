# Hashgard 主网指南

该文档目的是介绍如何运行一个 Hashgard 节点并加入主网

## 运行 Hashgard 节点

### 步骤 1：在您的服务器上安装 Hashgard

请参照 [hashgard 安装文档](./installation.md) 安装 Hashgard。

### 步骤 2：创建钱包

```bash
hashgardcli keys add ${your_wallet_name}
```

记得在创建钱包后，将助记词妥善保存在安全的地方。

如果你忘记密码，这是恢复账户的唯一方法。

检测你的钱包：

```
hashgardcli keys list
```

### 步骤 3：设置默认参数

设置 hashgardcli 命令行客户端的默认连接节点：

```bash
hashgardcli config chain-id hashgard
hashgardcli config trust-node true
```

格式化输出：

```plain
hashgardcli config indent true
hashgardcli config output json
```

### 步骤 4：初始化节点并获取配置文件

#### 4.1：初始化节点

```bash
hashgardd init ${your_node_name} --chain-id=hashgard --home <path>
```

如果您参与过hashgard的测试网，需要在使用 `init` 命令初始化节点之前删掉旧的数据文件：

```bash
rm -rf $HOME/.hashgardd
```

#### 4.2：下载 genesis 和 config 文件

[latest](https://github.com/hashgard/mainnet/tree/master/latest)中包含了主网最新版本配置文件和genesis文件。进入 hashgard 的 config 文件路径，使用hashgard主网网络的[genesis.json](https://github.com/hashgard/mainnet/blob/master/latest/genesis.json) 和[config.toml](https://github.com/hashgard/mainnet/blob/master/latest/config.toml)文件替换掉 hashgard 初始化生成的对应文件，同时将[hashgardd.toml](https://github.com/hashgard/mainnet/blob/master/latest/hashgardd.toml)放至该目录下。

#### 4.3: 修改配置文件

编辑 `~/.hashgard/config/config.toml` 文件，
您需要修改其中 `moniker` 字段，
`moniker` 是您的节点名称

```toml
# A custom human readable name for this node
moniker = "<your moniker name>"
```

### 步骤 5：运行完整节点

使用以下命令启动节点：

```bash
hashgardd start > hashgard.log &
```

检查节点状态是否正常：

```bash
hashgardcli status
```

如果节点成功运行，您将看到以下输出:

```json
{
  "node_info": {
    "protocol_version": {
      "p2p": "5",
      "block": "8",
      "app": "0"
    },
    "id": "b783ac2b41da096ddc3a26c2a39e3b0c1ea49d9e",
    "listen_addr": "127.0.0.190:26656",
    "network": "hashgard",
    "version": "0.27.0",
    "channels": "4020212223303800",
    "moniker": "hashgard_test",
    "other": {
      "tx_index": "on",
      "rpc_address": "tcp://0.0.0.0:26657"
    }
  },
  "sync_info": {
    "latest_block_hash": "AFB6261A76DCC6176FF5248B3B5BEDEEBD38B6DA3D18AD21ADD4054AEDEED016",
    "latest_app_hash": "1DEAF3D71AD735F4E375439DAFD96C8934E944D8D32F6179F55C5470E219D132",
    "latest_block_height": "77280",
    "latest_block_time": "2018-12-24T07:13:53.787154732Z",
    "catching_up": false
  },
  "validator_info": {
    "address": "5959DF3D28F601407A98D0B038174E288ED45BD7",
    "pub_key": {
      "type": "tendermint/PubKeyEd25519",
      "value": "wYrxKp7cw14eQiqzfGBggEV474ZA2lc35AieJM5SM6Y="
    },
    "voting_power": "950"
  }
}
```

当您看到 `catching_up` 是 `false`，表示节点的区块数据与 testnet 已经同步完成，否则表示它仍在同步。

您现在已经成功运行了一个 Hashgard 完整节点并接入主网。

## 后续步骤

您现在拥有一个活动的完整节点。下一步是什么？

### 步骤 6：升级到验证人( Validator )节点

您可以将您的节点升级成为 Hashgard 验证人节点，继续进入 [创建验证人节点](./create-validator.md)。

您也可以委托，解绑，再委托。

### 步骤 7：验证人节点发行TOKEN

当您的节点成为Hashgard验证人节点且满足条件后，您可以 [发行自定义的token](./issue-token.md)通过链上挖出。
