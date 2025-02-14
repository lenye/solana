<p> English | <a href="README_CN.md"> 中文 <a/></p>

### Proposal: Monitor Solana pump.fun Platform Real-time Transaction Activity and Push Transaction Information in Real-time.

<details>

<summary>pump.fun Real-time Transaction Activity</summary>

Utilize high-performance Solana nodes to listen in real-time to transactions related to the pump.fun platform on the
Solana blockchain, parse the transaction data, extract buy/sell information, and then push the information in JSON
format to the user's Webhook URL.

* **Real-time Push:** Real-time push of buy/sell transaction information on the pump.fun platform.
* **New Token Monitoring:** Ability to automatically detect and monitor newly created tokens on pump.fun.
* **Data Format:** Push data in JSON format for easy parsing and use by users.
* **Security:** Provide Webhook signature verification to ensure data security and reliability.

**JSON Data Format**

* sol_amount (in lamports)
* price (in SOL)

#### create

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
        }
    ],
    "tx_hash": "2KH3bWHYsvzz8AJjkyMugGWgaAjGRVjjnfvGixV8PS5FbR7LobTWkx7SaVgpiDbS4x7GT5M7VxsAQjkXL2WjKSvq",
    "block_time": 1727058754,
    "slot": 291446204
}
```

#### buy

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

#### sell

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

# solana pump.fun token swap api

Get the real-time price of then token, token trading, use the following API endpoints:

* price: https://swap.nanhook.com/pumpfun/price
* buy: https://swap.nanhook.com/pumpfun/buy
* sell: https://swap.nanhook.com/pumpfun/sell

### Price

http request

```shell
curl -X 'GET' \
  'https://swap.nanhook.com/pumpfun/price?mint=Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump' \
  -H 'accept: application/json'
```

http response

```json
{
    "SOL": "0.0000000282"
}
```

### Buy

amount: 1000000000 lamports => 1 SOL

slippage: 6 => 6%

http request

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

http response

```json
{
    "tx_hash": "4KyWfG9w4kPjKWP6KBBTgcqCtaKBzgqS1WvSSF5KvfmJPN5Kh9WsaZrX7kigrHe7v8xcMyujdZCEwRdmigyL5WJ9",
    "associated_token_account": "795dYUac4c7J7uQZ1TdTfZYsTx2Xhutpbsy21on9oWWi"
}
```

### Sell

amount: 10412144167202 => 10412144.167202 mint

slippage: 6 => 6%

http request

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

http response

```json
{
    "tx_hash": "67NrDWQ87tc4Bgjox7RN4QnjyVqEWzv9ziQq2nFeELdGCVKe6oaFvASCSH112kwgXUxqRNANeb4RhAQP5fG4mtDy",
    "associated_token_account": "J1jvePNYHbe5QHAQoaohTVWfojHo1Qiqac73uUwvd3fo"
}
```

### Associated Token Account

https://solana.com/docs/core/tokens#associated-token-account

Associated Token Account as the "default" token account for a specific mint and owner.

### Swagger UI

https://swap.nanhook.com/swagger/

This is not the official pump.fun API.
Using our API can help you create your own pump.fun trading robots and tools.
You can use the API for free, with rate limits for each endpoint.
