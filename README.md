<p> English | <a href="README_CN.md"> 中文 <a/></p>

### Monitor Solana blockchain pump.fun real-time transaction activity with Webhook-based real-time transaction information push.

https://github.com/lenye/pumpfun_tracker

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
