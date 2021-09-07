---
layout: post
title: must win ... can analytics save my ff team?
---

I'll begin this post with a vulnerable statement about a topic which has almost 0 consequence on life and whose weight is only felt by me: I cannot figure out how to win at fantasy football.  

I've been playing fantasy football for at least 20 years now. In all that time, I've won the championship only once, and had a handful of 2nd and 3rd place wins. I'm more of a basketball person, and I think what's staved off my utter embarassment is a profound naivety about how to win (i.e. "if I never look up how to win, then I never put any effort into it and I'm not culpable") and some sort of mental gymnastics wherein I reason that I'm more of a basketball person. 

After 2 decades though, I'd expect my intuition would have increased, and I'd subconsciously be making great moves as a manager. 

This is not the case. 

So this year I'm going to use some skills that I didn't have 20 years ago and ~over-engineer~ engineer my way out of this mess. I've started by creating a repo and doing some initial exploratory data analysis (EDA). This EDA is found [here](https://github.com/kevcisme/fantasy-football/blob/main/draft-day-eda.ipynb){:target="_blank"} in full, but I'm going to post a summarization and insights learned.

In this post, I'm going to discuss some metrics that I'm going to assume are meaningful. 
But before I get there, I need to smash some naivety and read something. I ran a simple search on Arxiv [arxiv.org](https://arxiv.org){:target="_blank"}. It seems as though most research supports the idea of predicting match outcomes, like [Football Futures](http://cs229.stanford.edu/proj2011/SierraFoscoFierro-FootballFutures.pdf){:target="_blank"} whose authors use Support Vector Machines (SVMs) to predict outcome of the real life football game. In [Fantasy Football Prediction](https://arxiv.org/pdf/1505.06918.pdf){:target="_blank"} the author extends this idea to predict the outcome of a fantasy football game. This is also done using a SVM. The author mentions that 

> A large part of my work is to create a proper dataset from the real game data.  

which makes sense. This might be useful for later predictions. Maybe I'll run this SVM and then predict outcomes and shock my league. However, these feel like party tricks compared to winning a championship. The draft is likely the best point of entry for EDA and maybe some machine learning. 

Regarding EDA on the draft itself, I am having trouble finding any source datasets. I will work on building one out. There is some work done on predicting performance at a player level that was done on European Football (p.s. I'm being lazy and calling American Football -> football because laziness conforms to American stereotypes better). This work on predicting player level scores involves time series modeling - [Time Series Modeling for Dream Team in Fantasy Premier League](https://arxiv.org/pdf/1909.12938.pdf){:target="_blank"}. It would appear that modeling is fairly green-field, because I can't seem to find papers. So let's focus on what's out there for machine learning.

Regarding machine learning on my draft, I suspect that a Reinforcement Learning Bot could be deployed here. To this end, I found a paper [MimicBot](https://arxiv.org/pdf/2108.09478.pdf){:target="_blank"} which seems to mostly tackle this problem (p.s. terrible puns are going to be a thing. I don't apologize). 

There's a company called [Gridiron AI](https://gridironai.com/football/){:target="_blank"} and they seem to offer a product. It's $5 so I'll subscribe and check out their dataset (they offer "downloadable data" if you become a member). 

Lastly, there's a couple YouTube videos. Professor Kevin Zatloukal discussed ML and its application to fantasy football and investing in [Excess Returns](https://www.youtube.com/watch?v=LqchDk2t0h8){:target="_blank"}. He mentions clustering around 0:23:35 and I wonder if there's some clustering that could be helpful? I'll explore these after my initial EDA. He really gets into his approach around 28:48 after he explains what clustering is. 

Let's get back on those metrics. 

## ADP

Average Draft Position (ADP).

ADP to me is like a wisdom of the crowd measure. In the era of big data, it's a breadcrumb that ESPN and Yahoo toss to fans. I have no idea how it's calculated but I'll operate on an assumption that it's defined like "across all drafts that have happened on our platform, this is average number that this person was picked on." I have an assumption that this might be useful. I found through some exploration that there are a number of times where experts would draft at a much lower position:
<img src="https://raw.githubusercontent.com/kevcisme/fantasy-football/main/assets/high-delta-adp.png">

and then a few times where the experts would have drafted much later than the ADP of the crowd:
<img src = "https://raw.githubusercontent.com/kevcisme/fantasy-football/main/assets/low-delta-adp.png">

I'm mostly posting these so that I can track. I don't have an opinion yet on what it means to have a delta in one direction or another.

## Past Performance

I have an assumption that it's not solely by chance that we see certain people winning our league often and others losing. I performed some analysis and I'll continue to update this as I get more findings.

### Summary:

So in summary, this is an ongoing project. I _think_ I can beat my friends with a little bit of machine learning knowledge to bolster me. Really, when I think about it, that's what I'm optimizing for: 

> Destroying my friends and crushing their spirits using math.

Till next time!  
