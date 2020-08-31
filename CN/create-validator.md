# 创建验证人节点

### 验证人是什么

验证人节点负责通过投票将新块提交给整个区块链网络。
验证人节点如果离线、双重签署交易或不投票，验证人将会受到惩罚，其抵押的股权将被削减。
如果您要成为验证人节点，请确保您节点的安全性，以避免资产损失。

### 创建验证人

> 在此之前，请确保您已经创建了一个本地钱包并持有一定量的主网币GARD。
>

您可以通过运行以下命令找到验证人 pubkey：

```bash
hashgardd tendermint show-validator
```

接下来，通过 hashgardcli tx staking create-validator 命令使节点升为验证人节点：

```bash
hashgardcli tx staking create-validator \
  --amount=1000000ugard \
  --pubkey=$(gaiad tendermint show-validator) \
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

> commission 参数
>
> commission-max-change-rate 是 commission-rate 的变更百分比。
> 如：1% 到 2% commission-rate 有 100% 的变更, 但变更百分比 commission-max-change-rate 只有 1%。

> Min-self-delegation
>
> 最小自抵押数量必须为正整数。
> 如：min-self-delegation=10 表示您的验证人节点在任何时候的抵押数量不能小于 10gard。

### 查看验证人信息

使用以下命令查看验证人的信息：

```bash
hashgardcli query staking validator ${validator-address}
```

您也可以通过区块链浏览器查看验证人信息：
https://explorer.hashgard.com/#/validator