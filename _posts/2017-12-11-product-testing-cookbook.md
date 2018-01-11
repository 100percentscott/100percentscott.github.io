---
layout: post
title:  causality cookbook
date:   2017-12-11 10:30:00
---
<br/>
![](https://i.imgur.com/WiwWoSn.png?1){:height="50%" width="50%"}

## **Question**
We often want to know the effect of X on Y.  This is causal inference.  It’s a problem that can come up in lots situations.  Most commonly when we plan to make a change to a product, and we want to know how it will effect a set of outcomes we care about. For example:
- How will splitting a signup form across several pages affect conversion rates and contact rates?
- How does a new app screen affect driver positioning?
- How does a cancellation fee affect user retention?

This post outlines some thinking to help approach these problems.
<br><br>

## **Mechanism**
First, I find helpful is to clearly define what the causal **relationship of interest** is, and to outline through what **mechanism** it works.  The relationship of interest is important because it determines what metrics you will look at, and at what level you will randomise (if possible).  The mechanism is important because if you can’t convincingly explain it in simple terms, then you are at risk of wasting your time, or worse, identifying a spurious effect (ie. bullshit).

The good news is that if it’s a product change you will already have a hypothesis (validated with users and data) here -- it’s the reason you want to change the product.
<br><br>

## **Randomisation, the gold standard**
Second, the key question now should be: **is randomisation is possible?** If yes, there are experimental techniques available.  If no, there are non-experimental techniques available which are a little less clean.  Fortunately, you can randomise well most of the time in product.

Aside: to understand causality, the goal is to overcome **selection bias**.  An example: Do hospitals make people healthier?  To answer this we could compare the health of people who have and have not been to hospital in the past year.  We’d learn that people who have not been to hospital are healthier, and might conclude that hospitals make people sick.  Of course, this is not the case.  Sick people choose to go to hospital.  This is selection bias.  This is why correlation ≠ causation.

**Randomisation solves the selection problem**.  That is why it is the gold standard.  If we randomly assign users into the treatment group (go to hospital) and control group (do not go to hospital), then we can be sure that users don’t select into a group based on other factors (eg. sickness, or some other unobservable factor).  This is an example of **user-level randomisation**.  Randomisation can be done at other levels too (eg. time, region, social group)
<br><br>

## **Networks and Marketplaces**
Networks and marketplaces are special cases worth calling out here.

From [okcupid](https://tech.okcupid.com/the-pitfalls-of-a-b-testing-in-social-networks/): “unfortunately, if you're doing tests for a product that relies heavily on **interaction between users** -- such as a dating app -- doing random assignment on a per-user basis can lead to unreliable experiments and misleading conclusions… Here's an example: Let's say one of our devs built a new video-chat feature and wanted to test if people liked it before launching it to all of our users. I could do an A/B test that randomly gave video-chat to one half of our users... but who would they use the feature with? ”.

Even if we overcame the logistical challenge, there remains the problems of **cannibalisation**, and **contamination**.  For example, suppose a ride-hailing app tests a price change.  It randomly assigns users to a treatment group (new lower price) and a control group (old price).  There is now more demand for cars from users in the treatment group because it’s cheaper.  As a result drivers are now more likely to match with users in the treatment group, and less likely to match with users in the control group.  As a driver can only match with one user at a time, treatment trips increase and control trips decrease.  This is cannibalisation, and measuring the difference in trips taken between treatment and control groups would be biased by it.
<br><br>

## **Framework**
![](https://i.imgur.com/hus5si9.png)
<br><br>

## **AB Testing in Practice**
![](https://i.imgur.com/TbmfEpa.png)
