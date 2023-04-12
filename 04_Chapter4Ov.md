# Chapter 4: Overview of Option Greeks

Welcome back, brave Knights of the Round Table! In the previous chapter, we delved into the intricacies of option pricing models. We covered the Black-Scholes and Garman-Kohlhagen models, how they work, and their respective strengths and weaknesses. We also discussed the importance of volatility in option pricing.

In this chapter, we will explore the concept of option Greeks, an integral part of options trading. Greeks are a way to measure the sensitivity of an option's price to changes in various parameters. Understanding Greeks is crucial for hedging an option portfolio, managing risk, and making informed investment decisions.

Before we proceed, let us take a moment to appreciate the origins of the term "option Greeks." Fun fact: it has nothing to do with the ancient Greeks! Instead, it derives from the mathematical symbols used to represent the Greeks. Delta (Δ), Gamma (Γ), Theta (Θ), Vega (ν), and Rho (ρ) are all written in the Greek alphabet.


## Delta
Delta represents the change in option price for a one-point move in the underlying asset. It is sensitive to changes in asset price and the time remaining until expiration. Delta is often used to hedge option positions by balancing them with the underlying asset.

## Gamma
Gamma is the rate of change of delta, measuring the sensitivity of delta to changes in the underlying asset price. It is important for monitoring the effectiveness of delta hedging, especially in high-volatility scenarios.

## Theta
Theta, also known as time decay, measures the rate of option price decay as time passes. It is usually negative, meaning that options lose value as time passes. Theta is important for option sellers who want to profit from time decay.

## Vega
Vega represents the sensitivity of an option's price to changes in implied volatility. It is often used to assess the impact of changes in volatility on an option portfolio. Vega is highest for at-the-money options and decreases as options become more in- or out-of-the-money.

## Rho
Rho measures the sensitivity of an option's price to changes in interest rates. It is less important than the other Greeks for equity options, since their values are usually not strongly affected by interest rates. However, it is crucial for fixed income options.

Now that we have introduced the option Greeks, we can begin implementing them in our C++ code. Stay tuned, brave Knights, for the next chapter, where we will dive deeper into the complexities of low-latency option volatility estimation.
# Chapter 4: Overview of Option Greeks

Welcome back, brave Knights of the Round Table! In the previous chapter, we delved into the intricacies of option pricing models. We covered the Black-Scholes and Garman-Kohlhagen models, how they work, and their respective strengths and weaknesses. We also discussed the importance of volatility in option pricing.

At the next meeting of the Round Table, King Arthur called forth Sir Delta, who had recently been in charge of the kingdom's option portfolio. Sir Delta came forward, feeling a bit nervous under the King's stern gaze. "Your Majesty," he began, "I have been monitoring our option portfolio, but I fear that I have not fully understood the concept of option Greeks."

The other knights looked at Sir Delta with raised brows, for they had heard of option Greeks but were not entirely sure what they were either. The King, however, nodded. "An astute concern, Sir Delta. For how can one manage risk without understanding it fully?"

And so, Sir Delta set out to research and learn all he could about option Greeks. He discovered delta, which measures the sensitivity of an option's price to changes in the underlying asset. He learned about gamma, which is the rate of change of delta, and about how to monitor the effectiveness of delta hedging. He read about theta, which measures time decay, and how it is important to option sellers. Sir Delta also learned about vega, which measures the sensitivity of an option's price to changes in implied volatility, and rho, which measures the sensitivity of an option's price to changes in interest rates.

Sir Delta was feeling quite knowledgeable about option Greeks, but he wasn't sure how to implement this in the kingdom's option portfolio. So, he consulted with Sir Black-Scholes, who was well-versed in option pricing models. Together, they developed a framework for incorporating option Greeks into the portfolio management system.

They started by calculating delta and gamma for each option in the portfolio using C++ code. They then monitored these values and made adjustments as necessary to keep the portfolio well-hedged. They also used theta and vega to evaluate the impact of time decay and volatility changes on the portfolio's value.

Thanks to Sir Delta's diligence and Sir Black-Scholes' expertise, the kingdom's option portfolio became much more dynamic and resilient. And at the next meeting of the Round Table, King Arthur commended Sir Delta's hard work and presented him with a shiny new sword to honor his accomplishment.

The other knights were impressed and inspired by Sir Delta's success, and they set out to learn more about option Greeks themselves. And so, the kingdom's option portfolio continued to thrive thanks to the ingenuity and hard work of its knights.

But the journey isn't over yet, brave knights. Stay tuned for the next chapter, where we will dive deeper into the complexities of low-latency option volatility estimation.
# Implementation of Option Greeks in C++

As mentioned in the previous chapter, option Greeks are an important tool for managing options portfolios and assessing risk. In this chapter, we will explore how to implement option Greeks in our C++ code.

First, let's define some variables:

```c++
double spotPrice;       // current price of the underlying
double strikePrice;     // strike price of the option
double volatility;      // implied volatility of the option
double riskFreeRate;    // risk-free interest rate
double timeToExpiry;    // time until option expiration
```

Using these variables, we can calculate the option price using the Black-Scholes formula:

```c++
double d1 = (log(spotPrice / strikePrice) + (riskFreeRate + 0.5 * volatility * volatility) * timeToExpiry) / (volatility * sqrt(timeToExpiry));
double d2 = d1 - volatility * sqrt(timeToExpiry);
double callOptionPrice = spotPrice * normalCDF(d1) - strikePrice * exp(-riskFreeRate * timeToExpiry) * normalCDF(d2);
```

Here, `normalCDF()` is a function that calculates the cumulative distribution function of a standard normal distribution. This can be implemented using numerical approximation methods, such as Taylor series or quadrature rules.

Now that we have calculated the option price, we can use finite differences to calculate the option Greeks. For example, to calculate delta, we can perturb the spot price by a small amount `h` and calculate the resulting change in option price:

```c++
double h = 0.0001;      // small perturbation
double perturbedSpotPrice = spotPrice + h;
double perturbedCallOptionPrice = perturbedSpotPrice * normalCDF(d1_perturbed) - strikePrice * exp(-riskFreeRate * timeToExpiry) * normalCDF(d2_perturbed);
double delta = (perturbedCallOptionPrice - callOptionPrice) / h;
```

Similarly, we can calculate gamma, theta, vega, and rho by perturbing the corresponding variables and calculating the resulting changes in option price.

```c++
double perturbedVolatility = volatility + h;
double perturbedCallOptionPrice = spotPrice * normalCDF(d1_perturbed) - strikePrice * exp(-riskFreeRate * timeToExpiry) * normalCDF(d2_perturbed);
double vega = (perturbedCallOptionPrice - callOptionPrice) / h;
```

And that's it! By implementing these calculations in our C++ code, we can effectively manage our options portfolios with greater precision and foresight.

Remember, brave Knights, that option Greeks are just one tool in the complex world of options trading. In the next chapter, we will delve into the intricacies of low-latency option volatility estimation, another crucial aspect of successful trading.