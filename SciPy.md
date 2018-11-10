#Hypothesis Testing with SciPy

## Statistical Concepts

### Intro

When conducting data analysis, we want to say something meaningful about our data. Often, we want to know if a change or difference we see in a dataset is "real" or if it’s just a normal fluctuation or a result of the specific sample of people we have chosen to measure. A difference we observe in our data is only important if we can be reasonably sure that it is representative of the population as a whole, and reasonably sure that our result is repeatable.

In this lesson, we will cover the fundamental concepts that will help us create tests to measure our confidence in our statistical results:

-Sample means and population means
-The Central Limit Theorem
-Why we use hypothesis tests
-What errors we can come across and how to classify them

### Sample Mean and Population Mean

A sample is a subset of the entire population. The mean of each sample is the sample mean and it is an estimate of the population mean.

For a population, the mean is a constant value no matter how many times it's recalculated. But with a set of samples, the mean will depend on exactly what samples we happened to choose. From a sample mean, we can then extrapolate the mean of the population as a whole. There are many reasons we might use sampling, such as:
-We don't have data for the whole population.
-We have the whole population data, but it is so large that it is infeasible to analyze.
-We can provide meaningful answers to questions faster with sampling.

### Central Limit Theorem

A sample can be skewed to one direction of the total population if  the sample mean was far off from your population mean. It looks like the measured sample must have been the highest or the lowest representative of the population sample. How do you get an average sample that looks more like the average population?

This is a natural consequence of the fact that a set of samples has less data than the population to which it belongs. If our sample selection is poor then we will have a sample mean seriously skewed from our population mean.

There is one surefire way to mitigate the risk of having a skewed sample mean — take a larger set of samples. The sample mean of a larger sample set will more closely approximate the population mean. This phenomenon, known as the *Central Limit Theorem*, states that if we have a large enough sample size, all of our sample means will be sufficiently close to the population mean.

### Hypothesis Tests

A *null hypothesis* is a statement that the observed difference is the result of chance.

*Hypothesis testing* is a mathematical way of determining whether we can be confident that the *null hypothesis* is false. Different situations will require different types of hypothesis testing.

### Type I Or Type II

In statistical hypothesis testing, we concern ourselves primarily with two types of error. The first kind of error, known as a Type I error, is finding a correlation between things that are not related. This error is sometimes called a "false positive" and occurs when the null hypothesis is rejected even though it is true.

For example, let's say you conduct an A/B test for an online store and conclude that interface B is significantly better than interface A at directing traffic to a checkout page. You have rejected the null hypothesis that there is no difference between the two interfaces. If, in reality, your results were due to the groups you happened to pick, and there is actually no significant difference between interface A and interface B in the greater population, you have been the victim of a false positive.

The second kind of error, a Type II error, is failing to find a correlation between things that are actually related. This error is referred to as a "false negative" and occurs when the null hypothesis is accepted even though it is false.

For example, with the A/B test situation, let's say that after the test, you concluded that there was no significant difference between interface A and interface B. If there actually is a difference in the population as a whole, your test has resulted in a false negative.

### P-Values

We have discussed how a hypothesis test is used to determine the validity of a null hypothesis. A hypothesis test provides a numerical answer, called a p-value, that helps us decide how confident we can be in the result. A p-value is the probability that the null hypothesis is true.

A p-value of 0.05 would mean that there is a 5% chance that the null hypothesis is true. This generally means there is a 5% chance that there is no difference between the two population means.

Before conducting a hypothesis test, we determine the necessary threshold we would need before concluding that the results are significant. A higher p-value is more likely to give a false positive so if we want to be very sure that the result is not due to just chance, we will select a very small p-value.
