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

## Hypothesis Testting 

### Types of Hypothesis Test

When we are trying to compare datasets, we often need a way to be confident knowing if datasets are significantly different from each other.
Some situations involve correlating numerical data like a professor expects an exam average to be roughly 75%, and wants to know if the actual scores line up with this expectation. Was the test actually too easy or too hard?

Others involve categorical data, for example:
a pollster wants to know if men and women have significantly different yogurt flavor preferences. Does a result where men more often answer "chocolate" as their favorite reflect a significant difference in the population?

You will learn how about how we can use hypothesis testing to answer these questions. There are several different types of hypothesis tests for the various scenarios you may encounter. Luckily, SciPy has built-in functions that perform all of these tests for us, normally using just one line of code.

For numerical data, we will cover:
-One Sample T-Tests
-Two Sample T-Tests
-ANOVA
-Tukey Tests

For categorical data, we will cover:
-Binomial Tests
-Chi Square

### 1 Sample T-Testing

Let's imagine the fictional business BuyPie, which sends ingredients for pies to your household, so that you can make them from scratch. Suppose that a product manager wants the average age of visitors to BuyPie.com to be 30. In the past hour, the website had 100 visitors and the average age was 31. Are the visitors too old? Or is this just the result of chance and a small sample size?

We can test this using a univariate T-test. A univariate T-test compares a sample mean to a hypothetical population mean. It answers the question "What is the probability that the sample came from a distribution with the desired mean?"

When we conduct a hypothesis test, we want to first create a null hypothesis, which is a prediction that there is no significant difference. The null hypothesis that this test examines can be phrased as such: "The set of samples belongs to a population with the target mean".

The result of the 1 Sample T Test is a p-value, which will tell us whether or not we can reject this null hypothesis. Generally, if we receive a p-value of less than 0.05, we can reject the null hypothesis and state that there is a significant difference.

SciPy has a function called ttest_1samp, which performs a 1 Sample T-Test for you.

**ttest_1samp** requires two inputs, a distribution of values and an expected mean:
```python
tstat, pval = ttest_1samp(example_distribution, expected_mean)
print(pval)
```
It also returns two outputs: the t-statistic and the p-value — telling us how confident we can be that the sample of values came from a distribution with the mean specified.

In the last exercise, we got a p-value that was much higher than 0.05, so we cannot reject the null hypothesis. Does this mean that if we wait for more visitors to BuyPie, the average age would definitely be 30 and not 31? Not necessarily. In fact, in this case, we know that the mean of our sample was 31.

P-values give us an idea of how confident we can be in a result. Just because we don’t have enough data to detect a difference doesn’t mean that there isn’t one. Generally, the more samples we have, the smaller a difference we’ll be able to detect.

### 2 Sample T-Test

Suppose that last week, the average amount of time spent per visitor to a website was 25 minutes. This week, the average amount of time spent per visitor to a website was 28 minutes. Did the average time spent per visitor change? Or is this part of natural fluctuations?

One way of testing whether this difference is significant is by using a 2 Sample T-Test. A 2 Sample T-Test compares two sets of data, which are both approximately normally distributed.

The null hypothesis, in this case, is that the two distributions have the same mean.

We can use SciPy's **ttest_ind** function to perform a 2 Sample T-Test. It takes the two distributions as inputs and returns the t-statistic (which we don't use), and a p-value.
```python
tstat, pval = ttest_ind(sample1, sample2)
print(pval)
```

### Dangers of Multiple T-Tests

Suppose that we own a chain of stores that sell ants, called VeryAnts. There are three different locations: A, B, and C. We want to know if the average ant sales over the past year are significantly different between the three locations.

At first, it seems that we could perform T-tests between each pair of stores.

We know that the p-value is the probability that we incorrectly reject the null hypothesis on each t-test. The more t-tests we perform, the more likely that we are to get a false positive, a Type I error.

For a p-value of 0.05, if the null hypothesis is true then the probability of obtaining a significant result is 1 – 0.05 = 0.95. When we run another t-test, the probability of still getting a correct result is 0.95 * 0.95, or 0.9025. That means our probability of making an error is now close to 10%! This error probability only gets bigger with the more t-tests we do.

### ANOVA

