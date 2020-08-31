# 发行代币

#### 节点所有者发行TOKEN须知：

##### 1、发行TOKEN须按规则至少自质押GARD和锁仓GGT，请通过查询质押发行TOKEN配置命令查看数量及GGT锁定周期。

查询命令：

```
hashgardcli query staking issue-token-config
```

返回结果：

```
{
  "lock_coins": [
    {
      "denom": "uggt",
      "amount": "1000000000000"
    }
  ],
  "lock_period_height": "10512000",
  "min_self_delegation": "10000000000000"
}
```

`lock_coins`：锁仓GGT数量（1GGT=1000000uggt)

`lock_period_height`GGT锁定周期，发行TOKEN后出块数满足要求则可赎回锁定的GGT资产，若不满足则可以发起提案通过投票的方式取回。

`min_self_delegation`自质押GARD最小值，发行货币时锁定，节点退出后可以发起提案通过投票的方式取回。

##### 2、发行TOKEN您可配置是否预挖指定的数量到指定的地址

##### 3、只有当您的节点出块时才可挖出您发行的TOKEN，您可分别指定您的节点和所有投票节点可在每块挖出的数量

##### 4、节点解绑到期后，自抵押的GARD按发行规则最少抵押的部分会转入到发行的TOKEN对应的锁仓地址，剩余的会返回到质押者地址

##### 5、节点解绑到期后，锁仓的GGT按规则在锁仓高度内则转入到发行的TOKEN对应的锁仓地址，否则会返回到质押者地址

##### 6、节点解绑到期后，任何人都可以发起提案从发行的TOKEN对应的锁仓地址支取GARD和GGT，由所有节点投票同意是否可支取

发行代币命令：

```
hashgardcli tx staking issue-token stake_issue_token.json --from ${name}
```

`stake_issue_token.json`内容：

```
{
	"denom": "uexp",
	"total_supply": "100000000000000",
	"pre_mint_address": "",
	"pre_mint_amount": "0",
	"description": {
		"whole_name": "Experience",
		"website": "https://www.exp.top/",
		"icon": "https://www.exp.top/img/icon.png",
		"details": "exp"
	},
	"genesis_height": 100000,
	"per_block_mint": [{
			"start_height": 100000,
			"self_node_amount": "10000000",
			"others_node_amount": "5000000"
		},
		{
			"start_height": 8200000,
			"self_node_amount": "6000000",
			"others_node_amount": "600000"
		}
	]
}
```

`denom`发行TOKEN的命名，以u开头，例：发行名为EXP的TOKEN，则denom填写uexp。

`total_supply`发行总量，默认的小数位数是6位数精度，例：发行10000个TOKEN，则total_supply填写10000000000（即1EXP=1000000uexp)。

`pre_mint_address`预挖地址，若有预挖需求则填写预挖出TOKEN存放的钱包地址。

`pre_mint_amount`预挖数量，若有预挖需求则填写预挖出TOKEN数量，若无则填写0。

`genesis_height`发行的TOKEN开始挖矿的高度。

