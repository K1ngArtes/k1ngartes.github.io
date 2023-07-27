---
title: "I've joined Clustr"
date: 2023-07-27
draft: false
---
My idea with Tiny Projects didn’t go according to plan. Sometime in March, Tim, who I played football with back in Manchester, approached me and proposed to join his startup. We have never been close and haven’t spoken since my uni years, so I was both surprised and flattered to be contacted.

# Oh no, is it... crypto?
The project is called Clustr. It is a crypto/web3 project. Not something I am fond of, I will be honest. However, the idea is somewhat useful. In a nutshell, Clustr would allow users to make better investment decisions by analysing the current state of the market, ranking existing coins based on the methodology (available publicly for anyone to judge for themselves), creating demo portfolios or importing existing ones, and analyse them based on a pre-defined set of metrics. It will grow into an investment platform, providing users with various investment insights to help them make better investment decisions. Newbies to the market could learn how to build crypto portfolios step-by-step while being exposed to the driving forces behind the decision-making made by professionals in an easy-to-digest form. More sophisticated users would benefit from the platform’s insights (such as growth projections) and a large selection of rated coins. Feel free to check the [landing page](https://www.clustr.io/).

It doesn’t sound that bad. But let’s be frank, the bar is extremely low; not being a scam in the crypto world is considered a rarity. In addition, I do not consider myself a proper crypto-investor; I did invest during the frenzy and eventually gave up when the market crashed, so my knowledge on the matter is minimal. However, I imagine myself continuing to invest if I had an educational resource to teach me the “proper” way. Clustr could be just what people like me need.

# April fools
On the 1st of April, I joined the team as a lead backend engineer. The decision didn’t come lightly, and I went back and forth for some time. Was I willing to dedicate my most valuable resource - time, to someone else's dream startup? Crypto is not something I would do myself. Add to it an alien tech stack (Python, Django, GraphQL) and tight deadlines. What about the team of people I have never seen before? What about the previous startups failing miserably with absolutely 0£ landing into my account (more like costing me tens of thousands in time alone)? I guess the time will show, but I imagine myself going insane waiting for something perfect to arrive at my doorstep. I have tried launching a website creation agency in The White Robot, attempted to hit it big with grocery deliveries at [Devo](https://devo.co.uk/), and now it is time to make my shot in cryptocurrency with Clustr.

![3 months later](/27-07-2023-i-have-joined-clustr/3_months_later.jpg)

Clustr launched on the 7th of July on [ProductHunt](https://www.producthunt.com/products/clustr#clustr). We have built a stable lander, web application, and backend system in three months without too many hacks. The core functionality of version 1.0:
* Allow users to inspect the selection of more than 700 coins.
* Inspect coin prices, capitalisation, and Clustr rank.
* Registration process via the magic link.
* Create up to three demo portfolios in a guided step-by-step process.
* Inspect individual portfolio views, including monthly performance, ATH, ATL, AAR, internally calculated “risk” value and portfolio rank.

{{< figure src="/27-07-2023-i-have-joined-clustr/main_page.png" title="An elephant at sunset" caption="View of the main page">}}
{{< figure src="/27-07-2023-i-have-joined-clustr/portfolio_view.png" title="An elephant at sunset" caption="View of the single portfolio page">}}

From the backend perspective, the combination of unfamiliar technologies made it challenging. I only wrote basic scripts with Python before and have never tried Django. I’ve only seen others use GraphQL and have never written a GraphQL API myself. I was familiar with Docker fundamentally; I never ran DBs in Docker or did nothing close to 5+ apps running on the same VM. All of these were solvable tasks that people had done many times before, and there were more than enough tutorials on the topic so that I could find my way around. The main issue was - I was short on time. Three months is not enough to launch a startup with robust foundations from scratch when you are working a full-time job.

# A few thoughts on the development process without any particular order
* ChatGPT was extremely useful, especially when you have no clue what you are doing. At first, I used it to write basic scripts and later adapted it to explain concepts and ideas.
* Man, I love statically typed languages. I love knowing the shape of the data I am operating on. Sure, the initial development time in Python is low, you can write whatever the hell you want, but I am concerned about its long-term prospect. As the project grows, understanding what things do will become harder and harder. Returning to the code I wrote three months ago, I go, “What the hell am I even working on within here”. I have adapted type hinting in the project, but it is still such as chore and a forced matter that I am TRULLY not having fun.
* You have to find your way around with data. It can be challenging to get the data you need about Crypto. And even when you get it, it is very often garbage. And you don’t have money to pay to get a better one. So you create a Frankenstein code base built with fallback-on-top-of-a-fallback trying to cover as many loopholes in your data as possible, hoping that your users will *“avoid using coin number 643, cause it misses both market closing price, daily price, S&P data, and rank on the second week of January 2015”*. 

As a result of our work, we got “The Product of the Day” and “The Product of the Week” on Product Hunt. We were in the PH weekly newsletter and appeared in its “stories” on the mobile app for the whole week. Contrary to our expectations, we didn’t get much traffic from these events. We have put extra resources into replication, performed load testing (I have used [Artillery](https://www.artillery.io/) for that), and removed some of the bottlenecks (a quick memcache solves many issues) to end up with almost no server load. I wouldn’t call it premature optimisation, as I hope we will get more and more users as time passes.

# What's next?
For now, we are concentrating on getting “The Product of the Month”, which will (from my understanding) get us into a “big boys” league (as far as PH is concerned). We have to get our hands dirty with some internal PH politics, upvotes and comments grinding to get it. Many startups are launching along with us, some of which are already backed by investors, like Y Combinator. The results will be available on the 1st of August, which will mark four months of my time in Clustr. Despite the grind, crunch, and stress, I remain optimistic we will make it through.
