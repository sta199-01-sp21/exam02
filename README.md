# STA 199: Exam 02- Due Monday April 5 at 11:59 PM

# Instructions

The exam questions are in the README portion of the repository below.

### Deadline

This exam is due on Monday April 5 at 11:59 PM.

You must submit a PDF document to Gradescope that corresponds to an
`.Rmd` file on your GitHub repository in order to receive credit for
this exam.

**There will be no grace period. Start and submit the exam early in
order to** **avoid any last-minute technical issues.**

**You may resubmit the exam before the deadline.**

If a PDF is not uploaded to Gradescope by the submission deadline, your
latest commit prior to the deadline will be used as your submission.
There will be a penalty for failing to submit a PDF to Gradescope.

Commit and push often and at appropriate times. Part of your grade will
be based on quality of commit history.

### Rules

  - This is an individual assignment.
  - Everything in your repository is for your eyes only.
  - You may not collaborate or communicate anything about this exam to
    **anyone** except the instructor. For example, you may not
    communicate with other students, the TAs, or post/solicit help on
    the internet, email or via any other method of communication.
  - You may use `R`, as well as any notes, books, or existing internet
    resources to answer exam questions.
  - You must cite any code you use as inspiration. A failure to cite is
    plagiarism. Cite any sources by providing a link to the original
    source in your exam write-up.
  - No TA office hours will be held while the exam is live.
  - Piazza will be inactive while the exam is live.
  - Do not email the TAs with questions.
  - If you have questions email the instructor. Questions should only be
    about understanding the data or the exam’s instructions. You may not
    ask questions on any topics from past assignments or material
    related to the exam.
  - The instructor will provide code debugging if needed, but this will
    result in a **grade penalty** if needed.

### Academic Integrity

By taking this exam, you pledge to uphold the Duke Community Standard:

  - I will not lie, cheat, or steal in my academic endeavors;
  - I will conduct myself honorably in all my endeavors; and
  - I will act if the Standard is compromised.

### Submission

Please only upload your PDF document to Gradescope. Before you submit
the uploaded document, mark where each answer is to the exercises. If
any answer spans multiple pages, then mark all pages. Make sure to
associate the “Overall” section with the first page. **Failure to do so
may result in points** **being taken off.**

Make sure that your uploaded PDF document matches your `.Rmd` and the
PDF in your repository exactly. Points will be deducted for
non-reproducibility.

## Introduction

In recent years, bike share programs have become increasingly popular,
with cities across the United States adopting these programs. Riders can
either rent for a single ride or (in many cities) get a subscription to
these programs. Bike share programs can be useful for riders who may not
have space to store a bicycle and also are a way for individuals to play
their own small role in helping combat climate change. As evidence of
their newfound importance, Treasury Secretary Pete Buttigieg was
recently spotted riding a rideshare bicycle in Washington D.C.

The below dataset provides information on bikeshare ridership in the
Capital Bikeshare program in 2011.

  - `date`: date
  - `season`: season
      - 1: spring
      - 2: summer
      - 3: fall
      - 4: winter
  - `month`: month (1 - 12)
  - `holiday`: whether or not day is holiday
  - `weekday`: day of the week (1 = Monday)
  - `working`: work day or not (1 = yes)
  - `weather`:
      - 1: clear or only partly cloudy
          - 2: cloudy or misty
          - 3: light rain or light snow or scattered thunderstorms
          - 4: heavy rain or ice or thunderstorms
  - `temp` : temperature in Fahrenheit
  - `hum`: humidity
  - `windspeed`: windspeed in km / hour
  - `casual`: count of casual users
  - `registered`: count of registered users
  - `count`: count of total rental bikes including both casual and
    registered

## Packages

You’ll need the following `R` packages for this exam. These are included
in `exam_02.Rmd`.

``` r
library(tidyverse)
library(infer)
library(broom)
```

## Data

To get started, read in the data. This code is provided in your
`exam_02.Rmd` file.

``` r
bikes <- read_csv("data/bikes.csv")
```

## Tasks

You must use functions in the loaded packages above when applicable. You
must also follow the `tidyverse` coding style. All visualizations should
implement best practices as discussed in lecture. You do not need to
print out your tibble result unless a task asks you to do so.

