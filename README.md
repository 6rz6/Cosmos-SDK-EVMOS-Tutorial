# Cosmos-SDK-EVMOS-Tutorial
Create your own blockchain and Validator Nodes using the Cosmos SDK and EVMOS - A simple to follow tutorial (for the complete SDK Tutorial see reference 1 below)

## Its easy Getting Started
1. Install the lastest [GO version](https://go.dev/doc/install) and remove previous versions

Linux CLI:
```
     rm -rf /usr/local/go
     cd /usr/local
     wget https://go.dev/dl/go1.22.1.linux-amd64.tar.gz
     tar -C /usr/local -xzf go1.22.1.linux-amd64.tar.gz
     run -> $ go version in CLI -> Expected result: go version go1.22.1 linux/amd64
```
2. 

3. Install node      ```sudo apt install npm```
4. install GNUmake   ```sudo apt install make```
5. install Rust      ```curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh```
6. Pull the cosmos SDK from github and clone it to /home/cosmos/cosmos-sdk
   Make sure you are using the same version as below v0.45.4
   ```
   mkdir cosmos
   cd cosmos
   git clone https://github.com/cosmos/cosmos-sdk
   cd cosmos-sdk
   git checkout v0.45.4 

   ```
8. If Everything was installed correctly, you should be able to run in /home/cosmos/cosmos-sdk/
   ```make build```
   once the build has been completed without errors.
   run ```./build/simd version``` which should return 0.45.4.

All the steps above are described in the [cosmos.network tutorials portal](https://tutorials.cosmos.network/tutorials/3-run-node/#run-a-node-api-and-cli) 
and in the [full sdk tutorial including Docker images and cosmos sdk official docs](https://tutorials.cosmos.network/tutorials/2-setup/)
## How to Use the Cosmos SDK to Run a Node, API, and CLI
1. watch this short [vid to review the next steps](https://youtu.be/wNUjkp2PFQI)
    ```
    <iframe width="576" height="324" src="https://www.youtube.com/embed/wNUjkp2PFQI" title="Running a Node" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
    ```
2. run in folder /home/CosmosSDK/cosmos-sdk/build # ``` ./simd init demo ```    
   the output should be in a firmat of a Genenis json file (starting with "moniker": "demo")
   
4. run /home/CosmosSDK/cosmos-sdk/build # ```./simd keys list```

5. Next create keys by running ```./simd keys add b9lab``` and the expected output should be:

   ```
     **Important** write this mnemonic phrase in a safe place.
     It is the only way to recover your account if you ever forget your password.

     **happy fast write warm make glory easy ride light woman mean loving confirmed taste clear apple garden burden calm twelve visual dance high social rich**

     Press 'Enter' key to continue.
   ```

     - address: cosmos15n5glgs7n8shcptapfte6klvcwpwz3qc20t4e2
       name: b9lab
       pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey",
       "key":"Ah+vpcVHqLpwbBAzKqcecPtucu5c1HZRW8gYHxGAhY+"}'
       type: local

7. Define the amount of tokens to create followed by the token name ('stake') in our chain
   /cosmos-sdk/build # ```./simd genesis add-genesis-account b9lab 100000000stake```

8. Define the cost of staking for a Validator Node (use the chain-id name from the Genesis json_1 file) /cosmos-sdk/build #
   ```
   ./simd genesis gentx b9lab 70000000stake --chain-id test-chain-tgFWQe
     Genesis transaction written to "/root/.simapp/config/gentx/gentx-
     eee5fe21000bcbfd270e34d19f227be66cfa5084.json"
   ```

9. Finally we run /cosmos-sdk/build # ```./simd genesis collect-gentxs```
   which will output a complete json file including the keys and chain,tokens,
   allocations,gas prices (see the complete Genesis json_2 file below)


## Start The Blockchain
     
   run  ```./simd start ```

   You will see the chain initiating and the blocks getting generated with an increasing Height value which represents the block number:
   
   ![image](https://github.com/6rz6/Cosmos-SDK-EVMOS-Tutorial/assets/102882394/dcc7a296-888e-4694-b052-c0d2cee885f5)

   The blocks will keep increasing which indicates our new blockchain is running successfully:

   ![image](https://github.com/6rz6/Cosmos-SDK-EVMOS-Tutorial/assets/102882394/a3d576df-6722-4607-ad33-dee50d79e485)

### Wallet Balance

  Open a new terminal and check the balance for the account named b9lab: ``` ./simd query bank balances $(./simd keys show b9lab-1) ```
  The result will indicate the wallet balance has been decreased by the staking costs we defined for our Validator Node:

       balances:
     - amount: "30000000"
       denom: stake
       pagination:
       total: "1"

### Creating a new Wallet Account

  Create a new wallet account named student: ``` ./simd keys add student ``` 
  The result will generate another unique MNMC phrase for the student's wallet:

  ```
     **Important** write this mnemonic phrase in a safe place.
     It is the only way to recover your account if you ever forget your password.

     **skate apart write warm make glory blossom ball material fat mean confirm taste demand apple uncle burden calm twelve visual dance disease audit federal**

     Press 'Enter' key to continue.
  ```

- address: cosmos1u7209hpnrajperpznlsy9zmdvr3jx2npfu7w4u
  name: student
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"Anu7Dkoa51eJK7tj65KdzfZ9Cn9lq6RqFxG7B85cdQOn"}'
  type: local

We have created a wallet for the student. In this stage the wallet has 0 balance and isnt known by the blockchain, lets send him some tokens

### Sending and Receiving tokens on our Blockchain





  
Genesis JSON_2
   ```
      {
 "moniker": "demo",
 "chain_id": "test-chain-tgFWQe",
 "node_id": "eee5fe21000bcbfd270e34d19f227be66cfa5084",
 "gentxs_dir": "/root/.simapp/config/gentx",
 "app_message": {
  "auth": {
   "params": {
    "max_memo_characters": "256",
    "tx_sig_limit": "7",
    "tx_size_cost_per_byte": "10",
    "sig_verify_cost_ed25519": "590",
    "sig_verify_cost_secp256k1": "1000"
   },
   "accounts": [
    {
     "@type": "/cosmos.auth.v1beta1.BaseAccount",
     "address": "cosmos15n5glgs7n8shcptapfte6klvcwpwz3qc20t4e2",
     "pub_key": null,
     "account_number": "0",
     "sequence": "0"
    }
   ]
  },
  "authz": {
   "authorization": []
  },
  "bank": {
   "params": {
    "send_enabled": [],
    "default_send_enabled": true
   },
   "balances": [
    {
     "address": "cosmos15n5glgs7n8shcptapfte6klvcwpwz3qc20t4e2",
     "coins": [
      {
       "denom": "stake",
       "amount": "100000000"
      }
     ]
    }
   ],
   "supply": [
    {
     "denom": "stake",
     "amount": "100000000"
    }
   ],
   "denom_metadata": [],
   "send_enabled": []
  },
  "circuit": {
   "account_permissions": [],
   "disabled_type_urls": []
  },
  "consensus": {},
  "distribution": {
   "params": {
    "community_tax": "0.020000000000000000",
    "base_proposer_reward": "0.000000000000000000",
    "bonus_proposer_reward": "0.000000000000000000",
    "withdraw_addr_enabled": true
   },
   "fee_pool": {
    "community_pool": [],
    "decimal_pool": []
   },
   "delegator_withdraw_infos": [],
   "previous_proposer": "",
   "outstanding_rewards": [],
   "validator_accumulated_commissions": [],
   "validator_historical_rewards": [],
   "validator_current_rewards": [],
   "delegator_starting_infos": [],
   "validator_slash_events": []
  },
  "evidence": {
   "evidence": []
  },
  "feegrant": {
   "allowances": []
  },
  "genutil": {
   "gen_txs": [
    {
     "body": {
      "messages": [
       {
        "@type": "/cosmos.staking.v1beta1.MsgCreateValidator",
        "description": {
         "moniker": "demo"
        },
        "commission": {
         "rate": "100000000000000000",
         "max_rate": "200000000000000000",
         "max_change_rate": "10000000000000000"
        },
        "min_self_delegation": "1",
        "validator_address": "cosmosvaloper15n5glgs7n8shcptapfte6klvcwpwz3qc0mlq4e",
        "pubkey": {
         "@type": "/cosmos.crypto.ed25519.PubKey",
         "key": "7GfKExkRy0rm1wxHL+PK1qA2YNzAXz+d7VZbq1MF4ig="
        },
        "value": {
         "denom": "stake",
         "amount": "70000000"
        }
       }
      ],
      "memo": "eee5fe21000bcbfd270e34d19f227be66cfa5084@65.109.61.123:26656"
     },
     "auth_info": {
      "signer_infos": [
       {
        "public_key": {
         "@type": "/cosmos.crypto.secp256k1.PubKey",
         "key": "Ah+vpcVHqLpwbBAzKqGfeFPtucu5c1HZRW8gYHxGAhY+"
        },
        "mode_info": {
         "single": {
          "mode": "SIGN_MODE_DIRECT"
         }
        }
       }
      ],
      "fee": {
       "gas_limit": "200000",
       "payer": "cosmos15n5glgs7n8shcptapfte6klvcwpwz3qc20t4e2"
      }
     },
     "signatures": [
      "kBxQgw1PSfBiHufAZB//2KVMwgcUO+ah/dcsKLNcHEIzChl7ZuYSXvSlBjYe6B5wBUbptpgggWy2JBbZmB7bzQ=="
     ]
    }
   ]
  },
  "gov": {
   "starting_proposal_id": "1",
   "deposits": [],
   "votes": [],
   "proposals": [],
   "deposit_params": null,
   "voting_params": null,
   "tally_params": null,
   "params": {
    "min_deposit": [
     {
      "denom": "stake",
      "amount": "10000000"
     }
    ],
    "max_deposit_period": "172800s",
    "voting_period": "172800s",
    "quorum": "0.334000000000000000",
    "threshold": "0.500000000000000000",
    "veto_threshold": "0.334000000000000000",
    "min_initial_deposit_ratio": "0.000000000000000000",
    "proposal_cancel_ratio": "0.500000000000000000",
    "proposal_cancel_dest": "",
    "expedited_voting_period": "86400s",
    "expedited_threshold": "0.667000000000000000",
    "expedited_min_deposit": [
     {
      "denom": "stake",
      "amount": "50000000"
     }
    ],
    "burn_vote_quorum": false,
    "burn_proposal_deposit_prevote": false,
    "burn_vote_veto": true,
    "min_deposit_ratio": "0.010000000000000000",
    "proposal_cancel_max_period": "0.500000000000000000",
    "optimistic_authorized_addresses": [],
    "optimistic_rejected_threshold": "0.100000000000000000",
    "yes_quorum": "0.000000000000000000",
    "expedited_quorum": "0.500000000000000000"
   },
   "constitution": ""
  },
  "group": {
   "group_seq": "0",
   "groups": [],
   "group_members": [],
   "group_policy_seq": "0",
   "group_policies": [],
   "proposal_seq": "0",
   "proposals": [],
   "votes": []
  },
  "mint": {
   "minter": {
    "inflation": "0.130000000000000000",
    "annual_provisions": "0.000000000000000000"
   },
   "params": {
    "mint_denom": "stake",
    "inflation_rate_change": "0.130000000000000000",
    "inflation_max": "0.200000000000000000",
    "inflation_min": "0.070000000000000000",
    "goal_bonded": "0.670000000000000000",
    "blocks_per_year": "6311520"
   }
  },
  "nft": {
   "classes": [],
   "entries": []
  },
  "protocolpool": {
   "continuous_fund": [],
   "budget": [],
   "to_distribute": "0"
  },
  "runtime": {},
  "slashing": {
   "params": {
    "signed_blocks_window": "100",
    "min_signed_per_window": "0.500000000000000000",
    "downtime_jail_duration": "600s",
    "slash_fraction_double_sign": "0.050000000000000000",
    "slash_fraction_downtime": "0.010000000000000000"
   },
   "signing_infos": [],
   "missed_blocks": []
  },
  "staking": {
   "params": {
    "unbonding_time": "1814400s",
    "max_validators": 100,
    "max_entries": 7,
    "historical_entries": 10000,
    "bond_denom": "stake",
    "min_commission_rate": "0.000000000000000000",
    "key_rotation_fee": {
     "denom": "stake",
     "amount": "1000000"
    }
   },
   "last_total_power": "0",
   "last_validator_powers": [],
   "validators": [],
   "delegations": [],
   "unbonding_delegations": [],
   "redelegations": [],
   "exported": false
  },
  "upgrade": {},
  "vesting": {}
 }
}
   ```
JSON1
   ```
   
   {
      "moniker": "demo",
      "chain_id": "test-chain-tgFWQe",
      "node_id": "eee5fe21000bcbfd270e34d19f227be66cfa5084",
      "gentxs_dir": "",
      "app_message": {
       "auth": {
        "params": {
         "max_memo_characters": "256",
         "tx_sig_limit": "7",
         "tx_size_cost_per_byte": "10",
         "sig_verify_cost_ed25519": "590",
         "sig_verify_cost_secp256k1": "1000"
        },
        "accounts": []
       },
       "authz": {
        "authorization": []
       },
       "bank": {
        "params": {
         "send_enabled": [],
         "default_send_enabled": true
        },
        "balances": [],
        "supply": [],
        "denom_metadata": [],
        "send_enabled": []
       },
       "circuit": {
        "account_permissions": [],
        "disabled_type_urls": []
       },
       "consensus": {},
       "distribution": {
        "params": {
         "community_tax": "0.020000000000000000",
         "base_proposer_reward": "0.000000000000000000",
         "bonus_proposer_reward": "0.000000000000000000",
         "withdraw_addr_enabled": true
        },
        "fee_pool": {
         "community_pool": [],
         "decimal_pool": []
        },
        "delegator_withdraw_infos": [],
        "previous_proposer": "",
        "outstanding_rewards": [],
        "validator_accumulated_commissions": [],
        "validator_historical_rewards": [],
        "validator_current_rewards": [],
        "delegator_starting_infos": [],
        "validator_slash_events": []
       },
       "evidence": {
        "evidence": []
       },
       "feegrant": {
        "allowances": []
       },
       "genutil": {
        "gen_txs": []
       },
       "gov": {
        "starting_proposal_id": "1",
        "deposits": [],
        "votes": [],
        "proposals": [],
        "deposit_params": null,
        "voting_params": null,
        "tally_params": null,
        "params": {
         "min_deposit": [
          {
           "denom": "stake",
           "amount": "10000000"
          }
         ],
         "max_deposit_period": "172800s",
         "voting_period": "172800s",
         "quorum": "0.334000000000000000",
         "threshold": "0.500000000000000000",
         "veto_threshold": "0.334000000000000000",
         "min_initial_deposit_ratio": "0.000000000000000000",
         "proposal_cancel_ratio": "0.500000000000000000",
         "proposal_cancel_dest": "",
         "expedited_voting_period": "86400s",
         "expedited_threshold": "0.667000000000000000",
         "expedited_min_deposit": [
          {
           "denom": "stake",
           "amount": "50000000"
          }
         ],
         "burn_vote_quorum": false,
         "burn_proposal_deposit_prevote": false,
         "burn_vote_veto": true,
         "min_deposit_ratio": "0.010000000000000000",
         "proposal_cancel_max_period": "0.500000000000000000",
         "optimistic_authorized_addresses": [],
         "optimistic_rejected_threshold": "0.100000000000000000",
         "yes_quorum": "0.000000000000000000",
         "expedited_quorum": "0.500000000000000000"
        },
        "constitution": ""
       },
       "group": {
        "group_seq": "0",
        "groups": [],
        "group_members": [],
        "group_policy_seq": "0",
        "group_policies": [],
        "proposal_seq": "0",
        "proposals": [],
        "votes": []
       },
       "mint": {
        "minter": {
         "inflation": "0.130000000000000000",
         "annual_provisions": "0.000000000000000000"
        },
        "params": {
         "mint_denom": "stake",
         "inflation_rate_change": "0.130000000000000000",
         "inflation_max": "0.200000000000000000",
         "inflation_min": "0.070000000000000000",
         "goal_bonded": "0.670000000000000000",
         "blocks_per_year": "6311520"
        }
       },
       "nft": {
        "classes": [],
        "entries": []
       },
       "protocolpool": {
        "continuous_fund": [],
        "budget": [],
        "to_distribute": "0"
       },
       "runtime": {},
       "slashing": {
        "params": {
         "signed_blocks_window": "100",
         "min_signed_per_window": "0.500000000000000000",
         "downtime_jail_duration": "600s",
         "slash_fraction_double_sign": "0.050000000000000000",
         "slash_fraction_downtime": "0.010000000000000000"
        },
        "signing_infos": [],
        "missed_blocks": []
       },
       "staking": {
        "params": {
         "unbonding_time": "1814400s",
         "max_validators": 100,
         "max_entries": 7,
         "historical_entries": 10000,
         "bond_denom": "stake",
         "min_commission_rate": "0.000000000000000000",
         "key_rotation_fee": {
          "denom": "stake",
          "amount": "1000000"
         }
        },
        "last_total_power": "0",
        "last_validator_powers": [],
        "validators": [],
        "delegations": [],
        "unbonding_delegations": [],
        "redelegations": [],
        "exported": false
       },
       "upgrade": {},
       "vesting": {}
      }
     }
```
