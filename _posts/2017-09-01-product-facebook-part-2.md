---
layout: post
title:  product @facebook - part 2
date:   2017-09-01 10:30:00
---
<br/>

The objective is to understand how FB thinks about and ultimately builds its products. <br>
Part 1 covers the company and the nature of their product. <br>
Part 2 runs through their iOS app. <br>
This is part 2.

-----------------------
# **News Feed**

### **A. What is the goal?**

![](https://i.imgur.com/B8mS4Hk.png){:height="50%" width="50%"}
<br>
Recall Mark Zuckerberg described newsfeed as the answer to the question ‘what is going on with the world around you?’. The mission of newsfeed is to connect people with the content that matters most to them across their social graph. As Chris Cox [puts it](https://youtu.be/8-Yhpz_SKiQ?t=3m19s) “What we are really trying to get to is a world where, if you were to stack rank the thousands of events that were going on in the world around you, and say these were the 20 that really mattered to me that i want to talk about with my friends and family over dinner or drinks at the end of the day — were able to deliver those things to you every single day reliably. For 2 billion people”
<br>
<br>
### **B. How does it work?**
Each time a user opens FB, newsfeed runs through the following algorithm in order to decide what to show you, and in what order.
<br>
<br>
**Step 1 — Inventory**<br>
<br>
The first step is to determine what stories and content have been published across your social graph. When you first sign up for FB, newsfeed is completely empty. The most significant input that determines what  appears in your newsfeed is the social graph that you map out on FB (ie.
the people you decide to friend, and the publishers, businesses, and pages that you decide to follow). As a result everybody’s newsfeed is unique.
<br><br>

![](https://i.imgur.com/5cVrklT.png)
<br>
**Step 2 — Signals**<br>
<br>
FB evaluates all of this content using a wide range of different signals. These are low-level predictions of how meaningful the content might be to a user. <span style="background-color: #70f5c7">First-order user needs</span> (<span style="background-color: #70f5c7">connect</span>, <span style="background-color: #70f5c7">communicate</span>, <span style="background-color: #70f5c7">discover</span>, <span style="background-color: #70f5c7">share</span>, and <span style="background-color: #70f5c7">entertain</span>) and <span style="background-color: #70f5c7">second-order user needs</span> (<span style="background-color: #70f5c7">convenient</span>, <span style="background-color: #70f5c7">fast</span>, <span style="background-color: #70f5c7">reliable</span>, <span style="background-color: #70f5c7">simple</span>) clearly inform what signals FB look for here.

- **AUTHOR**
  - Who posted the story? (eg. close friend > friend-of-friend)
  - How often do they post?
  - What feedback does the author get?
  - How complete is their profile page?
- **POST**
  - Content
    - What type of content is it (format - photo, video, notification, etc)
    - What is the content quality? (eg. sensational vs informative)
    - When was it posted (recency)
    - Is it urgent/immediate (notification system is likely different)
  - Activity
    - Does the post already have engagement?
    - Who engaged with the content? (social proof)
    - Average time spent on content
- **READER**
  - Context
    - What device are you using?
    - What is your connectivity like?
    - Where are you?
    - What are you doing?
    - Who are you with?
  - History
    - What format of content do you historically engage with?
    - Whose content do you engage with?
    - How much do you value discovery?
<br><br>

![](https://i.imgur.com/Z8ksH6s.png)<br>
**Step 3 — Predictions**
<br><br>
At this point FB predicts a user’s reaction toward each piece of content across several dimensions:

- **Engagement** — FB predicts your engagement with each piece of content. They do this because (1) engagement is correlated with user-value, and (2) engagement delivers network-value.
  - How likely are you to click the content?
  - How likely are you to spend time with the story?
  - How likely are you to like, comment, and share?
- **Value** - FB predicts how valuable you’ll find each piece of content. They do this in addition to predicting engagement because it is a direct measure of what matters most.
  - How likely are you to find the content informative?
  - How likely are you to find the content entertaining?
  - How likely are you to find the content new? (ie. discovery)
  - Other -
  - How likely is it that the content is clickbait? (eg. content where p(sharing) is lower after reading it)
  - How likely is it that the content contains nudity?


**Step 4 — Relevancy score**
FB consolidates the predictions made into a relevancy score, and orders all posts in newsfeed according to the score. Ads fit into the newsfeed product as sponsored content in addition to this organic content.
<br>
<br>

### **C. How does FB evaluate how they are doing?**

Recall that the mission of newsfeed is to connect people with the content that matters most to them across their social graph. To evaluate how well they are doing with newsfeed, here is a breakdown of what measures FB might look at:

- <span style="background-color: #70f5c7">**1st order** (what people do)</span>
  - **Engagement** — how much a user engages with the content in their newsfeed is correlated with how much they value it. FB can measure:
    - *Clicks*
    - *Likes/Reactions*
    - *Comments*
    - *Shares*
  - **Usage** — how much a someone uses newsfeed is likely correlated with how much value they get from using it. FB can measure:
    - *Time spent* - how long do users spend on a content (/session, /week, /month)
    - *DAU/MAU* - how often does the user engage with the news feed
    - *Growth accounting* - what state are the users in (active/inactive user of newsfeed), and how were the flows between them affected (new/churn/return)
  - **Content flags** — FB allows users to flag content of a certain type (eg. false news story, overly promotional content, etc), and flagging rates are tracked.

![](https://i.imgur.com/EuStobW.png)<br>

- <span style="background-color: #70f5c7">**2nd order** (what people say)</span>
  - **User preference** — FB does have a representative panel of users that they regularly poll (feed quality panel). They ask them to score how much they would like to see pieces of content in their newsfeed, and compare that with the score FB gives that content. This is an direct way to evaluate the algorithm with human input.
  - **Quality of time spent** — FB conducts an ongoing user survey (eg. NPS, or feedback survey) to establish how meaningful the time spent on newsfeed was for their users
- <span style="background-color: #70f5c7">**3rd order** (wider impact)</span>
  - **Network impact** — what types of reads and writes are users creating? Has this mix shifted due to changes? How have those changes impacted their networks in terms of engagement, usage, and quality of time spent? This is more nebulous than a single metric.

Again… just watching the above metrics is not sufficient to determine the causal impact of the newsfeed product. To do this, FB could do several things such as run an AB test. That is beyond the scope of this post, but I do cover causality & product testing in another post.

-----------------------
## **Write Prompt**

![](https://i.imgur.com/8xPProU.png){:height="50%" width="50%"}
### **A. What is the goal?**

FB places a prompt for the user to write at the top of the newsfeed screen on iOS. The feature is fixed at the top of the newsfeed, meaning it is mainly seen by the user when they first enter the FB app. There are a couple of goals for this feature:

1. <span style="background-color: #70f5c7">**Share**</span>: recall one of FBs core use cases is to “enable people to share what matters to them (ie. their opinions, ideas, photos and videos, and other activities) with audiences ranging from their closest friends to the public at large”. The immediate goal of the write prompt is to make it frictionless for a user to do this.<br>
2. <span style="background-color: #70f5c7">**Connect**</span>: recall FB is a service for connecting with what matters most to you across your social graph. A secondary goal of the prompt is to help users connect with their network. That means enabling users to share what matters to them in a way that resonates with their network. For example, FB might nudge a user to post a video instead of a photo because their audience is more likely to engage with a video (ie. watch, comment, like… ).

<br>
![](https://i.imgur.com/6HTwek0.png){:height="50%" width="50%"}

### **B. How does it work?**

There are a few things FB can alter dynamically (other than redesigning the tool): (1) **the text** in the box (“what’s on your mind?”), (2) **the order** of the format type buttons. <span style="background-color: #70f5c7">The goal is to make it as easy as possible for a user to post, and to help make those posts as meaningful as possible to the user</span>. The tool is mainly seen when a user first enters the FB app. At the time a user opens the app, FB may evaluate the following to determine how to show the prompt — with the aim of **predicting** the following questions: (a) **what are you most likely to want to post about?** (b) **who is most the meaningful audience (ie. likely to engage with) for that post?** (c) **what format is most likely to drive engagement?**:

- **Author**
  - Context
    - What device are you using?
    - What is your connectivity like?
    - Where are you?
    - What are you doing?
    - Who are you with?
  - History
    - Content (what)
      - What do you post about?
      - Behaviour (how)
      - How often do you post?
      - When do you post? (in the moment, following day, following month?)
      - What format do you post in?
    - Audience (to who)
      - Who engages with your posts?
      - What type of posts do they engage with?
      - How do they engage with your posts?
      - When do they engage your the posts?
      - How often do they engage with your posts?
      - What engagement is most meaningful to you?
- **Audience**
  - Context
    - What device are they using?
    - What is their connectivity like?
    - Where are they?
    - What are they doing?
    - Who are they with?

If a user does not post frequently, FB can match the user with a very similar user to infer the likelihood that the person will post, and the likelihood that their post will be engaged with etc, using the above.

<br>
### **C. How does FB evaluate how they are doing?**

The goal is to make it as easy as possible for a user to post, and to help make those posts as meaningful as possible to the user. To evaluate how well they are doing with the prompt, here is a breakdown of what measures FB might look at:
- <span style="background-color: #70f5c7">**1st order** (what people do)</span>
  - **Usage** - how much someone posts correlates with how much value they get from the feature. FB can measure:
    - *Posts per user* - how often does each user post /day, /week, /month
    - *Time to post* - how long does it take a user to post? Split by type
    - *Abandoned posts* - what % of posting attempts are unsuccessful
    - *Growth accounting* - what state are the users in (active/inactive poster), and how were the flows between them affected (new/churn/return)
  - **Engagement** — engagement correlates with value to both the author (ie. they connect) and the reader. FB can measure engagement /post (ie. is each post more likely to be engaged with) or /user (ie. is each user more likely to engage with posts), specifically looking at:
    - *Clicks*
    - *Likes/Reactions*
    - *Comments*
    - *Shares*
- <span style="background-color: #70f5c7">**2nd order** (what people say)</span>
  - **User preferences** — ask a set of users to create their own preferred post-prompt layout and compare their choice with FBs ranking (mirror newsfeed approach).
  - **Quality of time spent** — FB uses an ongoing user survey (eg. NPS, or feedback survey) to establish how meaningful time spent on FB was for their users. The goal of the post prompt is to enable users to share and connect — a core need. This metric is relevant to that.
- <span style="background-color: #70f5c7">**3rd order** (wider impact)</span>
  - **Network impact** — what types of reads and writes are users creating? Has this mix shifted due to changes in the feature? How have those changes impacted their networks in terms of engagement, usage, and quality of time spent? This is more nebulous than a single metric.

Just watching the above metrics is not sufficient to determine the causal impact of the post prompt product. To do this, FB could do several things such as run an AB test. That is beyond the scope of this post, but I do cover causality & product testing in another post.
<br>
<br>

-----------------------
## **Navigation**

-----------------------
## **Notifications**

-----------------------
## **Friends**

-----------------------
## **Groups**
