<p> <a href="README.md"> English <a/> |  中文 </p>

### 提案：监控 Solana 区块链 pump.fun 平台实时交易动向，实时推送交易信息。

<details>

<summary>pump.fun 实时交易动向</summary>

使用高性能的 Solana 节点，实时监听 Solana 区块链上与 pump.fun 平台相关的交易，并解析交易数据，提取买入/卖出信息，然后以 JSON
格式推送到用户的 Webhook URL。

* **实时推送:** 实时推送 pump.fun 平台上的买入/卖出交易信息。
* **新代币监控:** 能够自动检测和监控 pump.fun 上新创建的代币。
* **数据格式:** 以 JSON 格式推送数据，方便用户解析和使用。
* **安全性:** 提供 Webhook 签名验证，确保数据安全可靠。

**JSON 数据格式**

```text
sol_amount   单位为 lamports
price        单位为 SOL
```

#### 新创建代币, 买入代币

```json
{
    "market": "pump.fun",
    "instructions": [
        {
            "action": "create",
            "accounts": {
                "mint": "Kz2MfJf6ZNChZLK7Wofzma5BsnnebnPPZwN775sirCE",
                "bonding_curve": "31PV2wqSYVBp9NtjRQRnpUjJAuaBqbwY9oDqBtkj4ciV",
                "associated_bonding_curve": "DxFdVu8H4VuU9J3D2HKBShxt76bN9ns6BwqGGHuoXz1j",
                "user": "8wZiLEMF7sV6q4JbFyFNTyaBDPm5LXToKiE1n6moqDV5"
            },
            "data": {
                "name": "BENI",
                "symbol": "beni",
                "uri": "https://ipfs.io/ipfs/bafkreigegxjfgfb25vx64awsylnxc2rckbt4c766pg2ubpirj24otbcqjy"
            }
        },
        {
            "action": "buy",
            "accounts": {
                "mint": "Kz2MfJf6ZNChZLK7Wofzma5BsnnebnPPZwN775sirCE",
                "bonding_curve": "31PV2wqSYVBp9NtjRQRnpUjJAuaBqbwY9oDqBtkj4ciV",
                "associated_bonding_curve": "DxFdVu8H4VuU9J3D2HKBShxt76bN9ns6BwqGGHuoXz1j",
                "associated_user": "3mtehqFoc7EFtwEJH2XFaui21jQmKEPiRKkns7nFqB69",
                "user": "8wZiLEMF7sV6q4JbFyFNTyaBDPm5LXToKiE1n6moqDV5"
            },
            "data": {
                "sol_amount": 5108912872,
                "token_amount": 156138799597360,
                "timestamp": 1727058754,
                "price": "0.0000000383"
            }
        }
    ],
    "tx_hash": "2KH3bWHYsvzz8AJjkyMugGWgaAjGRVjjnfvGixV8PS5FbR7LobTWkx7SaVgpiDbS4x7GT5M7VxsAQjkXL2WjKSvq",
    "block_time": 1727058754,
    "slot": 291446204
}
```

### 买入代币

```json
{
    "market": "pump.fun",
    "instructions": [
        {
            "action": "buy",
            "accounts": {
                "mint": "FV1U42g3mvtKhWZgKf3s76sLTcXm1bGHTEwiAVHtpump",
                "bonding_curve": "Bzp9zS9KoQDRYTie7QmYZBGhQDN4ChDeGpNce9mn296g",
                "associated_bonding_curve": "J3Wmp7WSkeBAAaJhwJBTiGGWh2CB1b9FTYX1PUEzbLQA",
                "associated_user": "Fusy5dSHJwDjVnSp3mx9eRruWEME4RcQ8QhRs94F6XSs",
                "user": "devoM3KtGhwBbwHz8TQPaKRyRxMPp6t4j6pVMJepHFn"
            },
            "data": {
                "sol_amount": 361379303,
                "token_amount": 9479553659186,
                "timestamp": 1737732751,
                "price": "0.0000000385"
            }
        }
    ],
    "tx_hash": "4f35TmwfzGzfLFrEu8RukLA5ButTytEeZ5WcXkWkSpvCFDmVdJXCWjJrF91jXr7EvqzXkMPiHxhA3hRnqD7hFpm8",
    "block_time": 1737732751,
    "slot": 316088340
}
```