When comparing more than two numerical datasets, the best way to preserve a Type I error probability of 0.05 is to use ANOVA. ANOVA (Analysis of Variance) tests the null hypothesis that all of the datasets have the same mean. If we reject the null hypothesis with ANOVA, we're saying that at least one of the sets has a different mean; however, it does not tell us which datasets are different.

We can use the SciPy function f_oneway to perform ANOVA on multiple datasets. It takes in each dataset as a different input and returns the t-statistic and the p-value. For example, if we were comparing scores on a videogame between math majors, writing majors, and psychology majors, we could run an ANOVA test with this line:
```python
fstat, pval = f_oneway(scores_mathematicians, scores_writers, scores_psychologists)
```

The null hypothesis, in this case, is that all three populations have the same mean score on this videogame. If we reject this null hypothesis (if we get a p-value less than 0.05), we can say that we are reasonably confident that a pair of datasets is significantly different. After using only ANOVA, we can't make any conclusions on which two populations have a significant difference.

### Tukey's Range Test

We can perform a Tukey's Range Test to determine the difference between datasets.

The function to perform Tukey's Range Test is pairwise_tukeyhsd, which is found in statsmodel, not scipy. We have to provide the function with one list of all of the data and a list of labels that tell the function which elements of the list are from which set. We also provide the significance level we want, which is usually 0.05.

For example, if we were looking to compare mean scores of movies that are dramas, comedies, or documentaries, we would make a call to pairwise_tukeyhsd like this:
```python
movie_scores = np.concatenate([drama_scores, comedy_scores, documentary_scores])
labels = ['drama'] * len(drama_scores) + ['comedy'] * len(comedy_scores) + ['documentary'] * len(documentary_scores)

tukey_results = pairwise_tukeyhsd(movie_scores, labels, 0.05)
```
It will return a table of information, telling you whether or not to reject the null hypothesis for each pair of datasets.

###Binomial Test

So far, we have been working with numerical datasets. The tests we have looked at, the 1- and 2-Sample T-Tests, ANOVA, and Tukey's Range test, will not work if we can't find the means of our distributions and compare them.

If we have a dataset where the entries are not numbers, but categories instead, we have to use different methods.

To analyze a dataset like this, with two different possibilities for entries, we can use a Binomial Test. A Binomial Test compares a categorical dataset to some expectation.

Examples include:
-Comparing the actual percent of emails that were opened to the quarterly goals
-Comparing the actual percentage of respondents who gave a certain survey response to the expected survey response
-Comparing the actual number of heads from 1000 coin flips of a weighted coin to the expected number of heads

The null hypothesis, in this case, would be that there is no difference between the observed behavior and the expected behavior. If we get a p-value of less than 0.05, we can reject that hypothesis and determine that there is a difference between the observation and expectation.

SciPy has a function called binom_test, which performs a Binomial Test for you.

**binom_test** requires three inputs, the number of observed successes, the number of total trials, and an expected probability of success. For example, with 1000 coin flips of a fair coin, we would expect a "success rate" (the rate of getting heads), to be 0.5, and the number of trials to be 1000. Let's imagine we get 525 heads. Is the coin weighted? This function call would look like:
```python
pval = binom_test(525, n=1000, p=0.5)
```
It returns a p-value, telling us how confident we can be that the sample of values was likely to occur with the specified probability. If we get a p-value less than 0.05, we can reject the null hypothesis and say that it is likely the coin is actually weighted, and that the probability of getting heads is statistically different than 0.5.

### Chi Square Test

What if we also wanted to track if visitors added any items to their shopping cart? With three discrete categories of data per dataset, we can no longer use a Binomial Test. If we have two or more categorical datasets that we want to compare, we should use a Chi Square test. It is useful in situations like:
-An A/B test where half of users were shown a green submit button and the other half were shown a purple submit button. Was one group more likely to click the submit button?
-Men and women were both given a survey asking "Which of the following three products is your favorite?" Did the men and women have significantly different preferences?

In SciPy, you can use the function chi2_contingency to perform a Chi Square test.

The input to **chi2_contingency** is a contingency table where:
-The columns are each a different condition, such as men vs. women or Interface A vs. Interface B
-The rows represent different outcomes, like "Survey Response A" vs. "Survey Response B" or "Clicked a Link" vs. "Didn't Click"

This table can have as many rows and columns as you need.

In this case, the null hypothesis is that there's no significant difference between the datasets. We reject that hypothesis, and state that there is a significant difference between two of the datasets if we get a p-value less than 0.05.