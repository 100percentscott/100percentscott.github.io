---
layout: post
title:  causality cookbook
date:   2017-12-11 10:30:00
---
<br/>
![](https://i.imgur.com/WiwWoSn.png?1){:height="50%" width="50%"}

## **Question**
We often want to know the effect of X on Y.  This is called causal inference.  It’s a problem that can come up in lots situations.  Most commonly when we plan to make a change to a product, and we want to know how it will effect a set of outcomes we care about. For example:
- How does a new form affect contact rates?
- How does a new app screen affect driver positioning?
- How does a cancellation fee affect user retention?

This post outlines some thinking to help approach these problems.
<br><br>

## **Mechanism**
The first step that I find helpful is to clearly define what the causal relationship of interest is, and to think through what mechanism it works.  If it’s a product change, you should already have a strong hypothesis here that you have validated with users and data.  I believe that if you can’t convincingly explain the mechanism in simple terms, then you are at greater risk of identifying a spurious effect (ie. bullshit).
<br><br>

## **Randomisation, the gold standard**
To understand causality, the goal is to overcome **selection bias**.  An example: Do hospitals make people healthier?  We could compare the health of people who have and have not been to hospital in the past year.  We’d learn that people who have not been to hospital are healthier, and might conclude that hospitals make people sick.  Of course, this is not the case.  Sick people choose to go to hospital.  This is selection bias.  (aside: this example highlights why correlation ≠ causation).

**Randomisation solves the selection problem**.  That is why it is the gold standard.  If we randomly assign users into the treatment group (go to hospital) and control group (do not go to hospital), then we can be sure that users don’t select into a group based on other factors (eg. sickness, or some other unobservable factor).  This is an example of **user-level randomisation**.

Fortunately, you can randomise well most of the time in product.  However, there are times when we cannot randomise, such as when dealing with external shocks/events.  I’ll briefly cover solutions in this case.
<br><br>

## **Networks and Marketplaces**
There are a couple of special cases worth calling out.

**Networks** — [from okcupid](https://tech.okcupid.com/the-pitfalls-of-a-b-testing-in-social-networks/) “unfortunately, if you're doing tests for a product that relies heavily on interaction between users -- such as a dating app -- doing random assignment on a per-user basis can lead to unreliable experiments and misleading conclusions… Here's an example: Let's say one of our devs built a new video-chat feature and wanted to test if people liked it before launching it to all of our users. I could do an A/B test that randomly gave video-chat to one half of our users... but who would they use the feature with? ”.  This is true for social networks as well.

**Marketplaces** — similar to networks, but with additional problems of cannibalisation, and contamination.  For example, suppose a ride-hailing app wanted to test a price change.  It could randomly assign users to a treatment group (new lower price) and a control group (old price).  There is now more demand from users in the treatment group.
As a result drivers are now more likely to match with users in the treatment group, and less likely to match with users in the control group.  This is cannibalisation, and measuring the difference in trips taken between treatment and control groups would be biased.
<br><br>

## **Framework**
![](https://i.imgur.com/hus5si9.png)
