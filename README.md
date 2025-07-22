<p> English | <a href="README_CN.md"> 中文 <a/></p>

# pump.fun token price api

Get pump.fun real-time price from the Solana blockchain.

## 支持的操作系统

* Windows
* Linux
* macOS
* FreeBSD

## 上手指南

```shell
C:\>pumpfun_price.exe -h
Get pump.fun real-time price from the Solana blockchain

Usage:
  pumpfun_price [command]

Available Commands:
  api         Get the real-time price of then pump.fun token
  help        Help about any command
  rpc_version rpc node solana version

Flags:
  -h, --help              help for pumpfun_price
      --logfile           writing to a log file
  -l, --loglevel string   log level: debug, info, warn, error (default "error")
      --proxy string      proxy server, format: http://username:password@proxy_server_domain:port or socks5://username:password@proxy_server_ip:port
  -v, --version           version for pumpfun_price

Use "pumpfun_price [command] --help" for more information about a command.
```

### 安装`pumpfun_price`

`pumpfun_price`下载 [最新版本](https://github.com/lenye/solana/releases/tag/pumpfun_price_v25.7.0)

#### windows 操作系统

1. 解压下载文件`pumpfun_price_v25.7.0_windows_x86_64.zip`；
2. 运行`pumpfun_price.exe api`，开始 API 服务；

#### 完成

如果你顺利完成了以上步骤，那么恭喜你，属于你的`pumpfun_prices`搭建成功。

## 调用 API 获取 pump.fun token Price

* HTTP 方法: GET
* Endpoint: http://localhost:39270/pumpfun/price
* 数据格式: 请求和响应数据编码均为 UTF-8

### 请求参数

URL Query

| 参数名    | 类型     | 必填 | 描述             |
|:-------|:-------|:---|:---------------|
| `mint` | string | 是  | pump.fun token |

mint: The contract address of the token you want to trade (this is the text after the '/' in the pump.fun url for the
token.)

### 响应数据

API 服务器返回 `HTTP 200` 状态码, 表示查询成功。

| 字段名   | 类型     | 描述          |
|:------|:-------|:------------|
| `SOL` | string | token price |

API 服务器返回 `HTTP 4xx, 5xx` 状态码, 表示查询失败。

| 字段名       | 类型     | 描述   |
|:----------|:-------|:-----|
| `code`    | int    | 结果代码 |
| `message` | string | 结果描述 |

### Price

http request

```http
GET /pumpfun/price?token=Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump'
```

api server response

```http
content-type: application/json; charset=utf-8
 
{
    "SOL": "0.0000000282"
}
```

#### curl

```shell
curl -X 'GET' \
  'http://localhost:39270/pumpfun/price?mint=Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump'
```

### Monitor Solana blockchain pump.fun real-time transaction activity with Webhook-based real-time transaction information push.

https://github.com/lenye/pumpfun_tracker

### Swagger UI

https://swap.nanhook.com/swagger/

This is not the official pump.fun API.
Using our API can help you create your own pump.fun trading robots and tools.
You can use the API for free, with rate limits for each endpoint.

# Disclaimer

This project is for learning and research purposes only. Cryptocurrencies and trading involve risk, and you assume all
risks associated with using this software. We are not responsible for any losses incurred while using this software.