As a warning, this data may not be free from error. Use your best
judgment on how to deal with the data if you come across obvious
mistakes.

#### Task 1

Recode `weather` so instead of having values 1, 2, 3, 4, it contains
values `"clear"`, `"clouds"`, `"rain"`, and `"storm"` according to the
data dictionary. Overwrite `bikes`.

Mutate a new variable called `windchill` that is a function of
temperature (`temp`) and wind speed (`windspeed`), where `windchill` is
equal to temperature minus wind speed raised to the 0.60 power.
Overwrite `bikes`.

#### Task 2

Is it the heat or the humidity? Use a single code pipeline to report the
sample correlation between humidity and temperature.

Then, construct a 99% bootstrap confidence interval for the true
correlation. Display your bootstrap distribution and confidence interval
in an effective visualization and provide a concise, one-sentence
interpretation of your interval in the context of the problem. Use
10,000 replications in your simulation.

Suppose there is a hypothesis test about the population correlation,
where under the null hypothesis the correlation is 0.30. The test
considers a two-sided alternative hypothesis. Based on your bootstrap
confidence interval, should you reject or fail to reject the null
hypothesis at α = 0.05? Justify your answer without conducting the
hypothesis test.

#### Task 3

An official in the Department of Transportation claims that there are
more registered bike rentals on work days than weekends and holidays.
Perform a statistical hypothesis test to investigate this claim. Clearly
outline each step and provide an appropriate conclusion in the context
of the problem.

#### Task 4

Create a 90% CLT-based confidence interval for the true mean number of
bike rentals in Summer. Do this without using the R functions `t_test()`
and `t.test()`. Interpret your interval in the context of the problem.

#### Task 5

Fit a linear model to predict `count` based on the predictors `temp`,
`weather`, and `working`. Save this fitted model as an object named
`model_1`, and report the model output in a tidy format and write out
the linear model.

#### Task 6

Interpret each of the coefficients from `model_1` in the context of the
problem. Comment on whether or not each makes sense.

#### Task 7

Based on `model_1`, construct a 90% confidence interval for β\_temp and
provide an interpretation in the context of the problem.

#### Task 8

Suppose the next three days are as follows:

  - 80 and sunny for Independence day
  - 75 and cloudy for Saturday
  - 98 and clear for Sunday

Use your linear model (`model_1`) to make predictions for the count of
bike rentals for the next three days. Comment on the validity of these
predictions.

#### Task 9

Consider the model you fit in Task 5. Are all of the model assumptions
satisfied? Answer comprehensively and support your answer with
appropriate visualizations.

#### Task 10

Fit a linear model to predict `count` based on the predictors
`windchill`, `weather`, and the interaction between `windchill` and
`weather`. Save this fitted model as `model_2` and write out the linear
model for each type of weather.

#### Task 11

Create a scatterplot of `count` versus `windchill` with points colored
by `weather`. Display the fitted line for each weather category and
describe what you notice.

#### Task 12

Compare models `model_1` and `model_2`. Which model is better and why?

#### Task 13

Identify the following statements as TRUE or FALSE. Provide a brief, one
sentence justification for statements that are FALSE. No justification
is necessary for TRUE statements.

1)  If a researcher rejects the null hypothesis, then it is possible a
    Type II error was committed.

2)  The value of the parameter under the null hypothesis should be
    chosen after examining the sample data so the hypothesis test is
    done for a plausible value.

3)  If you want to reduce the chance of a Type I error, then you should
    choose a smaller significance level.

4)  Consider a hypothesis test where the value of the mean under the
    null is 10 and a two-sided alternative is considered. If the
    observed sample mean was found to be 15.2 from a sample of size 32,
    then we are able to reject the null hypothesis.

5)  For a hypothesis test at the 0.01 significance level, the
    probability you fail to reject the null hypothesis given that the
    null hypothesis is true is 0.99.

#### Task 14

A polling company approaches you and says they want to create a 95%
confidence interval for the population proportion on a topic of
interest. They want their margin of error to be at most 0.03. As with
most companies, they are limited in the resources they can expend on
data collection. Be specific on the sample size you would advise them to
take to meet their goals while minimizing costs.

