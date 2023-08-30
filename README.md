# Heston-Model
# Monte Carlo Option Pricing Model Incorporating Non-Constant Volatility

## Project Overview

The primary aim of this project is to create a Monte Carlo simulation for option pricing that incorporates non-constant volatility. The model expands upon the Black-Scholes framework by utilizing the Heston Model, which allows both the asset price S<sub>t</sub> and its volatility V<sub>t</sub> to be stochastic in nature. This provides a more realistic representation of market behavior, especially in turbulent market conditions where constant volatility models like Black-Scholes might not be adequate.

### Model Formulation

The Heston model is formulated as follows:

<img src="\images\heston.png">

i.e. both the underlying stock price as well as the volatility are modelled as stochastic processes compared to Black-Scholes, where only S is modelled as such.

Parameters/Variables:
- S<sub>t</sub> is the asset price at time t
- V<sub>t</sub> is the volatility at time t
- &mu; is the expected return of the asset
-  κ is the mean reversion speed
- &theta; is the long-term volatility
- &sigma; is the volatility of volatility
- dW<sup>1</sup><sub>t</sub> and dW<sup>2</sup><sub>t</sub>are Wiener processes, possibly correlated with correlation &rho;

### Data Source

The project utilizes Yahoo Finance's API to fetch historical stock prices and option chain data for specified tickers. The data is then preprocessed and used to calculate various parameters needed for the Heston model.

### Parameter Estimation

The model estimates the initial parameters such as μ, σ, κ, θ, and ρ based on historical data. These parameters are then used in the Monte Carlo simulation to generate multiple asset price paths.

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

E.g. 

<img src="\images\paths.png">

6. `plot_option_comparison(merged_comparison_df)`: Visualizes the comparison of option prices.
7. `all(ticker)`: End-to-end function that fetches data, performs simulations, and visualizes results for a given ticker.

## Results and Discussion

The model successfully simulates asset price paths and calculates option prices incorporating stochastic volatility. However, it has been observed that the Monte Carlo simulation tends to systematically underestimate the option prices when compared to market prices. This discrepancy could be due to various factors such as dividend payments, transaction costs, or perhaps an underestimation of market volatility. Using the Euler method, while simple, is definitely also sub-optimal.

See, for example, the results we get for AMD option prices.

<img src="\images\AMD">

Overall, especially considering the incredibly limited form our parameter estimation is taking, surprisingly close to actual prices. It would also be fun to just compare it to the Black-Scholes model's predictions, just to see how big an effecet that stochastic volatility has.

## Future Work

- Incorporate dividend payments and transaction costs into the model. We're literally just selecting stocks from the S&P 500 where they're basically irrelevant.
- Enhance parameter estimation techniques.
- Extend the model to price other types of derivatives.
