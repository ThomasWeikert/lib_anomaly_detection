# expected rate lower ci vs observed rate

## Overview
This project is an implementation of a new approach for modeling the expected rate for an anomaly detection system. The approach uses a single distribution such as Poisson or log-normal to compute the expected rate per minute given a mean and std of a previous sequence.

## Files
The project includes the following files:

- ```expected_rate.ipynb```: Simulates bookings data to create a test dataset to compare confidence interval of expected rate vs number of events. It generates random parameters and creates anomalies to mimic real-world booking data.
- ```test.ipynb```: This code contains several functions that preprocess hotel booking data, group it by arrival date, create sequences of data, estimate expected arrival rates, and generate confidence intervals for those rates. The data is loaded from a CSV file using the load_data function and preprocessed using the preprocess_data function. The preprocessed data is then filtered by hotel using the get_hotel_arrivals_by_date function, which generates a daily arrivals dataframe. Sequences of 14 days are extracted from the daily arrivals dataframe using the create_sequences function, and expected arrival rates are calculated using the calculate_exp_rate function. Confidence intervals for the expected rates are generated using the get_exp_rate_intervals function, which relies on the make_lognorm function to create lognormal distributions. Finally, the est_poission_rate_ci function estimates Poisson rate parameter confidence intervals for observed arrival rates, and the is_outlier function checks whether an expected rate falls outside a confidence interval and thus constitutes an outlier.
- ```hotel_booking.csv```: This is a CSV file that contains hotel booking data from Kaggle used for testing the approach.
- ```stat_test.ipynb```: some old work


### Overview syntethic data
The expected_rate.ipynb simulates bookings data to create a test dataset for an analytics model. It generates random parameters and creates anomalies to mimic real-world booking data.

#### Functionality
To create synthetic data three main functions are being used:
- seasonality: A function that generates a sine wave with a variable shape and strength to simulate seasonal variations.
- simulate_expected_by_minute: A function that generates the expected bookings rate per minute, given a number of days. It takes into account various parameters, such as daily, weekly, monthly, and quarterly seasonality, as well as random hourly fluctuations.
- simulate_bookings_minute: A function that simulates the actual bookings rate per minute, given the expected rate and a standard deviation.
- The code also includes a helper function, make_lognorm, that creates a lognormal distribution with a specific mean and standard deviation.

#### Usage
To use the code, call the make_test_dataframe function, which returns a pandas DataFrame with the following columns:

- minute: The minute of the day (0-1439).
- expected_rate: The expected bookings rate per minute.
- exp_rate_ci_min: The lower bound of the 98% confidence interval for the expected rate.
- exp_rate_ci_max: The upper bound of the 98% confidence interval for the expected rate.
- true_rate: The actual bookings rate per minute, which takes into account the lognormal distribution of the "true" rate.
- bookings: The number of bookings per minute, which follows a Poisson distribution with the actual rate.
- The DataFrame also includes a column anomaly_coef, which multiplies the true_rate column to account for anomalies in the data.

