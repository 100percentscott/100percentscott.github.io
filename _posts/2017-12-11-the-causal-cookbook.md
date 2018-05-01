---
layout: post
title:  the causal cookbook
date:   2017-12-11 10:30:00
---
“Good empirical research is almost never simply the mechanical application of statistical techniques”

![](https://i.imgur.com/WiwWoSn.png?1){:height="40%" width="40%"}

# **Contents**
**Framework**
- [Question](#1-question)
- [Mechanism](#2-mechanism)
- [Randomisation](#3-randomisation)
- [User Interactions](#4-user-interactions)
- [Map](#5-map)

**AB Testing in practise**
- [Power Analysis](#1-power-analysis)
- [Checks](#2-checks)
- [What Test?](#3-what-test)
- [Conclusions](#4-conclusions)
- [External Validity](#5-external-validity)

**ELI5 Hypothesis Testing**
- [Test Statistic](#test-statistic)
- [Hypotheses](#hypotheses)
- [Type I error](#type-i-error)
- [Type II error](#type-ii-error)
- [P-value](#p-value)
- [One-sided vs Two-sided](#one-sided-vs-two-sided)
- [Confidence Interval](#confidence-interval)
- [Unequal Groups](#unequal-groups)
- [Missing values](#missing-values)

**[Further Reading](#further-reading)**
<br><br>

-----------------------
### **1. Question**
Let’s say we want to know the causal effect of X on Y, where X is a change to a product and Y is a set of outcomes we care about. For example:
- How will splitting a signup form across several pages affect conversion rates & contact rates?
- How will a new app screen affect driver positioning?
- How will a cancellation fee affect user retention?

This post outlines some thinking to help approach these problems.
<br><br>

### **2. Mechanism**
First, **clearly define the causal relationship the mechanism it works through**.  The relationship of interest is important because it determines what metrics you look at what method you use.  The mechanism is important because if you can’t convincingly explain it in simple terms, you are more likely to find a spurious effect (aka bullshit) if you find an effect at all.

The good news is that if it’s a product change you will already have a clear hypothesis validated to some extent with users and data.
<br><br>

### **3. Randomisation**
Second, ask the key question: **is randomisation possible?** If yes, there are experimental techniques available.  If no, there are non-experimental techniques available which are a little less clean.

Aside: to understand causality, the goal is to overcome **selection bias**.  

<span style="color:#d25b97">Selection Bias Intuition: Do hospitals make people healthier?  To answer this we could compare the health of people who have and have not been to hospital in the past year.  We’d learn that people who have not been to hospital are healthier, and might conclude that hospitals actually make people sick.  Of course, this is not the case.  Sick people choose to go to hospital, so the comparison is not a fair one.  This is selection bias, and why correlation ≠ causation.</span>

**Randomisation solves the selection problem**.  That is why it is the gold standard.  If we randomly assign users into the treatment group (go to hospital) and control group (do not go to hospital), then we can be sure that users don’t select into a group based on other factors (eg. sickness, or some other unobservable factor).  The comparison between groups is now a fair one.  This is an example of user-level randomisation.  Randomisation can be done at other levels too (eg. time, region, social group).
<br><br>

### **4. User Interactions**
Networks and marketplaces are special cases worth calling out.

From [okcupid](https://tech.okcupid.com/the-pitfalls-of-a-b-testing-in-social-networks/): “unfortunately, if you're doing tests for a product that relies heavily on **interaction between users** -- such as a dating app -- doing random assignment on a per-user basis can lead to unreliable experiments and misleading conclusions… Here's an example: Let's say one of our devs built a new video-chat feature and wanted to test if people liked it before launching it to all of our users. I could do an A/B test that randomly gave video-chat to one half of our users... but who would they use the feature with? ”.

Even if we overcame the logistical challenge, there remains the problems of **cannibalisation**, and **contamination**.  For example, suppose a ride-hailing app tests a price change.  It randomly assigns users to a treatment group (new lower price) and a control group (old price).  There is now more demand for cars from users in the treatment group because it’s cheaper.  As a result drivers are now more likely to match with users in the treatment group, and less likely to match with users in the control group.  As a driver can only match with one user at a time, treatment trips increase and control trips decrease.  This is cannibalisation, and measuring the difference in trips taken between treatment and control groups would be biased by it.

So, it is important to ask: **do user interactions matter?**  If the answer is yes, then we need to choose a method that takes them into account.
<br><br>

### **5. Map**
Below pulls the questions outlined above together into a useful framework.  This is by no means an complete list of methods, but aims to provide some structure and insight.

![](https://i.imgur.com/hus5si9.png)
<br><br>

-----------------------
## **AB Testing in Practice**
Below outlines the workflow for running an AB test.  Let’s cover this first, and then we will get to what to do once the test has been run.

![](https://i.imgur.com/CUcyvAA.png){:height="60%" width="60%"}
<br><br>

### **1. Power Analysis**
It is good practice to first calculate the minimum sample size that you will need to draw a conclusion from the experiment.  Once we know the sample size needed, we can calculate how long we need to run a test for.  This is important for two reasons:  (1) There are opportunity and operational costs to running a test.  Thinking about these in relation to how long it takes to run a test are important.  (2) It sets the benchmark for how long the test needs to run before any conclusions can begin to be drawn from the data.  This is the ‘no-peeking’ rule.

![](https://i.imgur.com/qKKGlTn.png){:height="30%" width="30%"}

Assumptions needed to estimate the required sample size:
- **Minimum detectable effect (x-u)** — this is the smallest lift to the metric that we care about discovering. There is trade-off; the smaller this number, the longer the test will need to be run.
- **Level of confidence (⍺)** —  ⍺ is the probability of a false positive.  There is a trade off between the P(false positive) and P(detecting true positive) (aka power), so this should be set with the specific test in mind. It’s common practise to set ⍺ at 5%
- **Sample variance (s)** —  this is typically the variance in the metric prior to the test (or the base level proportion prior to the test for proportional data)

<span style="color:#d25b97">No-Peeking Intuition: in the early stages of an experiment, the results often show up as significant. This is because there are two-competing forces: (1) the small sample size (n) reduces the size of the test statistic, and (2) the effect size (x-u) can often be huge, which increases the test statistic.  It would be wrong to stop the test at this point and draw a conclusion.  This is why it is often suggested that you not look at the results until you reach the required sample size.</span>
<br><br>

### **2. Checks**
Once the needed amount of data has been collected (see power analysis), it’s time to begin to draw a conclusion.  The first step is to run a few checks on the data to make sure that your conclusions are going to be valid.  These are:
- **Randomisation** — randomisation is how we are able to overcome selection bias and draw causal inferences from the experiment.  It’s therefore important to validate in as much as you can that the randomisation you carried out worked.  This means asking questions like those listed below (note: if the answer to these questions is ‘no’, then the experiment may not be valid):
  - are the group sizes the correct size
  - are observables even across groups
  - are the pre-experiment trends of the groups the same
- **Outliers** — are there one or two values that drive the entire difference in the metric across groups?
- **Skewness** — the t-test is an appropriate test to use under certain assumptions, one of those being that the data is normally distributed (or the sample is large enough to approximate it).  When this is violated (eg. spend/customer which is heavily right skewed and has lots of 0’s), we can use techniques that do not rely on certain distributional assumptions (MWW test)
- **Corrections** — if alpha=5%, then we would expect to see a false positive once in every 20 tests. So, if you are testing many variants, there is a correction that needs to be made to reduce the chances of a false positive.  But the best solution is not to run many variants.
<br><br>

### **3. What test?**

![](https://i.imgur.com/TWQiASK.png){:height="60%" width="60%"}

### **4. Conclusions**
Once you have reached this point, you are ready to draw a conclusion from the experiment.  There are 2 cases:
- p-value <= alpha — congratulations, there is an effect!
- p-value > alpha — in this case, we need to check the power of the test. Here, Power = 1 - P(false negative)
  - If the power is low, then P(false negative) is high. In this case, the test is inconclusive
  - If the power is high, then P(false negative) is low. We can conclude there is no effect

### **5. External Validity**
Lastly, it is worth noting that the results of the test are only really true for the test itself.  There is the chance that when fully released the feature may under/over-perform relative to the test.

<span style="color:#d25b97">Intuition: let’s say a company AB tests a price increase.  Rather than increase prices on some existing users for the test, they find it easier to test on new customers as they join.  The test shows that these users are price insensitive.  When the company rolls out the new higher price to all users, they see a dip in demand.  In this case, it is because the test was not valid for existing users.  It could easily be the case that existing users are actually quite price sensitive, which is why they were early adopters of the product in the first place.</span>
<br><br>

-----------------------
# **ELI5 Hypothesis testing**

### **Test Statistic**
you can construct a test-statistic with a known distribution (under certain assumptions) based on your data and what you want to test.  Hypothesis testing uses this known distribution to evaluate whether your hypothesis is likely to be true or not given the data you observed.

### **Hypotheses**
- Null Hypothesis (H0) is typically the hypothesis that there is no effect (eg. the feature does not increase user engagement).  
- Alternative Hypothesis (H1) is what you are trying to prove (eg. the feature does increase user engagement)

![](https://i.imgur.com/HFU242M.png){:height="60%" width="60%"}<br>
![](https://i.imgur.com/zxrcvPW.png){:height="40%" width="40%"}

### **Type I error**
- False positive
- Type I error = Event = (reject Ho `|` Ho is true) = (claim effect `|` there is no effect)
- P(type I error) = P(reject Ho `|` Ho is true) = P(claim effect `|` there is no effect) = **⍺**
- <span style="color:#d25b97">Intuition — claim the feature does increase engagement when in fact it does not.</span>

### **Type II error**
- False negative
- Type II error = Event = (don’t reject Ho `|` Ho is false) = (claim no effect `|` there is an effect)
- P(type II error) = P(don’t reject Ho `|` Ho is false) = P(claim no effect `|` there is an effect) = **β**
- <span style="color:#d25b97">Intuition — claim the feature does not increase engagement when in fact it does.</span>
- Note that β totally depends on h1 — there is a different β for all levels of H1 you choose!

![](https://i.imgur.com/mFwfeaF.png){:height="60%" width="60%"}

### **Power of the test**
- Power = P(reject Ho `|` Ho is false) = P(claim effect `|` there is an effect) = (1-β)
- <span style="color:#d25b97">Intuition —  correctly claim the feature increases engagement</span>
- The choices we make in the power analysis directly impact the power of a test:
  - ⍺ — the lower alpha, the higher the power of the test. This is because it makes it easier to reject H0, but at the cost of increasing the P(type 1 error) ie. false positives
  - n — collecting more data reduces the variance of the test statistic, thereby increasing the power of the test
  - H1 — the alternative hypothesis is the minimum detectable effect (x-u) from the power analysis. The smaller the MDE, the smaller the power of the test (see figure below)

[Pic 3]

### **P-Value**
- P(result >= observed result `|` there is no effect)
- Definition — The P-value associated with an observed test statistic is the probability of getting a value for that test statistic as extreme as or more extreme than what was actually observed (relative to H1) given that H0 is true.
- Link to video of academics answering this question
- <span style="color:#d25b97">Intuition — Imagine that you have a coin that you suspect is weighted toward heads.  Your null hypothesis is then that the coin is fair.  You flip it 100 times and get more heads than tails.  The p-value won’t tell you whether the coin is fair, but it will tell you the probability that you’d get at least as many heads as you did if the coin was fair. </span>

### **Confidence interval**
Intuition — Say you want to measure the average height of adults in the uk.  You can measure everyone, and know it exactly.

But that’s not feasible, so you ask a sample of people.  The average height from that sample (sample average) may differ from the true average height (population average).  The CI reflects that uncertainty. How:
The Central Limit Theorem allows us to say that the average (proportion) of the sample follows a normal distribution centered on the true population average with standard deviation where sigma is the standard deviation of the population and n is the size of the sample.

Using this normal distribution, we are able to calculate a range for the average height around our sample average. This is called a confidence interval.
What affects width of CI?
- The variation in actual population — the more diversity there is in the population, the less accurate your sample proportion will be
- The sample size — to increase accuracy, you can take a larger sample.  The bigger the sample you take, the closer to having a good representation of everyone in the UK. But after a while, you start getting diminishing returns. Adding one more person to the sample doesn't add as much as the person before, and so on
- The confidence level chosen — the more accurate we want to be, the wider the range

Is the P(confidence interval includes the true average height) = 95% (if we chose that level)?
No! I don’t have an intuitive answer why
Consider the case where we did not choose the sample at random. What if we chose to measure the heights of the local basketball team and use that as the average height? It remains true however that the bigger the sample you take, the closer to having a good representation of everyone in the UK.


### **One sided vs. Two sided**
Using a one sided test increases the power of the test. Similar to choosing a lower ⍺, this is because it makes it easier to reject H0, but at the cost of increasing the P(type 1 error) ie. false positives.


### **Unequal groups**
Choosing unequal groups reduces the power of the test.  This happens because it increases the variance of the test statistic.  For intuition, look at the sample-sd formula for a 2-sample T-test.  The term is minimised when n1=n2.


### **Missing values**
One thing to be careful of are cases when there are missing values. For example, testing the time to complete a task. In this case, we only observe the time to complete for users who completed the task.
P-value = P(result >= observed result|there is no effect, user completed task)


## **Further reading**
- [Measurement & analysis of feed-ranking models on Instagram](https://www.facebook.com/atscaleevents/videos/vb.1576488989290866/1856120757994353/?type=2&theater)
- [The pitfalls of A/B testing in social networks](https://tech.okcupid.com/the-pitfalls-of-a-b-testing-in-social-networks/)
- [Detecting Network Effects: Randomizing Over Randomized Experiments](http://www.kdd.org/kdd2017/papers/view/detecting-network-effects-randomizing-over-randomized-experiments)
- [Estimating peer effects in networks with peer encouragement designs](http://www.pnas.org/content/113/27/7316.full)

<br>
<br>
