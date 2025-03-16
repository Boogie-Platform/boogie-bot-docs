# Boogie Bot API Documentation

This document provides detailed information about the available API endpoints for the Boogie Bot platform.

## Table of Contents

- [Authentication API](#authentication-api)
  - [Sign Up](#sign-up)
  - [Sign In](#sign-in)
  - [Get Profile](#get-profile)
  - [Update Profile](#update-profile)
- [Wallet API](#wallet-api)
  - [List Wallets](#list-wallets)
  - [Get Wallet](#get-wallet)
  - [Withdraw](#withdraw)
  - [Export Wallet](#export-wallet)
- [Trade API](#trade-api)
  - [Buy Token](#buy-token)
  - [Sell Token](#sell-token)
  - [Get Positions](#get-positions)
  - [Get Position by ID](#get-position-by-id)
- [Token API](#token-api)
  - [Get Token Info](#get-token-info)
- [Settings API](#settings-api)
  - [Get All Settings](#get-all-settings)
  - [Get Chain Settings](#get-chain-settings)
  - [Update Slippage](#update-slippage)
  - [Update Priority Fee](#update-priority-fee)
  - [Update Auto Sell](#update-auto-sell)

## Authentication API

The Authentication API provides endpoints for user registration, authentication, and profile management.

Base URL: `/api/auth`

### Sign Up

Creates a new user account.

- **URL**: `/api/auth/signup`
- **Method**: `POST`
- **Authentication**: None (Public)
- **Request Body**:
  ```json
  {
    "name": "string",
    "email": "string"
  }
  ```
- **Response**:
  ```json
  {
    "access_token": "string",
    "user": {
      "_id": "string",
      "name": "string",
      "email": "string"
    }
  }
  ```

### Sign In

Authenticates a user and returns a JWT token.

- **URL**: `/api/auth/signin`
- **Method**: `POST`
- **Authentication**: None (Public)
- **Request Body**:
  ```json
  {
    "email": "string"
  }
  ```
- **Response**:
  ```json
  {
    "access_token": "string",
    "user": {
      "_id": "string",
      "name": "string",
      "email": "string"
    }
  }
  ```

### Get Profile

Retrieves the profile information of the authenticated user.

- **URL**: `/api/auth/profile`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Response**: 
  ```json
  {
    "_id": "string",
    "name": "string",
    "email": "string"
  }
  ```

### Update Profile

Updates the profile information of the authenticated user.

- **URL**: `/api/auth/profile`
- **Method**: `PUT`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "name": "string"
  }
  ```
- **Response**:
  ```json
  {
    "user": {
      "_id": "string",
      "name": "string",
      "email": "string"
    }
  }
  ```

## Wallet API

The Wallet API provides endpoints for managing cryptocurrency wallets, checking balances, and performing transactions.

Base URL: `/api/wallet`

### List Wallets

Retrieves all wallets associated with the authenticated user.

- **URL**: `/api/wallet/`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Response**:
  ```json
  [
    {
        "address": "0x998838a9e953Cf3A14D92203C631315dFD8C31E8",
        "balance": null,
        "chain": {
            "id": 1,
            "code": "ethereum",
            "name": "Ethereum",
            "currency": "ETH"
        }
    },
    {
        "address": "0x60D164400cfbaA2716b8202D6D854fe7bb4211aa",
        "balance": null,
        "chain": {
            "id": 56,
            "code": "bsc",
            "name": "Binance",
            "currency": "BNB"
        }
    },
    {
        "address": "0x235bd419cCbf322A96870212D07A7c6F7d40f32e",
        "balance": null,
        "chain": {
            "id": 137,
            "code": "polygon",
            "name": "Polygon",
            "currency": "MATIC"
        }
    },
    {
        "address": "0x6332EbEADE6f0cB564E4CedbB7De8936549B43BB",
        "balance": null,
        "chain": {
            "id": 42161,
            "code": "arbitrum",
            "name": "Arbitrum",
            "currency": "ETH"
        }
    },
    {
        "address": "TTqT7vNWRPrBaLerG97AiAuQ4bmWMGC5ms",
        "balance": null,
        "chain": {
            "id": 728126428,
            "code": "tron",
            "name": "Tron",
            "currency": "TRX"
        }
    },
    {
        "address": "0x426CB7823C78af35d6fe58566CC8bf771557201B",
        "balance": null,
        "chain": {
            "id": 8453,
            "code": "base",
            "name": "Base",
            "currency": "ETH"
        }
    },
    {
        "address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
        "balance": "0.004985",
        "chain": {
            "id": 900,
            "code": "solana",
            "name": "Solana",
            "currency": "SOL"
        }
    }
  ]
  ```

### Get Wallet

Retrieves a specific wallet by address for the authenticated user.

- **URL**: `/api/wallet/:address`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Parameters**:
  - `address`: The wallet address to retrieve
- **Response**:
  ```json
  {
    "address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
    "balance": "0.004985",
    "chain": {
        "id": 900,
        "code": "solana",
        "name": "Solana",
        "currency": "SOL"
    }
  }
  ```

### Withdraw

Initiates a withdrawal from the user's wallet to a specified address.

- **URL**: `/api/wallet/withdraw`
- **Method**: `POST`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "to_address": "JD1BnehcihCuKFrZ83mgoSwhuZz1Bh8tDLSTDm9MPYcN",
    "amount": 0.005,
    "chain_code": "solana"
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "signature": "282rGuojRtzE8uT4fM7iz8yTfM4TbG3DPmyLNow9dn9bssfSD4LDBTxGmBvtDemakqhkf2HwwYYTdfgW3W7iwNmS",
    "amount": "0.005",
    "from_address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
    "to_address": "JD1BnehcihCuKFrZ83mgoSwhuZz1Bh8tDLSTDm9MPYcN",
    "explorer_url": "https://solscan.io/tx/282rGuojRtzE8uT4fM7iz8yTfM4TbG3DPmyLNow9dn9bssfSD4LDBTxGmBvtDemakqhkf2HwwYYTdfgW3W7iwNmS/"
  }
  ```
- **Error Responses**:
  - `400 Bad Request`: Returned when there are insufficient funds or other validation errors
  - `401 Unauthorized`: Returned when the user is not authenticated

### Export Wallet

Exports the user's wallet including private key and mnemonic phrase.

- **URL**: `/api/wallet/export`
- **Method**: `POST`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu"
  }
  ```
- **Response**:
  ```json
  {
    "address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
    "private_key": "585917e163f375877959e6389e9f1f176a957b373a32cd1133dbf38483f18069eb571148e365d508b265c6e95f1fab10a6d7e37efd07e9441f0b81407b0a31b6",
    "mnemonic_phrase": "execute spare tape tennis chief boring keen include any misery helmet tail",
    "chain": {
        "id": 900,
        "code": "solana",
        "name": "Solana",
        "currency": "SOL"
    }
  }
  ```

## Trade API

The Trade API provides endpoints for executing trades, managing positions, and tracking performance.

Base URL: `/api/trade`

### Buy Token

Initiates a token purchase transaction.

- **URL**: `/api/trade/buy`
- **Method**: `POST`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "address": "HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump",
    "amount": 0.002,
    "chain_code": "solana"
  }
  ```
- **Response**: 
  ```json
  {
    "success": true,
    "transaction": "33upMkF2jQTPjcNVk9vUSriPEsjPvy1bukpkqj18Br7oeWZvd4zsb7zB9SxLr7xWkbacxznpyJXPkhu5Cqmtewww",
    "txLink": "https://explorer.solana.com/tx/33upMkF2jQTPjcNVk9vUSriPEsjPvy1bukpkqj18Br7oeWZvd4zsb7zB9SxLr7xWkbacxznpyJXPkhu5Cqmtewww"
  }
  ```

### Sell Token

Initiates a token sell transaction.

- **URL**: `/api/trade/sell`
- **Method**: `POST`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "address": "HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump",
    "amount": 107741.461161,
    "chain_code": "solana"
  }
  ```
- **Response**: 
  ```json
  {
    "success": true,
    "transaction": "2JWEoKqXqremXzAbZzNTuEpgGUk4ZVQYYMQjMZ8kuaMXr2FrzgK3VPRM959jvFMQjVysCbQiouLYJEJmapY7cBAS",
    "txLink": "https://explorer.solana.com/tx/2JWEoKqXqremXzAbZzNTuEpgGUk4ZVQYYMQjMZ8kuaMXr2FrzgK3VPRM959jvFMQjVysCbQiouLYJEJmapY7cBAS"
  }
  ```

### Get Positions

Retrieves all trading positions for the authenticated user.

- **URL**: `/api/trade/positions`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Response**:
  ```json
  [
    {
      "chainId": "solana",
      "pairAddress": "5VnERYyP8sMDjc7kQiseQG149WqN68n3rFZz5qTSNqQf",
      "baseToken": {
        "address": "HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump",
        "name": "Elon Marsk",
        "symbol": "ELONM"
      },
      "quoteToken": {
        "address": "So11111111111111111111111111111111111111112",
        "name": "Wrapped SOL",
        "symbol": "SOL"
      },
      "netAmount": 107741.461161,
      "totalBought": 107741.461161,
      "totalSold": 0,
      "countSwap": 1,
      "countBuy": 1,
      "countSell": 0,
      "realizedPnL": 0,
      "unrealizedPnL": 0,
      "realizedPnLPercentage": 0,
      "unrealizedPnLPercentage": 0,
      "averageBuyPrice": 1.8562955973015477e-8,
      "currentPrice": 1.8562955973015477e-8
    }
  ]
  ```

### Get Position by ID

Retrieves a specific trading position by ID.

- **URL**: `/api/trade/positions/:id`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Parameters**:
  - `id`: The position ID to retrieve (format: `{chain_code}-{token_address}`)
- **Response**:
  ```json
  {
    "chain_id": "solana",
    "pair_address": "5VnERYyP8sMDjc7kQiseQG149WqN68n3rFZz5qTSNqQf",
    "base_token": {
        "address": "HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump",
        "name": "Elon Marsk",
        "symbol": "ELONM"
    },
    "quote_token": {
        "address": "So11111111111111111111111111111111111111112",
        "name": "Wrapped SOL",
        "symbol": "SOL"
    },
    "net_amount": 0,
    "total_bought": 107741.461161,
    "total_sold": 107741.461161,
    "count_swap": 2,
    "count_buy": 1,
    "count_sell": 1,
    "realized_pnl": -4.000000000002137e-7,
    "unrealized_pnl": 0,
    "realized_pnl_percentage": -4.000000000002137e-7,
    "unrealized_pnl_percentage": 0,
    "average_buy_price": 1.8562955973015477e-8,
    "current_price": 2.2443224656187884e-8
  }
  ```

## Token API

The Token API provides endpoints for retrieving token information.

Base URL: `/api/token`

### Get Token Info

Retrieves information about a specific token.

- **URL**: `/api/token/:address`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Parameters**:
  - `address`: The token address to retrieve
- **Query Parameters**:
  - `chain_code`: The blockchain code (e.g., "solana", "ethereum")
- **Response**:
  ```json
  {
    "chainId": "solana",
    "dexId": "raydium",
    "url": "https://dexscreener.com/solana/5vneryyp8smdjc7kqiseqg149wqn68n3rfzz5qtsnqqf",
    "pairAddress": "5VnERYyP8sMDjc7kQiseQG149WqN68n3rFZz5qTSNqQf",
    "labels": [
        "CLMM"
    ],
    "baseToken": {
        "address": "HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump",
        "name": "Elon Marsk",
        "symbol": "ELONM"
    },
    "quoteToken": {
        "address": "So11111111111111111111111111111111111111112",
        "name": "Wrapped SOL",
        "symbol": "SOL"
    },
    "priceNative": "0.00000001850",
    "priceUsd": "0.000002506",
    "txns": {
        "m5": {
            "buys": 1,
            "sells": 0
        },
        "h1": {
            "buys": 4,
            "sells": 5
        },
        "h6": {
            "buys": 31,
            "sells": 31
        },
        "h24": {
            "buys": 322,
            "sells": 371
        }
    },
    "volume": {
        "h24": 3537.81,
        "h6": 157.93,
        "h1": 28.62,
        "m5": 1.35
    },
    "priceChange": {
        "m5": 3.04,
        "h1": -31.35,
        "h6": -57.99,
        "h24": -78.99
    },
    "liquidity": {
        "usd": 166.33,
        "base": 38438393,
        "quote": 0.5166
    },
    "fdv": 2507,
    "marketCap": 2507,
    "pairCreatedAt": 1741884031000,
    "info": {
        "imageUrl": "https://dd.dexscreener.com/ds-data/tokens/solana/HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump.png?key=505160",
        "header": "https://dd.dexscreener.com/ds-data/tokens/solana/HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump/header.png?key=505160",
        "openGraph": "https://cdn.dexscreener.com/token-images/og/solana/HsKDKwGhR9wKh62CUHmUUXmb2jBwoFkfsbCUKtCppump?timestamp=1742077200000",
        "websites": [
            {
                "label": "Website",
                "url": "https://elonmarsk.link/"
            }
        ],
        "socials": [
            {
                "type": "twitter",
                "url": "https://twitter.com/E_Marsk_Sol"
            },
            {
                "type": "telegram",
                "url": "https://t.me/Elon_Marsk_Solana"
            }
        ]
    }
  }
  ```

## Settings API

The Settings API provides endpoints for managing user preferences and trading settings.

Base URL: `/api/settings`

### Get All Settings

Retrieves all settings for the authenticated user across all chains.

- **URL**: `/api/settings`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Response**:
  ```json
  [
    {
      "chain_id": 900,
      "chain_code": "solana",
      "address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
      "slippage": {
        "buy": 0.05,
        "sell": 0.05
      },
      "priority_fee": {
        "buy": 5000000,
        "sell": 5000000
      },
      "auto_sell": {
        "take_profit": {
          "price_percentage": 0.4,
          "amount_percentage": 0.85
        },
        "stop_loss": {
          "price_percentage": 0.4,
          "amount_percentage": 0.85
        }
      }
    },
    {
      "chain_id": 1,
      "chain_code": "ethereum",
      "address": "0x998838a9e953Cf3A14D92203C631315dFD8C31E8",
      "slippage": {
        "buy": 0.05,
        "sell": 0.05
      },
      "priority_fee": {
        "buy": 100000,
        "sell": 100000
      },
      "auto_sell": {
        "take_profit": {
          "price_percentage": 0.2,
          "amount_percentage": 1
        },
        "stop_loss": {
          "price_percentage": 0.2,
          "amount_percentage": 1
        }
      }
    }
  ]
  ```

### Get Chain Settings

Retrieves settings for a specific blockchain.

- **URL**: `/api/settings/:chainCode`
- **Method**: `GET`
- **Authentication**: JWT Auth (Bearer Token)
- **Parameters**:
  - `chainCode`: The blockchain code (e.g., "SOL", "ETH")
- **Response**:
  ```json
  {
    "chain_id": 900,
    "chain_code": "solana",
    "address": "Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
    "slippage": {
      "buy": 0.05,
      "sell": 0.05
    },
    "priority_fee": {
      "buy": 5000000,
      "sell": 5000000
    },
    "auto_sell": {
      "take_profit": {
        "price_percentage": 0.4,
        "amount_percentage": 0.85
      },
      "stop_loss": {
        "price_percentage": 0.4,
        "amount_percentage": 0.85
      }
    }
  }
  ```

### Update Slippage

Updates the slippage tolerance setting for trades.

- **URL**: `/api/settings/slippage`
- **Method**: `PUT`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "chain_code": "solana",
    "direction": "buy",
    "value": 5
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "message": "Slippage updated successfully",
    "direction": "buy",
    "value": 5
  }
  ```

### Update Priority Fee

Updates the priority fee setting for transactions.

- **URL**: `/api/settings/priority-fee`
- **Method**: `PUT`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "chain_code": "solana",
    "direction": "buy",
    "value": 0.005
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "message": "Priority fee updated successfully",
    "direction": "buy",
    "value": 0.005
  }
  ```

### Update Auto Sell

Updates the auto-sell configuration for trades.

- **URL**: `/api/settings/auto-sell`
- **Method**: `PUT`
- **Authentication**: JWT Auth (Bearer Token)
- **Request Body**:
  ```json
  {
    "chain_code": "solana",
    "type": "take_profit",
    "price_percentage": 0.4,
    "amount_percentage": 0.85
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "message": "Updated auto sell settings for account Gqfp6L1Vk44CRMJqCd3hsGPXajFpUXHge4zRh2RLTFAu",
    "type": "take_profit",
    "price_percentage": 40,
    "amount_percentage": 0.85
  }
  ```
