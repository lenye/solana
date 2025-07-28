# Pumpfun real-time price api

Get pump.fun real-time price from the Solana blockchain.

## Supported Operating Systems

* Windows
* Linux
* macOS
* FreeBSD

## Getting Started Guide

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

### Installing `pumpfun_price`

Download the [latest version](https://github.com/lenye/solana/releases/tag/pumpfun_price_v25.7.0)

#### Windows OS

1. Unzip the downloaded file `pumpfun_price_v25.7.0_windows_x86_64.zip`.
2. Run `pumpfun_price.exe api` to start the API service.

#### Completion

If you have successfully completed the steps above, congratulations! You have set up your own `pumpfun_price` instance.

## Calling the API to get pump.fun Token Price

* **HTTP Method**: GET
* **Endpoint**: http://localhost:39270/pumpfun/price
* **Data Format**: Both request and response data are UTF-8 encoded.

### Request Parameters

URL Query

| Parameter | Type   | Required | Description         |
|:----------|:-------|:---------|:--------------------|
| `mint`    | string | Yes      | The pump.fun token. |

mint: The contract address of the token you want to trade (this is the text after the '/' in the pump.fun url for the
token.)

### Response Data

#### Success Response

The API server returns an `HTTP 200` status code to indicate a successful query.

| Field Name | Type   | Description |
|:-----------|:-------|:------------|
| `SOL`      | string | token price |

#### Failure Response

The API server returns an `HTTP 4xx` or `5xx` status code to indicate a failed query.

| Field Name | Type   | Description        |
|:-----------|:-------|:-------------------|
| `code`     | int    | Result code        |
| `message`  | string | Result description |

### API

http request

```http
GET /pumpfun/price?token=Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump'
```

api server response

```http
HTTP/1.1 200 OK
content-type: application/json; charset=utf-8
 
{
    "SOL": "0.0000000282"
}
```

### Swagger UI

http://localhost:39270/swagger/

### curl

```shell
curl -X 'GET' \
  'http://localhost:39270/pumpfun/price?mint=Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump'
```

### Python

```python
import requests
import json

# Define the base URL for the API endpoint
BASE_URL = "http://localhost:39270/pumpfun/price"

def get_pumpfun_price(mint_address: str):
    """
    Calls the API to get the price for a specific pump.fun token.

    Args:
        mint_address: The contract address (mint) of the token to query.

    Returns:
        A dictionary containing the parsed JSON response, or None if an error occurred.
    """
    # Prepare the URL query parameters.
    # Note: The documentation table specifies the parameter as 'mint', 
    # while the example request uses 'token'. We will follow the table.
    params = {
        'mint': mint_address
    }

    print(f"[*] Querying for token: {mint_address}")

    try:
        # Send the GET request with a 10-second timeout
        response = requests.get(BASE_URL, params=params, timeout=10)

        # Check the HTTP status code to determine if the request was successful
        if response.status_code == 200:
            # Success Response (HTTP 200)
            data = response.json()
            price = data.get("SOL")
            print("✅ Query successful!")
            print(f"   └── Token Price (SOL): {price}")
            return data
        else:
            # Failure Response (HTTP 4xx or 5xx)
            print(f"❌ Query failed with HTTP status code: {response.status_code}")
            try:
                # Try to parse the error details from the JSON response
                error_data = response.json()
                code = error_data.get("code")
                message = error_data.get("message")
                print(f"   ├── Error Code: {code}")
                print(f"   └── Error Message: {message}")
                return error_data
            except json.JSONDecodeError:
                # If the response body isn't valid JSON, print the raw text
                print(f"   └── Could not parse JSON from response: {response.text}")
                return None

    except requests.exceptions.RequestException as e:
        # Handle network-level errors (e.g., connection refused, timeout)
        print(f"❌ A network error occurred: {e}")
        return None

# --- Main execution block to demonstrate usage ---
if __name__ == "__main__":
    # --- Scenario 1: Simulate a successful query ---
    # Using the token address from the documentation's example
    successful_token = "Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump"
    print("--- Scenario 1: Simulating a successful query ---")
    get_pumpfun_price(successful_token)

    print("\n" + "="*50 + "\n")

    # --- Scenario 2: Simulate a failed query ---
    # Using a deliberately invalid token address to trigger an API error
    failed_token = "this_is_not_a_valid_solana_address"
    print("--- Scenario 2: Simulating a failed query ---")
    get_pumpfun_price(failed_token)
```

### PHP

```php
<?php

/**
 * Calls the API to get the price for a specific pump.fun token.
 *
 * @param string $mintAddress The contract address (mint) of the token to query.
 * @return void This function prints its output directly.
 */
function getPumpFunPrice(string $mintAddress): void
{
    // Define the base URL for the API endpoint
    $baseUrl = 'http://localhost:39270/pumpfun/price';

    // Prepare the URL query parameters
    $params = ['mint' => $mintAddress];

    // Build the full URL with the query string
    // http_build_query() will correctly URL-encode the parameters
    $url = $baseUrl . '?' . http_build_query($params);

    echo "[*] Querying for token: {$mintAddress}\n";

    // 1. Initialize a cURL session
    $ch = curl_init();

    // 2. Set cURL options
    // Set the URL to fetch
    curl_setopt($ch, CURLOPT_URL, $url);
    // Return the response as a string instead of outputting it directly
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    // Set a timeout of 10 seconds for the request
    curl_setopt($ch, CURLOPT_TIMEOUT, 10);

    // 3. Execute the cURL request
    $responseBody = curl_exec($ch);
    // Get the HTTP status code from the response
    $httpStatusCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);

    // 4. Check for cURL-level errors (e.g., connection failed)
    if (curl_errno($ch)) {
        echo "❌ A cURL error occurred: " . curl_error($ch) . "\n";
        curl_close($ch);
        return;
    }

    // 5. Always close the cURL session
    curl_close($ch);

    // 6. Process the response based on the HTTP status code
    if ($httpStatusCode == 200) {
        // Success Response (HTTP 200)
        echo "✅ Query successful!\n";
        // Decode the JSON response into a PHP associative array
        $data = json_decode($responseBody, true);

        if (json_last_error() === JSON_ERROR_NONE && isset($data['SOL'])) {
            echo "   └── Token Price (SOL): " . $data['SOL'] . "\n";
        } else {
            echo "   └── Could not parse JSON from success response.\n";
        }
    } else {
        // Failure Response (HTTP 4xx or 5xx)
        echo "❌ Query failed with HTTP status code: {$httpStatusCode}\n";
        $errorData = json_decode($responseBody, true);

        if (json_last_error() === JSON_ERROR_NONE && isset($errorData['code'])) {
            echo "   ├── Error Code: " . $errorData['code'] . "\n";
            echo "   └── Error Message: " . $errorData['message'] . "\n";
        } else {
            // If the response body isn't valid JSON, print the raw text
            echo "   └── Could not parse JSON from error response: {$responseBody}\n";
        }
    }
}

// --- Main execution block to demonstrate usage ---

// --- Scenario 1: Simulate a successful query ---
// Using the token address from the documentation's example
$successful_token = "Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump";
echo "--- Scenario 1: Simulating a successful query ---\n";
getPumpFunPrice($successful_token);

echo "\n" . str_repeat("=", 50) . "\n\n";

// --- Scenario 2: Simulate a failed query ---
// Using a deliberately invalid token address to trigger an API error
$failed_token = "this_is_not_a_valid_solana_address";
echo "--- Scenario 2: Simulating a failed query ---\n";
getPumpFunPrice($failed_token);

?>
```

### JavaScript

```javascript
/**
 * Calls the API to get the price for a specific pump.fun token.
 *
 * @param {string} mintAddress The contract address (mint) of the token to query.
 * @returns {Promise<void>} This function logs its output directly to the console.
 */
async function getPumpFunPrice(mintAddress) {
  // Define the base URL for the API endpoint
  const baseUrl = 'http://localhost:39270/pumpfun/price';

  // Use URLSearchParams to safely build the query string.
  // This correctly handles encoding of special characters.
  const params = new URLSearchParams({ mint: mintAddress });
  const url = `${baseUrl}?${params.toString()}`;

  console.log(`[*] Querying for token: ${mintAddress}`);

  try {
    // 1. Send the GET request using fetch
    const response = await fetch(url, {
      signal: AbortSignal.timeout(10000) // 10-second timeout
    });

    // 2. Parse the JSON body. This works for both success and error responses.
    const data = await response.json();

    // 3. Check if the HTTP status code indicates success (200-299)
    if (response.ok) {
      // Success Response (HTTP 200)
      console.log("✅ Query successful!");
      console.log(`   └── Token Price (SOL): ${data.SOL}`);
    } else {
      // Failure Response (HTTP 4xx or 5xx)
      console.log(`❌ Query failed with HTTP status code: ${response.status}`);
      console.log(`   ├── Error Code: ${data.code}`);
      console.log(`   └── Error Message: ${data.message}`);
    }
  } catch (error) {
    // 4. Handle network-level errors or other exceptions
    if (error.name === 'TimeoutError') {
      console.log('❌ A network error occurred: The request timed out.');
    } else if (error instanceof SyntaxError) {
        console.log('❌ An error occurred: Failed to parse JSON from response.');
    }
     else {
      console.log(`❌ A network error occurred: ${error.message}`);
    }
  }
}

// --- Main execution block to demonstrate usage ---
// We wrap the calls in an async IIFE (Immediately Invoked Function Expression)
// to use await at the top level.
(async () => {
  // --- Scenario 1: Simulate a successful query ---
  // Using the token address from the documentation's example
  const successfulToken = "Di9zMoWNCppeMiNqVXoNYvWbisVYsdkkwvrSkreYpump";
  console.log("--- Scenario 1: Simulating a successful query ---");
  await getPumpFunPrice(successfulToken);

  console.log("\n" + "=".repeat(50) + "\n");

  // --- Scenario 2: Simulate a failed query ---
  // Using a deliberately invalid token address to trigger an API error
  const failedToken = "this_is_not_a_valid_solana_address";
  console.log("--- Scenario 2: Simulating a failed query ---");
  await getPumpFunPrice(failedToken);
})();
```

# Disclaimer

This project is for learning and research purposes only. Cryptocurrencies and trading involve risk, and you assume all
risks associated with using this software. We are not responsible for any losses incurred while using this software.