---
layout: post
title:  product — facebook (part 1)
date:   2017-09-01 10:30:00
---
<br/>

-----------------------
## **Intro**
![](https://i.imgur.com/PRa4WK9.png)
<br>
<br>
The purpose of this post is to understand how products are built at FB <br>
Part 1 covers the company and the nature of their products <br>
Part 2 is a breakdown of the FB iOS app <br>
<br>
This is part 1.
<br>
<br>

-----------------------
### **1.  A service for connecting**

In one sentence, FB is as a service for connecting. It’s an oversimplified, but useful paradigm. And FB shares this same view of themselves. Here’s how they describe their company in their 10k:


- We help people:
  - stay connected with **friends and family**
  - **discover and learn** about what is going on in the world around them
  - enable people to **share what matters** to them (ie. their opinions, ideas, photos and videos, and other activities) with audiences ranging from their closest friends to the public at large
  - **stay connected everywhere**
- Our top priority is to build **useful and engaging products**

<br>
Mark Zuckerberg gave a more nuanced view of FB [in 2013](https://youtu.be/c-E3cfPHjeY):

>“Our mission is to make the world more open and connected. And the way that we do this is by giving people tools so that they can <span style="background-color: #70f5c7">map out the stories of their lives and all of their connections</span>. We believe in this concept that we call the <span style="background-color: #70f5c7">social graph</span> – it’s the sum of all of these different connections in the world. And we believe that if we give people the tools to map out this graph, then that map that people build can be the basis for building all different kinds of <span style="background-color: #70f5c7">services for connecting</span>…
<br/>
<br/>
There are two primary kinds of services for connecting. There are ones that help you stay connected with people and things that you are already connected to. And there are ones that help you discover and make new connections. Most people think of Facebook primarily as the former, a service that helps people stay connected with people that they already know. But going back to the beginning of Facebook, way before newsfeed, the way that people used Facebook was actually to browse around and discover lots of new things in their network
<br/>
<br/>
…so, one way that we think about Facebook is as if it is this big community that’s producing this living database of all of this content and the stories of people's lives. Just like any database you should be able to query it. <span style="background-color: #70f5c7">We imagine that every screen of the Facebook product is the result of some query that someone is doing to learn about their network and the people around them</span>.
<br/>
<br/>
There are a few major use cases, and we call these the pillars of the Facebook product ecosystem. The first query that is really common that a lot of people want to do is they want to know ‘what is going on with the people around them? what is going on with the world?’. That’s NewsFeed. The content on this page is really the answer to the question ‘what is going on with the world around you?’. Another really common query that people want to do is ‘who is this person? tell me their story, tell me something about them’. And that’s timeline.”

<br/>
### **2. Social by design**

FB’s products are social by design. FB say so in their 10k: “Our product development philosophy is centered on products that are social by design, which means that **our products are designed to place people and their social interactions at the core of the product experience**”

**The social graph** is how FB frame people and their social interactions. The most intuitive way to think about the social graph is as follows: FB provides tools that let users map out the stories of their lives. The social graph is the digital representation of this map.

Here is Adam Mosseri talking about it [in 2010](https://youtu.be/bKZiXAFeBeY?t=15m):
> We talk a lot about the social graph internally and externally. The social graph is the digital representation on Facebook of real world entities – your relationship with a friend we call a friendship, you going to a party we call you rsvp-ing to an event, your football team is a group. we talk about the social graph as just objects and connections between objects within the system that represent real life entities… Writes are creations of objects or connections between objects, and reads are reads of that information…

<br/>
![](https://i.imgur.com/tcSJj08.png){:height="70%" width="70%"}
<br/>
<br/>
So how does FB leverage the social graph in their products?

We know that: (1) FB is a service for connecting, (2) FB products are social by design, (3) FBs top priority is to build useful and engaging products. This means that FB is going to use the social graph to connect. But more than just that, FB is going to use the social graph to determine what to connect, with the goal making its products useful and engaging. This turns out to be a really interesting problem.

As pointed out by Adam, not all elements of a user’s social graph are of equal value to them or their network — “the fact that you liked a comment (a type of write) is obviously less valuable than you telling us that you had a baby, or that you switched jobs. So clearly all writes were not created equal”.

A useful and engaging product is one that connects the right user to the right information/experience at the right time. To do this FB needs to quantify the user-value and network-value of every element of each user’s social graph. Only then can the right information/experience be surfaced to the user.

This poses two big challenges:
1. The technical challenge of **computing this at scale**. This is a O(n^2) problem at an enormous scale. This is out of the scope of this post, other than to flag this is where Friendster faulted. And to flag that this is where FB engineering is awesome.
2. The challenge of deciding **how to quantify** user-value and network-value. Here are two examples that show the nature of this problem:

![](https://i.imgur.com/bnoW6uY.png){:height="70%" width="70%"}

**Example #1: How should FB determine what friendships matter most to you?** FB could rank friendships according to something like Dunbar’s pyramid - which maps [Dunbar's number](https://en.wikipedia.org/wiki/Dunbar%27s_number) from strongest to weakest ties. The strength of the tie ideally captures the emotional and information-sharing content of the relationship. One way FB might measure this strength is by the frequency of writes between users. “It turns out that frequency of communication maps pretty cleanly on the subjective “friendship” or “liking” scale. After all, if you dislike someone, would you talk to them more often than you have to?” (Social Network Analysis)

**Example #2: How should FB rank posts when showing them to a user?** This turns out to be one of the core problems that NewsFeed solves, which I cover later. For now, these are some of the factors that FB might take into account:
- Relevance — do I care at all?
- Saliency — do I care right now? when is it? where am i? what am i doing?
- Source — who posted it? do I trust this person? Has it been corroborated?
- Format — is it a video? Is it a photo?
- Social Proof — who else has seen it? how have they reacted to it?
- Resonance — does the content of the post mesh with what I already believe in?
- Severity — how good or bad is the content of the post?
- Immediacy — does this post demand an immediate action? What is the consequence of inaction?
- Certainty — does the post cause certain pain or pleasure or is the chance low?
- Entertainment value — is it funny? is it a good read?
- Context — what else is happening at the moment?


<br/>
### **3. Use Cases & User Needs**

FB is a service for connecting with what matters most to you across your social graph. People use FB to:
- <span style="background-color: #70f5c7">**connect**</span>
- <span style="background-color: #70f5c7">**communicate**</span>
- <span style="background-color: #70f5c7">**discover**</span>
- <span style="background-color: #70f5c7">**share**</span>
- <span style="background-color: #70f5c7">**entertain**</span>

This is what FB tell us. For comparison, I surveyed 100 people on [mturk](https://www.mturk.com/mturk/welcome) (yes, it’s small and not representative). The results were surprisingly consistent with this, with a few nuances. Namely:
- connecting with friends & family — is by far the most common use of FB
- discovering news — is the top use of FB after connecting and communicating with people
- connecting != communicating — though most people use FB to stay connected with friends & family, they are likely using other platforms to directly communicate with them. My guess is that people see messenger or whatsapp as distinct from FB here
- few use FB to share content (10%) — according to [Adam Mosseri](https://youtu.be/bKZiXAFeBeY?t=16m40s): “we found that 85% of the content in the system was generated by […] around 20% of users in the system”. Again, my guess is that people see messenger/whatsapp/instagram as distinct from FB here

![](https://i.imgur.com/IZjTjhS.png){:height="50%" width="50%"}

There are second-order user needs to consider. **What is the causal mechanism behind why someone would choose to use FB at any given moment?**

FB address this in their 10k “we compete with companies that... provide social and communication products and services that are designed to engage users and capture time spent on mobile devices and online”

FB wins if it meets an additional set of basic user needs:
- it is **convenient** to use (eg. apps work on all devices)
- it is **fast/reliable** (eg. quick load times, works in high/low connectivity)
- it is **simple** to use (eg. upload a photo, comment)
- a user’s **social graph is engaged** (ie. present, active, and responsive. This means, for instance, they post/engage with content, respond to direct messages quickly, etc)

There are more levels below this, but for the purpose of this post, this gives a sense of what user considerations influence product decisions.

<br/>
### **4. Engagement is critical**

![](https://i.imgur.com/wU9atQP.png){:height="50%" width="50%"}

Engagement is critical to FB. FB point this out in their 10k: “The size of our user base and our users’ level of engagement are critical to our success.” It’s key to FB for several reasons:

- **Growth** – the more people on the platform, the more useful the platform is to all users
- **User Experience** – the more engaged users are, the more they read and write, and the more responsive they are. This makes it easier to connect each user to a meaningful experience - whether that is surfacing a new post from an interest group, or posting a photo that quickly gets liked by your friends.
- **Content** – time and attention spent on the platform attracts content
- **Revenue** – time and attention spent on the platform drives ad revenue. FB in their 10k: “we generate substantially all of our revenue from selling advertising placements to marketers. Our ads let marketers reach people based on a variety of factors including age, gender, location, interests, and behaviors. Marketers purchase ads that can appear in multiple places including on FB, Instagram, and third-party applications and websites.”

<br/>
### **5. Stakeholders**

FB is a multi-billion dollar company, which means it has lots of different stakeholders. It follows that the needs of those stakeholders will sometimes be important factors when product decisions are made. A good outline of that is made by [Adam Mosseri in 2010](https://youtu.be/bKZiXAFeBeY?t=12m53s):
> At Facebook, in product, there is a healthy skepticism of being overly data driven. It is very difficult for a set of metrics to fully represent what you value. There are a lot of factors that go into making any sort of product decision. Quantitative data is one [], qualitative data is another, **strategic interests** are another, **user interests** are another (what people complain about, what people ask for), **network interests** (which are significantly different), **competition** clearly factors into our decision making, **regulatory bodies** at this point (at our scale we have to deal with privacy advocacy groups, the EU...), and **business interests** (explicitly we value revenue generation right now less than growth and engagement. Growth being defined by how many users come onto the site, engagement being defined by how often users use the site). So, these are all important factors that we use in making our decisions

<br/>
### **6. Perverse outcomes**

A thorny challenge that FB faces is the abuse of their products. FB products need to not only be built with the most optimistic use cases in mind, but also with the dangers of their misuse in mind. Some examples of where FB product thinking addresses these issues in public are:
- **Offensive content** - “The idea is to give everyone in the community options for how they would like to set the content policy for themselves. Where is your line on nudity? On violence? On graphic content? On profanity? What you decide will be your personal settings. We will periodically ask you these questions to increase participation and so you don’t need to dig around to find them. For those who don’t make a decision, the default will be whatever the majority of people in your region selected, like a referendum. Of course you will always be free to update your personal settings anytime.”
- **Polarization** - “Research shows that some of the most obvious ideas, like showing people an article from the opposite perspective, actually deepen polarization by framing other perspectives as foreign. A more effective approach is to show a range of perspectives, let people see where their views are on a spectrum and come to a conclusion on what they think is right… the best solutions for improving discourse may come from getting to know each other as whole people instead of just opinions – something FB may be uniquely suited to do.”
- **Clickbait** - “In general, if you become less likely to share a story after reading it, that’s a good sign the headline was sensational. If you’re more likely to share a story after reading it, that’s often a sign of good in-depth content. We recently started reducing sensationalism in News Feed by taking this into account for pieces of content, and going forward signals like this will identify sensational publishers as well”


<br/>
### **7. Summary**
- FB is a service for connecting
- Social is core to the product experience (FB is a network)
- Engagement is critical
- First order user needs to:
  1. connect
  2. communicate
  3. discover
  4. share
  5. entertain
- Non-user interests matter (but less)
- Perverse outcomes matter
<br/>
<br/>
<br/>
