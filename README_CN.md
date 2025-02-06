<p> <a href="README.md"> English <a/> |  中文 </p>

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