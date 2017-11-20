---
layout: post
title:  product @facebook - part 1
date:   2017-09-01 10:30:00
---
<br/>

-----------------------
## **Intro**
![](https://i.imgur.com/PRa4WK9.png)
The objective is to understand how FB thinks about and ultimately builds its products. I’ll first cover the company and the nature of their product [Part 1]. I’ll then run through their iOS app [Part 2]
<br>
<br>

-----------------------
## **A. Facebook**

<a name="mission"></a>
### **1.  A service for connecting**

FB is a service for connecting. As you read this section it will become increasingly apparent that this is true. Much of the rest of this post then deals with the question of FB connecting ‘who’ with ‘what’ (and ‘what’ with ‘who’).

Let’s begin with the insights we garner from their 10k:
>- We help people:
  - stay connected with <span style="background-color: #70f5c7">friends and family</span>
  - <span style="background-color: #70f5c7">discover and learn</span> about what is going on in the world around them
  - enable people to <span style="background-color: #70f5c7">share what matters</span> to them (ie. their opinions, ideas, photos and videos, and other activities) with audiences ranging from their closest friends to the public at large
  - stay connected everywhere
- Our top priority is to build useful and engaging products
- Our product development philosophy is centered on <span style="background-color: #70f5c7">products that are social by design</span>, which means that our products are designed to place people and their social interactions at the core of the product experience
- The size of our user base and our users’ level of engagement are critical to our success.
- We generate substantially all of our revenue from selling advertising placements to marketers. Our ads let marketers reach people based on a variety of factors including age, gender, location, interests, and behaviors. Marketers purchase ads that can appear in multiple places including on FB, Instagram, and third-party applications and websites.
- We compete with companies that sell advertising, as well as with companies that provide social and communication products and services that are designed to engage users and capture time spent on mobile devices and online

<br>
That gives a pretty good sense of the frame through which FB views it’s products. A more nuanced view that stands out came from [Mark in 2013]((https://youtu.be/c-E3cfPHjeY)):

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


<br/><a name="social graph"></a>
### **2. Social by design**

FB provides tools that let users map out the stories of their lives. The social graph is the digital representation of this map. It is fundamental to how products are thought about at FB. Adam Mosseri talked about it in this [video in 2010](https://www.youtube.com/watch?v=bKZiXAFeBeY):(15min)
<br>
> We talk a lot about the social graph internally and externally. The social graph is the digital representation on Facebook of real world entities – your relationship with a friend we call a friendship, you going to a party we call you rsvp-ing to an event, your football team is a group. we talk about the social graph as just objects and connections between objects within the system that represent real life entities… Writes are creations of objects or connections between objects, and reads are reads of that information…

<br/>
![](https://i.imgur.com/tcSJj08.png){:height="70%" width="70%"}
<br/>
<br/>
The image above illustrates the social graph using terminology from social network analysis.

We know that <span style="background-color: #70f5c7">(1) FB is a service for connecting</span>, and <span style="background-color: #70f5c7">(2) FB products are social by design</span>. That means that FB is going to be either using the social graph to connect things, and/or connecting things within the social graph. We also know that <span style="background-color: #70f5c7">(3) FBs top priority is to build useful and engaging products</span>. That means FB needs to be able to determine what is useful and engaging from (or using) a social graph. This turns out to be a really interesting problem.

As pointed out by Adam, not all nodes, edges, fields, reads, or writes are of equal value to a user or their network — “the fact that you liked a comment (a type of write) is obviously less valuable than you telling us that you had a baby, or that you switched jobs. So clearly all writes were not created equal”. To build a great product — one that connects the right user to the right thing at the right time — FB must first quantify the <span style="background-color: #70f5c7">user-value</span> and <span style="background-color: #70f5c7">network-value</span> of every element of each user’s social graph.

This poses several challenges. There is the technical challenge of computing this at scale. This is out of the scope of this post, other than to flag this is where Friendster faulted. There is the challenge of deciding **how to quantify** user-value and network-value. I don’t have any special insights into FBs finely tuned ‘addiction’ engine here. I’ll have to infer how FB approaches this as we run through the individual product breakdowns. Here, however, are two examples for illustrative purposes:

![](https://i.imgur.com/bnoW6uY.png){:height="70%" width="70%"}

**Example #1**: How should FB determine what friendships matter most to you? They could rank friendships according to something like Dunbar’s pyramid - which maps [Dunbar's number](https://en.wikipedia.org/wiki/Dunbar%27s_number) from strong to weak ties. As you go down the pyramid, the emotional and information-sharing content of the relationships decrease, and the number of relationships increase. Or they could use the frequency of writes between users. ‘It turns out that frequency of communication maps pretty cleanly on the subjective “friendship” or “liking” scale. After all, if you dislike someone, would you talk to them more often then you have to?’
(note: see Social Network Analysis)

**Example #2**: How should FB rank posts when showing them to a user? FB might take the following into account:
- Relevance - do I care at all?
- Saliency — do I care right now? when is it? where am i? what am i doing?
- Source - who posted it? do I trust this person? Has it been corroborated?
- Format - is it a video? Is it a photo?
- Social Proof - who else has seen it? how have they reacted to it?
- Resonance - does the content of the post mesh with what I already believe in?
- Severity - how good or bad is the content of the post?
- Immediacy - does this post demand an immediate action? What is the consequence of inaction?
- Certainty - does the post cause certain pain or pleasure or is the chance low?
- Entertainment value - is it funny? is it a good read?
- Context - what else is happening at the moment?



<br/><a name="problem/solution space"></a>
### **3. Use Cases**

We know from their 10k that FB sees **these** as among their major use cases. For comparison, I surveyed 100 people on [mturk](https://www.mturk.com/mturk/welcome) (yes, it’s small and not representative). The results were surprisingly consistent with what FB state in their 10k, with a few nuances. Namely:
- connecting with friends & family is by far the most common use of FB
- discovering news is the top use of FB after connecting and communicating with people
- connecting != directly communicating. Though most people use FB to stay connected with friends & family, they are likely using other platforms to directly communicate with them. My guess is that people see messenger or whatsapp as distinct from FB here
- only a small share of users say they use FB to share content (10%). According to Adam Mosseri: “we found that 85% of the content in the system was generated by […] around 20% of users in the system”. Again, my guess is that people see messenger/whatsapp/instagram as distinct from FB here

![](https://i.imgur.com/IZjTjhS.png){:height="50%" width="50%"}

Simplifying this, FB is a service for connecting with what matters most to you across your social graph. People use it to: (1) <span style="background-color: #70f5c7">connect</span>, (2) <span style="background-color: #70f5c7">communicate</span>, (3) <span style="background-color: #70f5c7">discover</span>, (4) <span style="background-color: #70f5c7">share</span>, and (5) <span style="background-color: #70f5c7">entertain</span>.

There are second-order use cases and needs too. What about the causal mechanism behind why someone would choose to use FB at any given moment? I have no specific data, but would expect to see reasons such as: to take a break at work, to occupy time on a commute, to discover funny videos when bored, to update their family on a new event, etc.

In each of these cases a person chooses FB over other products and experiences that compete to capture their time and attention (sleep is often an example here). FB wins if it meets a set of basic user needs in addition to those listed above:
1. it is <span style="background-color: #70f5c7">convenient</span> to use (eg. apps work on all devices)
2. it is <span style="background-color: #70f5c7">fast/reliable</span> (eg. quick load times, works in high/low connectivity)
3. it is <span style="background-color: #70f5c7">simple</span> to use (eg. upload a photo, comment)
4. their social graph is <span style="background-color: #70f5c7">present</span>, <span style="background-color: #70f5c7">active</span>, and <span style="background-color: #70f5c7">responsive</span> (eg. post/engage with content, respond to direct messages quickly)

There are more levels below this, but for the purpose of this post, this gives a sense of what user considerations influence product decisions.



<br/><a name="stakeholders"></a>
### **4. Stakeholders**

FB is a multi-billion dollar company, which means it has lots of different stakeholders. It follows that the needs of those stakeholders will sometimes be important factors when product decisions are made. A good outline of that is made by [Adam Mosseri in 2010](https://www.youtube.com/watch?v=bKZiXAFeBeY) [12m53]:
> At Facebook, in product, there is a healthy skepticism of being overly data driven. It is very difficult for a set of metrics to fully represent what you value. There are a lot of factors that go into making any sort of product decision. Quantitative data is one [], qualitative data is another, **strategic interests** are another, **user interests** are another (what people complain about, what people ask for), **network interests** (which are significantly different), **competition** clearly factors into our decision making, **regulatory bodies** at this point (at our scale we have to deal with privacy advocacy groups, the EU...), and **business interests** (explicitly we value revenue generation right now less than growth and engagement. Growth being defined by how many users come onto the site, engagement being defined by how often users use the site). So, these are all important factors that we use in making our decisions

<br/><a name="engagement"></a>
### **5. Engagement**

![](https://i.imgur.com/wU9atQP.png){:height="50%" width="50%"}

It is my understanding that engagement is a core focus of product teams at FB. It’s key to the platform for several reasons:
- **Growth** – the more people on the platform, the more useful the platform is to all users
- **User Experience** – the more engaged users are, the more they read and write, and the more responsive they are. This makes it easier to connect each user to a meaningful experience - whether that is surfacing a new post from an interest group, or posting a photo that quickly gets liked by your friends.
- **Content** – time and attention spent on the platform attracts content
- **Revenue** – time and attention spent on the platform drives ad revenue

<br/><a name="abuse/misuse"></a>
### **7. Perverse outcomes**

A challenge that FB faces is the abuse of their products. I suspect FB products are built with both the most optimistic use cases in mind, and with the dangers of their misuse in mind. Some examples of where product thinking addresses these issues in public:
- **Offensive content** - “The idea is to give everyone in the community options for how they would like to set the content policy for themselves. Where is your line on nudity? On violence? On graphic content? On profanity? What you decide will be your personal settings. We will periodically ask you these questions to increase participation and so you don’t need to dig around to find them. For those who don’t make a decision, the default will be whatever the majority of people in your region selected, like a referendum. Of course you will always be free to update your personal settings anytime.”
- **Polarization** - “Research shows that some of the most obvious ideas, like showing people an article from the opposite perspective, actually deepen polarization by framing other perspectives as foreign. A more effective approach is to show a range of perspectives, let people see where their views are on a spectrum and come to a conclusion on what they think is right… the best solutions for improving discourse may come from getting to know each other as whole people instead of just opinions – something FB may be uniquely suited to do.”
- **Clickbait** - “In general, if you become less likely to share a story after reading it, that’s a good sign the headline was sensational. If you’re more likely to share a story after reading it, that’s often a sign of good in-depth content. We recently started reducing sensationalism in News Feed by taking this into account for pieces of content, and going forward signals like this will identify sensational publishers as well”


<br/>
<a name="summary"></a>
### **6. Summary**
- FB is a service for connecting
- Social is core to the product experience (FB is a network)
- Engagement is key
- FB prioritises users
- First order user needs: to
  1. connect
  2. communicate
  3. discover
  4. share
  5. entertain
- Non-user interests matter (but less)
- Perverse outcomes matter

<br/>
**Part 2 [here](test)**
