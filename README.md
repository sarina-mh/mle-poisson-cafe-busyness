# Poisson Parameter Estimation via Maximum Likelihood

R implementation of Maximum Likelihood Estimation for a Poisson process, applied to estimating cafe busyness from hourly customer counts. Part of Engineering Probability and Statistics, University of Tehran.

## Overview

This notebook explores parameter estimation using Maximum Likelihood Estimation (MLE) in the context of a Poisson process. The scenario models customer arrivals at MKG Cafe, where the true arrival rate is unknown and must be estimated from observed hourly counts.

The notebook covers:

- Generating and analyzing a single 24-hour observation sample
- Constructing the log-likelihood function and finding the MLE visually
- Direct computation of the MLE (sample mean for Poisson)
- How observation length affects estimation precision
- Comparing the true Poisson distribution with the estimated one

## Mathematical Framework

### Poisson Distribution

The probability of observing $k$ events in a fixed interval:

$$P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$$

where $\lambda$ is the average rate of events per interval.

### Maximum Likelihood Estimation

Given observations $x_1, x_2, \ldots, x_n$ from a Poisson($\lambda$) distribution, the log-likelihood function is:

$$\ell(\lambda) = \sum_{i=1}^{n} \left( x_i \ln(\lambda) - \lambda - \ln(x_i!) \right)$$

Taking the derivative and setting it to zero:

$$\hat{\lambda}_{MLE} = \frac{1}{n}\sum_{i=1}^{n} x_i = \bar{x}$$

The MLE for the Poisson parameter equals the sample mean.

### Variance of the Estimate

The variance of $\hat{\lambda}$ decreases with observation length:

$$\text{Var}(\hat{\lambda}) = \frac{\lambda}{n}$$

## Repository Structure

```
eps-mle-cafe-simulation/
  EPS_CA6_MLE_Cafe.ipynb   # Main notebook (R kernel)
  README.md
  LICENSE
  environment.yml
  .gitignore
```

## Dependencies

- R >= 4.5
- ggplot2
- reshape2

## Installation

Install R packages before running the notebook:

```r
install.packages(c("ggplot2", "reshape2"))
```

Or use the conda environment:

```bash
conda env create -f environment.yml
conda activate eps-mle-cafe-simulation
```

## Usage

Open the notebook in Jupyter or VS Code with the R kernel extension:

```bash
jupyter notebook EPS_CA6_MLE_Cafe.ipynb
```

Run cells sequentially. The notebook starts by generating a 24-hour observation sample with a known true rate (lambda = 6), then walks through the estimation process.

## Results

The notebook produces visualizations covering:

- Log-likelihood curve showing the MLE peaks at the sample mean
- Distribution of lambda estimates across different observation lengths (6 to 168 hours)
- Variance of estimates decreasing as observation length increases
- Boxplot comparison of estimation spread across observation lengths
- True vs estimated Poisson PMF overlay

Key finding: with only 4 hours of observation, the standard deviation of lambda estimates is approximately 1.25. This shrinks substantially with longer observation periods, confirming the $1/\sqrt{n}$ convergence rate.

## Citation

If this work is useful for your research or coursework, please cite:

```bibtex
@misc{mahmoudi2026mlecafe,
  title = {Poisson Parameter Estimation via Maximum Likelihood},
  author = {Sarina Mahmoudi},
  year = {2026},
  note = {Engineering Probability and Statistics, Computer Assignment 6},
  institution = {University of Tehran, School of Electrical and Computer Engineering},
  instructors = {Dr. Bahrak, Dr. Vahhabi}
}
```

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.
