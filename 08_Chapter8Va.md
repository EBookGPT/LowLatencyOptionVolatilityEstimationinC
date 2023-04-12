# Chapter 8: Vanilla Option Pricing using Binomial Trees

Welcome to the eighth chapter of our book on Low Latency Option Volatility Estimation in C++. In the previous chapter, we learned about Monte Carlo Simulation for Option Pricing. Now, we will explore another popular method for vanilla option pricing - Binomial Trees.

Here, we have a special guest, John Cox, who is a renowned financial economist and a pioneer in derivative pricing. John Cox, along with Stephen Ross and Mark Rubinstein, developed the binomial options pricing model, which is widely used in the finance industry today.

The binomial tree model is a discrete-time method to approximate the price evolution of the underlying asset. It is a simple and intuitive model that can handle multiple sources of uncertainty, making it popular among practitioners. In this chapter, we will learn how to implement the binomial tree model to price vanilla options.

Before we dive into the implementation, let's discuss the theory behind the binomial tree model. The model assumes that the price of the underlying asset can evolve to one of two states in each time step. The assumption of only two states is a major simplification, but it allows us to construct a binary tree-like structure to represent the possible future states of the underlying asset.

The binomial tree model can be used to price both European and American options. For European options, we can use a backward induction algorithm to calculate the option price at each time step, starting from the final time step and working backward to the initial time step. For American options, we need to consider the possibility of early exercise at each time step, which makes pricing more complicated.

In the next section, we will implement the binomial tree model in C++ and use it to price vanilla options. We will start by defining a binomial tree class and then use it to price both European and American call options.

Are you excited to start implementing the binomial tree model? Let's get started!
# Chapter 8: Vanilla Option Pricing using Binomial Trees

### Dracula and the Pricing of Vanilla Options

As the sun set over the Transylvanian mountains, Dracula awoke from his slumber. He had been sleeping for nearly a century and was eager to catch up on what he had missed. He was particularly interested in the field of finance and derivatives pricing. So, he summoned his trusted advisor, John Cox, to teach him about pricing vanilla options using binomial trees.

John Cox arrived at Dracula's castle the very next day. He explained to Dracula how to construct a binomial tree as a model for the underlying asset price. In this model, the price of the asset can evolve to one of two states in each time step. Based on these two states, the binomial tree can be constructed in a step-by-step fashion, similar to a decision tree.

Dracula was fascinated by the simplicity of this model and how it could be used to price both European and American options. Cox then showed him how to calculate the option price at each time step using backward induction. This method worked well for European options but was more complicated for American options since early exercise needed to be taken into account.

Dracula was intrigued by this method and was eager to try it himself. He decided to price a European call option using binomial trees. He started by defining a binomial tree class in C++ and then used it to price the option. He was amazed at how quickly and accurately he could price the option using this method.

```c++
// define the binomial tree class
class BinomialTree {
public:
    // constructor
    BinomialTree(double s, double k, double r, double v, double t, int n);

    // calculate option price by backward induction
    double calculateOptionPrice();

private:
    double s;   // underlying asset price
    double k;   // option strike price
    double r;   // risk-free interest rate
    double v;   // implied volatility
    double t;   // expiration time of option
    int n;      // number of time steps in binomial tree
};

// implementation of constructor
BinomialTree::BinomialTree(double s, double k, double r, double v, double t, int n)
 : s(s), k(k), r(r), v(v), t(t), n(n) {}

// implementation of calculateOptionPrice function
double BinomialTree::calculateOptionPrice() {
    // calculate time interval and discount factor
    double dt = t / n;
    double df = exp(-r * dt);

    // calculate up and down factors
    double u = exp(v * sqrt(dt));
    double d = 1 / u;

    // calculate probability of up and down moves
    double p_u = (exp(r * dt) - d) / (u - d);
    double p_d = 1 - p_u;

    // construct binomial tree structure
    vector<vector<double>> price(n + 1, vector<double>(n + 1));
    for (int i = 0; i <= n; i++) {
        for (int j = 0; j <= i; j++) {
            price[i][j] = s * pow(u, j) * pow(d, i - j);
        }
    }

    // calculate option value at terminal nodes
    vector<double> optionValue(n + 1);
    for (int j = 0; j <= n; j++) {
        optionValue[j] = max(price[n][j] - k, 0.0);
    }

    // calculate option value at previous time steps using backward induction
    for (int i = n-1; i >= 0; i--) {
        for (int j = 0; j <= i; j++) {
            optionValue[j] = df * (p_u * optionValue[j+1] + p_d * optionValue[j]);
        }
    }

    return optionValue[0];
}

BinomialTree bt(s, k, r, v, t, n);
double optionPrice = bt.calculateOptionPrice();
```

Dracula was pleased with the result and impressed by how fast the code executed. He thanked John Cox for his expert guidance and vowed to use this method to price all his future financial derivatives.

### The Resolution

And so, Dracula had learned about the binomial tree model and how to use it to price vanilla options. He could now price options with great efficiency and accuracy, thanks to this simple yet powerful method. 

John Cox had once again shared his expert knowledge and had helped Dracula stay relevant in the ever-changing field of finance. Together, they raised their glasses of blood-red wine to celebrate this milestone in Dracula's journey of learning.
## Explanation of Code

In the Dracula story, we saw that Dracula was interested in pricing European call options using the binomial tree method. For this purpose, we defined a `BinomialTree` class in C++ that took in the parameters of the option as its input. These parameters included the underlying asset price `s`, the strike price `k`, the risk-free interest rate `r`, the implied volatility `v`, the expiration time `t`, and the number of time steps `n`.

In the constructor of the `BinomialTree` class, we simply initialize the parameters of the option. We then define a `calculateOptionPrice()` method that calculates the option price using backward induction. In this method, we first calculate the time interval `dt` and the discount factor `df`. We then calculate the up and down factors `u` and `d` based on the implied volatility and time interval. Using these factors, we calculate the probability of an up move and a down move `p_u` and `p_d`.

Next, we construct the binomial tree structure using a 2D vector `price`, where `price[i][j]` represents the price of the underlying asset at time `i` and state `j`. We start by initializing the tree at time `0` with the initial underlying asset price `s`. We then use the up and down factors to construct the tree for subsequent time periods.

At each leaf node of the tree, we calculate the option value as the maximum of the difference between the underlying asset price and the strike price and `0`. This gives us the option value at expiration. We then work backward from the final time period to the initial time period, calculating the option value at each node using the backward induction formula. Finally, we return the option value at time `0`, which represents the estimated option price.

To use this `BinomialTree` class to price the European call option for Dracula's purposes, we simply create a `BinomialTree` object and call the `calculateOptionPrice()` method on it. The resulting value is the estimated price of the call option based on the binomial tree model.

Overall, this code provides a simple and efficient implementation of the binomial tree method for option pricing.