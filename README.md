OKX Quant Infrastructure

A C++17 quantitative trading infrastructure for OKX.

OKX Quant Infrastructure is a modular C++17 project designed to provide a foundation for building quantitative trading systems. It focuses on market data processing, order book management, pre-trade risk controls, rate limiting, and historical trade replay.

The project is structured to support future integration with OKX market data APIs and trading execution services.

Features

* L2 Order Book Management — Load order book snapshots and process incremental price-level updates.
* Pre-Trade Risk Engine — Validate order quantity, notional value, market data freshness, and estimated slippage.
* Slippage Estimation — Estimate market-order execution slippage using visible order book depth.
* Rate Limiting — Token bucket implementation for controlling request frequency.
* Market Data Replay — Replay historical trade records from JSON Lines files.
* Automated Testing — Unit tests covering core order book, risk engine, and rate limiter functionality.
* Continuous Integration — GitHub Actions workflow for automated CMake builds and tests.

Project Structure

okx-quant-infra/
├── .github/
│   └── workflows/
│       └── ci.yml
├── app/
│   └── replay_cli.cpp
├── examples/
│   └── trades.jsonl
├── include/
│   └── quant/
│       ├── order_book.hpp
│       ├── rate_limiter.hpp
│       ├── replay.hpp
│       ├── risk_engine.hpp
│       └── types.hpp
├── src/
│   ├── order_book.cpp
│   ├── rate_limiter.cpp
│   ├── replay.cpp
│   └── risk_engine.cpp
├── tests/
│   └── test_main.cpp
├── CMakeLists.txt
└── README.md

Requirements

* C++17 compatible compiler
* CMake 3.16 or later
* Git

Build

Clone the repository:

git clone https://github.com/sojiang75-byte/-jsn.git
cd -jsn

Configure the project:

cmake -S . -B build -DCMAKE_BUILD_TYPE=Release

Build:

cmake --build build --config Release

Run tests:

ctest --test-dir build --output-on-failure

Market Data Replay

The replay module reads trade records in JSON Lines format.

Example:

{"type":"trade","symbol":"BTC-USDT","price":65000.0,"size":0.01,"ts_ms":1730000000000}

Run the replay CLI:

./build/replay_cli examples/trades.jsonl

Risk Management

The current risk engine supports the following checks:

Risk Control	Description
Maximum Quantity	Limits individual order quantity
Maximum Notional	Limits order notional value
Maximum Slippage	Rejects orders exceeding configured slippage
Market Data Freshness	Rejects stale or future-dated order book data
Order Book Depth	Rejects orders when visible liquidity is insufficient

Risk limits can be configured through RiskConfig.

Development Roadmap

* [x]	C++17 project foundation
* [x]	L2 order book snapshot and update handling
* [x]	Pre-trade risk engine
* [x]	Slippage estimation
* [x]	Token bucket rate limiter
* [x]	JSONL trade replay
* [x]	Unit testing
* [x]	GitHub Actions CI workflow
* [ ]	OKX WebSocket market data integration
* [ ]	OKX REST API integration
* [ ]	Strategy engine
* [ ]	Order execution module
* [ ]	Position and portfolio management
* [ ]	Real-time monitoring and logging

Security

* Never commit API keys, secrets, or account credentials.
* Use environment variables or a secure secret manager for sensitive configuration.
* Test all strategies and risk parameters in a simulated environment before considering live deployment.

Disclaimer

This project is intended for software development, research, and educational purposes. It does not provide investment advice or guarantee trading performance. The current version does not implement live order execution.

License

This project is licensed under the MIT License.