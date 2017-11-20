---
layout: post
title:  product @facebook
date:   2017-09-01 10:30:00
---
<br/>

-----------------------
## **Intro**
<span style="background-color: #70e1f5">[ My aim is to understand how FB approaches it’s products ]</span>. I’ll do this by running through their iOS app. Along the way I’ll link to content I found helpful. The rest of the post is as follows:
- A. Facebook
  1. [mission](#mission)
  2. [social graph](#social graph)
  3. [problem/solution space](#problem/solution space)
  4. [stakeholders](#stakeholders)
  5. [engagement](#engagement)
  6. [abuse/misuse](#abuse/misuse)
  7. [summary](#summary)
- B. iOS app
  1. [navigation](#navigation)
  2. [newsfeed](#newsfeed)
  3. [friends](#friends)
  4. [profile & timeline](#profile & timeline)
  5. [events](#events)
  6. [groups](#groups)
  7. [notifications](#notifications)
  <br/>
  <br/>

-----------------------
## **A. Facebook**

<a name="mission"></a>
### **1. Mission**
<span style="background-color: #70e1f5">[ product is mission ]</span>
I started by reading [FBs 10k](https://s21.q4cdn.com/399680738/files/doc_financials/annual_reports/FB_AR_2016_FINAL.pdf). Here I learned FB has a recently renewed mission... "Give people the power to build community and bring the world closer together". It used to be the longer "Facebook’s mission is to give people the power to share and make the world more open and connected. People use Facebook to stay connected with friends and family, to what’s going on in the world, and to share and express what matters to them." These statements are a concise articulation of FBs product vision, and reflect how their products are actually used. I found that positively surprising given how vapid mission statements can be.  
<br/>
Reading on, FB outlines more in their 2015 and 2016 10ks:

- Our top priority is to build useful and engaging products
- We also help people
  - discover and learn about what is going on in the world around them
  - enable people to share their opinions, ideas, photos and videos, and other activities with audiences ranging from their closest friends to the public at large
  - stay connected everywhere
- Our product development philosophy is centered on products that are social by design, which means that our products are designed to place people and their social interactions at the core of the product experience
- The size of our user base and our users' level of engagement are critical to our success.
- We generate substantially all of our revenue from selling advertising placements to marketers. Our ads let marketers reach people based on a variety of factors including age, gender, location, interests, and behaviors. Marketers purchase ads that can appear in multiple places including on Facebook, Instagram, and third-party applications and websites.
- We compete with companies that sell advertising, as well as with companies that provide social and communication products and services that are designed to engage users and capture time spent on mobile devices and online

<br/>
That gives a pretty good sense of the frame through which FB views it's products. A more nuanced view that stood out to me came from [Mark in 2013]((https://youtu.be/c-E3cfPHjeY)):

>“Our mission is to make the world more open and connected. And the way that we do this is by giving people tools so that they can map out the stories of their lives and all of their connections. We believe in this concept that we call the social graph -- it's the sum of all of these different connections in the world. And we believe that if we give people the tools to map out this graph, then that map that people build can be the basis for building all different kinds of services for connecting...
<br/>
<br/>
There are two primary kinds of services for connecting. There are ones that help you stay connected with people and things that you are already connected to. And there are ones that help you discover and make new connections. Most people think of Facebook primarily as the former, a service that helps people stay connected with people that they already know. But going back to the beginning of Facebook, way before newsfeed, the way that people used Facebook was actually to browse around and discover lots of new things in their network
<br/>
<br/>
...so, one way that we think about Facebook is as if it is this big community that's producing this living database of all of this content and the stories of peoples lives. Just like any database you should be able to query it. We imagine that every screen of the Facebook product is the result of some query that someone is doing to learn about their network and the people around them.
<br/>
<br/>
There are a few major use cases, and we call these the pillars of the Facebook product ecosystem. The first query that is really common that a lot of people want to do is they want to know 'what is going on with the people around them? what is going on with the world?'. That's NewsFeed. The content on this page is really the answer to the question 'what is going on with the world around you?'. Another really common query that people want to do is 'who is this person? tell me their story, tell me something about them'. And that's timeline."

<br/><a name="social graph"></a>
### **2. Social Graph**
<span style="background-color: #70e1f5">[ social is core to the product experience ]</span>
That brings us onto the social graph -- the core of FBs product and a major source of their competitive advantage. Understanding the social graph is critical to understanding how products are thought about at FB. Adam Mosseri talked about it in this [video in 2010](https://www.youtube.com/watch?v=bKZiXAFeBeY):(15min)
<br/>
>We talk a lot about the social graph internally and externally. The social graph is the digital representation on Facebook of real world entities -- your relationship with a friend we call a friendship, you going to a party we call you rsvp-ing to an event, your football team is a group. we talk about the social graph as just objects and connections between objects within the system that represent real life entities... Writes are creations of objects or connections between objects, and reads are reads of that information...
<br/>
<br/>
...this type of write - the fact that you liked a comment - is obviously less valuable than you telling us that you had a baby, or that you switched jobs. So clearly all writes were not created equal.

<br/>
![](https://i.imgur.com/CqrkhL1.png){:height="70%" width="70%"}
<br/>
<br/>
The image above illustrates the social graph using social network theory terminology. As pointed out by Adam, not all nodes, edges, fields, reads, or writes are of equal value to a user or their network. Therefore, FB must quantify the user-value and network-value of the different elements of each users graph to be in a position to offer a great product experience. A great product experience means surfacing the right information/experience to the right user at the right time, and can apply both to reads and writes. Here are two quick examples for illustration:
<br/>
<br/>*Example #1*: How should FB determine what friendships matter most to you? Should they rank friendships according to something like Dunbar's pyramid - which maps [Dunbar's number](https://en.wikipedia.org/wiki/Dunbar%27s_number) from strong to weak ties? 'As you go down the pyramid, the emotional and information-sharing content of the relationships decrease, and the number of relationships increase'. Or should they use the frequency of writes between users? 'It turns out that frequency of communication maps pretty cleanly on the subjective “friendship” or “liking” scale. After all, if you dislike someone, would you talk to them more often then you have to?'. Or something else?
<br/>
![](https://i.imgur.com/derydGR.png){:height="50%" width="50%"}
<br/>
*Example #2*: In what order should FB rank posts when showing them to a user? That might depend on:
- Relevance - do I care at all?
- Saliency — do I care right now? when is it? where am i? what am i doing?
- Source - who posted it? do I trust this person? Has it been corroborated?
- Format - is it a video? Is it a photo?
- Social Proof - who else has seen it? how have they reacted to it?
- Resonance - does the content of the post mesh with what I already believe in?
- Severity - how good or bad is the content of the post?
- Immediacy - does this post demand an immediate action? What is the consequence of inaction?
- Certainty - does the post cause certain pain or pleasure or is the chance low?
- Entertainment value - is it funny? A good read?
- Context - what else is happening at the moment?

Again, these are just quick examples. We'll see how FB approaches this as we run through the individual product breakdowns. But what is clear is that valuing the elements of a user's social graph is core to FB's product experience. It is what allows FB to master the 'science of addiction'.

<br/><a name="problem/solution space"></a>
### **3. Problem/Solution Space**
<span style="background-color: #70e1f5">[ users first ]</span>
Now that we have a good sense of FBs goal and the nature of their product, what about their users? Products are built to be used by people. And FB employs lots of researchers to understand what their users' needs are, and the mechanisms behind why & how they use FB. We'll infer from looking at their products what user problems FB believe they're solving. For comparison, I surveyed 100 people on [mturk](https://www.mturk.com/mturk/welcome). Yes, it's small and not representative, but it does gives some insight. Here's what they said:
<br/>
<br/>![](https://i.imgur.com/Fn5ZPwy.png)
<br/> Some observations:
- Connecting with friends & family is by far the most common use of FB
- Though most people use FB to stay connected with friends & family, they are likely using other platforms to directly communicate with them (messenger, whatsapp, etc)
- Only a small share of users say they use FB to share content (10%). According to [Adam Mosseri](https://youtu.be/bKZiXAFeBeY?t=16m40s): "we found that 85% of the content in the system was generated by [...] around 20% of users in the system". So this might make sense, though that could change significantly if Instagram were included.
- Discovering news is the top use of FB after connecting and communicating with people

The top high-level user needs seem to be to: (1) connect, (2) communicate, (3) discover, (4) share, and (5) entertain. (Coincidentally these exact needs are also listed in their 10k… and many people’s responses echoed FBs mission statement word for word)

But why use FB? At any given moment a person must choose to use FB. The reasons why they choose to use FB in that moment (I suspect) is different from what they use FB for — recall people mostly say they use FB to connect with the people & content that matter to them. I have no specific data, but would expect to see reasons such as: to take a break at work, to occupy time on a commute, to discover funny videos, to update their family on a new event, etc.

In each of these cases a person chooses FB over other products and experiences that compete to capture their time and attention (sleep is often an example here). FB wins if it meets a basic set of user needs:
- (1) it is convenient to use (eg. apps work on all devices)
- (2) it is fast/reliable (eg. quick load times, works in high/low connectivity)
- (3) it is simple to use (eg. upload a photo, comment)
- (4) their social graph is present, active, and responsive (eg. post/engage with content, respond to direct messages quickly)

Many of these needs are taken for granted at the scale of FB, and there of course more levels to this. But for the purpose of this post it gives a sense of what user considerations influence product decisions.


<br/><a name="stakeholders"></a>
### **4. Stakeholders**
<span style="background-color: #70e1f5">[ other interests influence product ]</span>
FB is a multi-billion dollar company, which means it has lots of different stakeholders. It follows that the needs of those stakeholders will sometimes be important factors when product decisions are made. A good outline of that is made by [Adam Mosseri in 2010](https://www.youtube.com/watch?v=bKZiXAFeBeY) [12m53]:
> At Facebook, in product, there is a healthy skepticism of being overly data driven. It is very difficult for a set of metrics to fully represent what you value. There are a lot of factors that go into making any sort of product decision. Quantitative data is one [], qualitative data is another, **strategic interests** are another, **user interests** are another (what people complain about, what people ask for), **network interests** (which are significantly different), **competition** clearly factors into our decision making, **regulatory bodies** at this point (at our scale we have to deal with privacy advocacy groups, the EU...), and **business interests** (explicitly we value revenue generation right now less than growth and engagement. Growth being defined by how many users come onto the site, engagement being defined by how often users use the site). So, these are all important factors that we use in making our decisions

<br/><a name="engagement"></a>
### **5. Engagement**
<span style="background-color: #70e1f5">[ the behaviour that matters most ]</span>
It is my understanding that engagement is one of the core focus' of product teams at FB. That is because engagement is the water that turns the wheel. It's key to the platform for several reasons:
- Growth -- the more people on the platform, the more useful the platform is to all users
- User Experience -- the more reads and writes on the platform, the easier it is to surface the right information or experience to the right user at the right time
- Content -- time and attention spent on the platform attracts good content from producers
- Revenue -- time and attention spent on the platform drives ad revenue

<br/>![](https://i.imgur.com/eIdQyjv.png){:height="50%" width="50%"}

<br/><a name="abuse/misuse"></a>
### **7. Abuse/Misuse**
<span style="background-color: #70e1f5">[ perverse outcomes matter ]</span>
A perhaps unique challenge that faces FB are the perverse outcomes that result from the misuse and abuse of their products. I suspect FB products are built with both the most optimistic use cases in mind, and the dangers of their misuse. Some examples of where product thinking addresses these issues in public:
- Offensive content - "The idea is to give everyone in the community options for how they would like to set the content policy for themselves. Where is your line on nudity? On violence? On graphic content? On profanity? What you decide will be your personal settings. We will periodically ask you these questions to increase participation and so you don't need to dig around to find them. For those who don't make a decision, the default will be whatever the majority of people in your region selected, like a referendum. Of course you will always be free to update your personal settings anytime."
- Polarization - "Research shows that some of the most obvious ideas, like showing people an article from the opposite perspective, actually deepen polarization by framing other perspectives as foreign. A more effective approach is to show a range of perspectives, let people see where their views are on a spectrum and come to a conclusion on what they think is right... the best solutions for improving discourse may come from getting to know each other as whole people instead of just opinions -- something Facebook may be uniquely suited to do."
- Click Bait - "In general, if you become less likely to share a story after reading it, that's a good sign the headline was sensational. If you're more likely to share a story after reading it, that's often a sign of good in-depth content. We recently started reducing sensationalism in News Feed by taking this into account for pieces of content, and going forward signals like this will identify sensational publishers as well"
- Political Ads - [here](https://newsroom.fb.com/news/2017/09/providing-congress-with-ads-linked-to-internet-research-agency/) and [here](https://newsroom.fb.com/news/2017/09/hard-questions-more-on-russian-ads/)

<br/>
<a name="summary"></a>
### **6. Summary**
- Mission drives product
- Social is core to the product experience
- Engagement is key
- Users come first
- User needs are to: (1) connect, (2) communicate, (3) discover, (4) share, (5) entertain
- Non-user interests matter (but less)
- Perverse outcomes matter

<br/>
<br/>

-----------------------
## **B. iOS App**
<a name="navigation"></a>
### **1. Navigation**
![](http://i.imgur.com/QwMxw7n.png){:height="70%" width="70%"}
<br/>
![](https://i.imgur.com/DL0kIOq.png){:height="70%" width="70%"}
<br/>
- Facebook is a bundle of separate but linked products that are social by design
- There are >30 separate products a user can navigate to through the iOS app menu.
- Every product that appears in a user's navigation menu is deliberate and purposeful. Why? Take 'City Guides' for eaxmple. According to my survey, 6% of FB users use 'City Guides'. With 2 billion DAUs, that makes 'City Guides' a product with 120 million DAUs. Even if i'm off by a factor of 100, that still makes it a product with 1.2 million DAUs.
- order: how does Facebook decide how to order the products in a user's navigation menu? newsfeed is the default start screen. the order changes. i index differently to the average user.
- messenger link
- contextual information
- notifications

*Use case:*
<br/>
*Metrics:*
- clicks
- time spent /product
- engagement /product
- efficiency (time spent in menu / #visits to menu)
<br/>
*Questions:*
- How should the products be ordered in the navigation menu?

-----------------------
<a name="newsfeed"></a>
## **NewsFeed**
*Use case:*
<br/>
- connect people with content that matters to them most
- discover
- entertain

*Metrics:*
<br/>
- time spent on feed
- engagement (likes, reactions, comments, shares)
- stories read (clicks, time /article)
- content consumed (clicks, time / post, reads, views, )
- sentiment
- retention

*Questions:*
- how should FB determine what prompt to place in the post box? (eg. what's on your mind?)
- how should content be ranked within NewsFeed


-----------------------
## **Friends**
*Use case:*
<br/>
*Metrics:*
<br/>
*Questions:*

-----------------------
## **Profile & Timeline**
*Use case:*
<br/>
*Metrics:*
<br/>
*Questions:*

-----------------------
## **Events**
*Use case:*
<br/>
*Metrics:*
<br/>
*Questions:*

-----------------------
## **Groups**
*Use case:*
<br/>
*Metrics:*
<br/>
*Questions:*

-----------------------
## **Notifications**
*Use case:*
<br/>
*Metrics:*
<br/>
*Questions:*

-----------------------
## **Videos**
First, a few videos that give great insight into product thinking @facebook:
- [Adam Mosseri - Data](https://www.youtube.com/watch?v=bKZiXAFeBeY)
- [Alex Schultz - Startup School](https://www.startupschool.org/?ref=producthunt)
- [FB - Graph Search](https://youtu.be/c-E3cfPHjeY)
- [Alex Schultz - Growth](http://original.livestream.com/f8industry/video?clipId=pla_a093cf1f-2d34-4e74-8377-9e54bc65d8e9&rt=1&ra=837233)
- [FB - Growth Accounting](https://www.facebook.com/FacebookforDevelopers/videos/3707283286197/)
- [Zuckerberg - 2005](https://www.youtube.com/watch?v=xFFs9UgOAlE)
- [FB - Reactions](https://developers.facebook.com/videos/f8-2017/how-we-shipped-reactions/)
- [FB - Growth](https://www.youtube.com/watch?v=0LjdplsQZoo)
- [Randy Edgar - PM Interview](https://www.youtube.com/watch?v=l43-_yXuZ-I)
- [FB - Push Notifications](https://www.youtube.com/watch?v=0K7AjHrK4TA)
- [FB - Analytics](https://www.youtube.com/watch?v=i9lGLnamtHs)
- [FB - NewsFeed 1](https://www.youtube.com/watch?v=8-Yhpz_SKiQ)
- [FB - NewsFeed 2](https://www.youtube.com/watch?v=LmN0A-KKK8M)

<br/>
<br/>

-----------------------
## **Glossary**
- Social Graph
- DAU - daily active user
- MAU - monthly active user
<br/>
<br/>