### 卖出代币

```json
{
    "market": "pump.fun",
    "instructions": [
        {
            "action": "sell",
            "accounts": {
                "mint": "4HSvu2598JRFhyfqVi6kXcsb3Y3AXepzE1iBJhGupump",
                "bonding_curve": "HkNRxBLdDcSRbC6aMb7LmGb29s5ZRg4RbC9QU4E1vjk",
                "associated_bonding_curve": "8uuptDvgwTV6LBPTXx4mstFG87k3Ytc8ziHWzxch94kC",
                "associated_user": "4MXdXg4uQRTN8pmKtWGMms2BfQ8Dq7vZDJ86PauLcD3g",
                "user": "FAThSTn33fq5qGAA7LkZNJ3xu7rroe4JtvRuoZzdthN9"
            },
            "data": {
                "sol_amount": 21003473,
                "token_amount": 168469183892,
                "timestamp": 1726935585,
                "price": "0.0000001246"
            }
        }
    ],
    "tx_hash": "5PD2KbbsRy2WUNfjimKdSq9xvqBGtaDBWXoSWn8TPkmhj5TGBPuGkWUJnjovFECGhtXwemuChRTX1hie7zyDDQkr",
    "block_time": 1726935585,
    "slot": 291165075
}
```

</details>

# solana pump.fun 代币兑换 API

获取代币的实时价格，购买和出售代币，使用以下 API：

* 价格：https://swap.nanhook.com/pumpfun/price
* 购买：https://swap.nanhook.com/pumpfun/buy
* 出售：https://swap.nanhook.com/pumpfun/sell

### 价格

http 请求

```shell
curl -X 'GET' \
  'https://swap.nanhook.com/pumpfun/price?mint=Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump' \
  -H 'accept: application/json'
```

http 响应

```json
{
    "SOL": "0.0000000282"
}
```

### 购买

amount: 1000000000 lamports => 1 SOL

slippage: 6 => 6%

http 请求

```shell
curl -X 'POST' \
  'https://swap.nanhook.com/pumpfun/buy' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "private_key": "wallet private key",
  "mint": "Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump",
  "amount": 1000000000,
  "slippage": 6
}'
```

http 响应

```json
{
    "tx_hash": "4KyWfG9w4kPjKWP6KBBTgcqCtaKBzgqS1WvSSF5KvfmJPN5Kh9WsaZrX7kigrHe7v8xcMyujdZCEwRdmigyL5WJ9",
    "associated_token_account": "795dYUac4c7J7uQZ1TdTfZYsTx2Xhutpbsy21on9oWWi"
}
```

### 出售

amount: 10412144167202 => 10412144.167202 mint

slippage: 6 => 6%

http 请求

```shell
curl -X 'POST' \
  'https://swap.nanhook.com/pumpfun/sell' \
  -H 'accept: application/json' \
  -H 'Content-Type: application/json' \
  -d '{
  "private_key": "wallet private key",
  "mint": "Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump",
  "amount": 10412144167202,
  "slippage": 6
}'
```

http 响应

```json
{
    "tx_hash": "67NrDWQ87tc4Bgjox7RN4QnjyVqEWzv9ziQq2nFeELdGCVKe6oaFvASCSH112kwgXUxqRNANeb4RhAQP5fG4mtDy",
    "associated_token_account": "J1jvePNYHbe5QHAQoaohTVWfojHo1Qiqac73uUwvd3fo"
}
```

### Associated Token Account

https://solana.com/docs/core/tokens#associated-token-account

关联代币账户作为特定代币铸造账户和所有者的“默认”代币账户。

### Swagger 用户界面

https://swap.nanhook.com/swagger/

这不是官方的 pump.fun API。使用我们的 API 可以帮助您创建自己的 pump.fun 交易机器人和工具。您可以免费使用该 API，每个端点都有速率限制。