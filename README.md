# Heston-Model
# Monte Carlo Option Pricing Model Incorporating Non-Constant Volatility

## Project Overview

The primary aim of this project is to create a Monte Carlo simulation for option pricing that incorporates non-constant volatility. The model expands upon the Black-Scholes framework by utilizing the Heston Model, which allows both the asset price \( S_t \) and its volatility \( V_t \) to be stochastic in nature. This provides a more realistic representation of market behavior, especially in turbulent market conditions where constant volatility models like Black-Scholes might not be adequate.

### Model Formulation

The Heston model is formulated as follows:

\`\`\`
dS_t = \\mu S_t dt + \\sqrt{V_t} S_t dW^1_t
dV_t = \\kappa (\\theta - V_t) dt + \\sigma \\sqrt{V_t} dW_t^2
\`\`\`

Where:
- \( S_t \) is the asset price at time \( t \)
- \( V_t \) is the volatility at time \( t \)
- \( \\mu \) is the expected return of the asset
- \( \\kappa \) is the mean reversion speed
- \( \\theta \) is the long-term volatility
- \( \\sigma \) is the volatility of volatility
- \( dW^1_t \) and \( dW^2_t \) are Wiener processes, possibly correlated with correlation \( \\rho \)

### Data Source

The project utilizes Yahoo Finance's API to fetch historical stock prices and option chain data for specified tickers. The data is then preprocessed and used to calculate various parameters needed for the Heston model.

### Parameter Estimation

The model estimates the initial parameters such as \( \\mu \), \( \\sigma \), \( \\kappa \), \( \\theta \), and \( \\rho \) based on historical data. These parameters are then used in the Monte Carlo simulation to generate multiple asset price paths.

### Closed-Form Solution

For comparative purposes, the project also includes a closed-form solution of the Heston model. Although the primary focus is American options, the closed-form solution is calculated for European options, providing a basis for comparison.

### Visualization and Analysis

The simulated asset paths are visualized, and the option prices are calculated for multiple strike prices. These simulated prices are compared with the actual market prices and the closed-form Heston model prices. The comparison provides insights into how well the model performs and where it might need adjustments.

## Usage

The project consists of several functions:

1. `get_ticker_data(ticker)`: Fetches and preprocesses historical stock and option data for a given ticker.
2. `get_parameters(option_data_df, stock_data_df)`: Estimates initial parameters needed for the Heston model.
3. `heston_price()`: Calculates the closed-form Heston option price.
4. `heston_monte_carlo()`: Performs Monte Carlo simulation for option pricing using the Heston model.
5. `mc_paths(option_data_df, stock_data_df)`: Integrates all the steps and returns a DataFrame comparing the Monte Carlo, closed-form, and actual option prices.
6. `plot_option_comparison(merged_comparison_df)`: Visualizes the comparison of option prices.
7. `all(ticker)`: End-to-end function that fetches data, performs simulations, and visualizes results for a given ticker.

## Results and Discussion

The model successfully simulates asset price paths and calculates option prices incorporating stochastic volatility. However, it has been observed that the Monte Carlo simulation tends to systematically underestimate the option prices when compared to market prices. This discrepancy could be due to various factors such as dividend payments, transaction costs, or perhaps an underestimation of market volatility.

## Future Work

- Incorporate dividend payments and transaction costs into the model.
- Enhance parameter estimation techniques.
- Extend the model to price other types of derivatives.
