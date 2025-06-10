# Options Trading Strategy Simulator
*Backend engine for modeling and testing options trading strategies with integrated authentication workflows*

## Key Contributions

### 🚀 Simulation Engine Implementation
- Designed and implemented backend engine to model/test predefined and custom options trading strategies
- Developed dynamic RESTful APIs that auto-generate trade legs using live/historical options data based on:
  - Index selection
  - Strategy type
  - Expiration parameters
  - Strike price parameters
- Utilized FastAPI for asynchronous, validated endpoints enabling real-time simulation and trade leg storage
- Ensured robust error handling and modular architecture for future extensibility (PnL calculations)

### 🗄️ Data Architecture
- Built scalable PostgreSQL schema with optimized tables:
  - `simulations` (core strategy metadata)
  - `simulation_legs` (individual trade components)
- Implemented date-partitioned tables for efficient querying of minute-level market data
- Designed indexed relationships for fast strategy execution and backtesting

### 🔐 Authentication System
- **OTP Verification**:
  - Integrated Twilio for OTP-based user registration/authentication
  - Implemented JWT token management for secure session handling
- **Password Workflows**:
  - Configured SMTP server for automated password delivery
  - Developed email templates for system-generated credentials
  - Created secure token system for password-reset links
  - Implemented full reset workflow via email validation

## Technical Architecture
| Component        | Technology               | Implementation Details                  |
|------------------|--------------------------|-----------------------------------------|
| **Framework**    | FastAPI                  | Async endpoints with Pydantic validation|
| **Database**     | PostgreSQL               | Date-partitioned tables for time-series |
| **Auth**         | Twilio + JWT             | OTP verification + token management     |
| **Email**        | SMTP                     | Password delivery + reset workflows     |
| **Infrastructure**| Uvicorn                 | ASGI server for high concurrency        |

## Workflow Integration
```mermaid
graph LR
A[User Registration] --> B[Twilio OTP Verification]
B --> C[Account Creation]
C --> D[SMTP Password Delivery]
D --> E[Strategy Simulation]
E --> F[Trade Leg Generation]
F --> G[Market Data Query]
G --> H[Result Computation]
