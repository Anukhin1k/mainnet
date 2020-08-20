# Installation

You will install two executables according to this guide:

1. hashgard. This is the main program, it runs as a node of Hashgard blockchain.
2. hashgardcli. This is the client of Hashgard, it's used to execute most commands like creating wallet and sending transactions.

## Prepare Your VPS

It is recommended to run the Hashgard Validator Node on VPS.

If you run the node on your local machine, it will be jailed when your computer is hibernating or shutting down.

**Recommend Configurations**

- CPU: 2 Cores
- RAM: 8GB
- Storage: 100GB SSD
- OS: Ubuntu 16.04+ ；CentOS 7.5+

## Download Executables

Download packages from [Github Releases](https://github.com/hashgard/hashgard/releases) according to your OS,

then extract the excutables (hashgard and hashgardcli) to the specified directory:

- Linux / MacOS: /usr/local/bin

Run the commands below to test the executable installation:

```bash
hashgardd help
hashgardcli help
```

If they are installed successfully, you'll see the output:

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
