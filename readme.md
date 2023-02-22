## Introduction
This code simulates bookings data to create a test dataset for an analytics model. It generates random parameters and creates anomalies to mimic real-world booking data.

## Functionality
To create synthetic data three main functions are being used:
- seasonality: A function that generates a sine wave with a variable shape and strength to simulate seasonal variations.
- simulate_expected_by_minute: A function that generates the expected bookings rate per minute, given a number of days. It takes into account various parameters, such as daily, weekly, monthly, and quarterly seasonality, as well as random hourly fluctuations.
- simulate_bookings_minute: A function that simulates the actual bookings rate per minute, given the expected rate and a standard deviation.
- The code also includes a helper function, make_lognorm, that creates a lognormal distribution with a specific mean and standard deviation.

## Usage
To use the code, call the make_test_dataframe function, which returns a pandas DataFrame with the following columns:

- minute: The minute of the day (0-1439).
- expected_rate: The expected bookings rate per minute.
- exp_rate_ci_min: The lower bound of the 98% confidence interval for the expected rate.
- exp_rate_ci_max: The upper bound of the 98% confidence interval for the expected rate.
- true_rate: The actual bookings rate per minute, which takes into account the lognormal distribution of the "true" rate.
- bookings: The number of bookings per minute, which follows a Poisson distribution with the actual rate.
- The DataFrame also includes a column anomaly_coef, which multiplies the true_rate column to account for anomalies in the data.

