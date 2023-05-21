# Monte Carlo simulation using Weibull Distribution
This project focuses on utilizing Monte Carlo simulation techniques to generate random numbers following the Weibull distribution by leveraging the inverse cumulative density function (ICDF). The inverse CDF method allows us to transform uniformly distributed random numbers into numbers that follow a desired probability distribution. For this case 

## Implemented Codes
In this project I used two Weibull implementations of 2 and 3 parameters, one to find the best parameters (scale, shape and location) and one that generates random numbers.

### Finding the best parameters (fitweibull2(x), fitweibull3(x)):
These functions are used for estimating the parameters of the Weibull distribution: fitweibull2 for the 2-parameter Weibull distribution and fitweibull3 for the 3-parameter Weibull distribution. These functions utilize optimization techniques to estimate the scale, shape, and location parameters based on the provided data array (x).

Short explanation: used SciPy exponweib module for the Weibull probability density function (PDF), and the minimize function from the SciPy optimize module for minimizing the negative log-likelihood function. The negative log-likelihood function is defined as optfun. It takes a parameter vector theta as input and computes the negative log-likelihood of the Weibull distribution with shape theta[0], scale theta[1], and fixed location 0 at the given dataset x. The negative log-likelihood is returned as the objective to be minimized. The optimization is performed using the minimize function. It takes the negative log-likelihood function (optfun), initial guesses (initial_guess), optimization method (SLSQP), bounds for the shape and scale parameters (bounds), and a tolerance level (tol) as input. The optimization aims to find the parameter values that minimize the negative log-likelihood. The values 1.2 and 0.572 are used as coefficients in the parameter estimation process of the Weibull distribution. These coefficients are commonly used as heuristics or empirical values 

### Generating random numbers (weinbull2_rand(data, loops, size=None), weinbull3_rand(data, loops, size=None)):

Random numbers were generated using the the Inverse Cumulative Density Function, and has two loops, the first one to create a set of data and take the mean of results, and the second one to generate the desired amount of random values.

## Testing

In the tests, the metrics evaluated were the proximity of the results to the original value of a data set of vibration values of a machine. Where three combinations were evaluated.
    - 1st Combination: Implemented parameter search code and random number generation code.
    - 2nd Combination: stats.weibull_min.fit for parameter search and weibull_min function for random number generation.
    - 3rd Combination: Implemented parameter search code and weibull_min function for generating random numbers.

## Results and Conclusion

- The codes were developed to present two main differences in relation to the scipy module's weibull_min function (used to generate random numbers) and stats.weibull_min.fit (used to find the parameters given a set of data):
    - Greater precision, when performing an internal loop of interactions to generate a value based on the averages, and thus generate a set of numbers of the desired size, in addition to presenting greater precision to find the parameters of the Weibull distributions.
    - Shorter calculation time.
  
- In the tests for the 2-parameter Weibull, the 1st Combination presented results with greater precision, but the 3rd combination obtained very close results, with a better execution time, both also with results with very low difference in relation to the original values. The 2nd combination obtained values far from the original with high execution time.

- In the tests for the 3-parameter Weibull, the 1st Combination presented results with greater precision, the 3rd presented a better execution time, but with a certain distance from the original values. The 2nd combination obtained values far from the original with high execution time.

- The choice of combination and which of the Weibull distribution types and code combinations is dependent on the situation, however, for the tests carried out, the 3nd combination presents the best combination of precision and time for Weibull using two parameters, and the 1st combination presents the best results for Weibull of three parameters.


