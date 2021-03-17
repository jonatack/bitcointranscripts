---
title: Redesigning Bitcoin Fee Market
TranscriptBy: Bryan Bishop
---

Redesigning bitcoin's fee market

Or Sattath (The Hebrew University)

<https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2017-September/015093.html>

<https://www.reddit.com/r/Bitcoin/comments/72qi2r/redesigning_bitcoins_fee_market_a_new_paper_by/>

paper: <https://arxiv.org/abs/1709.08881>

He will be exploring alternative auction markets.

Hello. This is joint work with Aviv Zohar and I have just moved. And Ron Lavi. And I am going to be talking about tehcniques from... auction theory.. to rethink how fees in bitcoin are done.

Just a fast recap of how the current mechanism works. Each block has a size. Users are asked to specify the fee they will even pay. And the miner orders the transactions in sat/byte.

Let's do some thought experiments on what happens in the case where the block reward is kind of minimum at some point in the future as it will happen. There are some advancement that makes all the hardware 100x better than bandwidth, disk space, CPU, everything is 100x better let's say. What about increasing the block size by 100x? That should work out. And it did from many perspectives. From an economics perspective, it's problematic in a particular sense. If you increase the block size, then there may not be enough transactions to fit in the block and this might cause a drop in revenue for miners. This is a race to the bottom. Since blocks are not full, miners have an incentive to not take many small fees, so users might adapt their fees and revenue for the miners will deminish and the security of the entire network also decreases. It would be very cheap to-- because the system does not buy enough security. That's kind of bad. And this is the thing that we want to ask about and question.

What are the design rules? As we have seen, increasing the hardware parameters and the block size might decrease the miner revenue. So what we want is to have a system without this effect. We want to maximie therevenue for the miners, and in particular if the increase in bandwidth and hardware parameters for the network we could increase the miner's revenue. And another issue that is somehow.. the block size issue is the main property that determines the current fee market... determines is related to both the security aspects to avoid DoS attacks and things like that, and also economic aspects. One of the angles is to decouple these two issues. And perhaps the last design goal is to related to the previous talk which is to simplify the user experience. It's sort of complex right now. How should the user decide those fees and how ...

Bitcoin mining can be analyze

((ask maaku for the rest of this document))

... and buyers can't collude, and we have strong identities in auction theory and we need to make sure that this is somehow that we at least notice that we have to somehow take it into account.

So we have two main results or two main mechanisms. One of them is called the ... which is described later, it's RSOP mechanism. It's a nice result. It's very different from the current mechanism and you can see how rich the class of auctions you can use. Unfortunately it's not very practical. I'll explain why. The other mechanism you can use is the monopolistic price mechanism which is I think more practical. Let's start with the first even though it's not that practical. And to finish this, which is like, which are called monopolsitical price and monopolistic revenue... suppose you want to sell, and you, suppose that for the you want to do price discrimination. And suppose you have people who are interested in mining and they are willing to pay up to fee n to fee m. The max over v, times i, times i. What's going on here? If you ask for the price vi, there are more people willing to pay that. So if you ask them, then your fee revenue would be... maximizing over all possible values and that's why it's called a monopolsitic price. So the again, the value itself is one of these monopolistic revenue and the price you ask, and vi is the monopolistic price. And the example is that suppose that the .. values are 3, 2, and 1. If the price was 3 then you would have one buyer, so the revenue would be 3. If you ask, for, then the price would be 2, and then the revenue is four, and if the price was one you would have 3 buyers, so your revenue would be 3. So the monopolistic price here is two, right, and the revenue is 4.

Of course, if you knew the values of the users, it's kind of using to determine the price. Miners are-- sorry, users are usually strategic and rational. They might not give you their true value. In particular, in bitcoin actually, users can even be, they can havem ore subtle strategy where they put multiple bits and they discuss in the paper and we won't discuss it here. So hnnow we are ready to present and there are some mechanism and there's random sampling optimal p something based on Goldberg et al 2006. Suppose that users have values 5, 4, 3, 2, and 1. Suppose you put them into two groups randomly and now you do something kind of weird. You calculate the monoopolistic price for a group, and you think about what this is, and there are two users, and the monopolistic price is four, and now you offer it for a second grouping, and you take the monopolistic price here and you offer it to group A, and now you have in group A, one user that is willing to pay more than 4, so that user... and he... pays 4.. and vice versa. So the monopolstic price in group 2 is, so this guy wins, and basically.

So why did we do this? The first thing we notice is that this is a truthful auction that forces users to reveal their true value. They lose nothing from telling them their true value. Let's try to see why. At some point, your offer, yout ake it over leave it offer. Now, the offer that you are given in some sense is fully determined by the other group. It doesn't determine-- it's not determined at all, it's what you have set. So you have no reason to manipulate or say something which wasn't the truth, you wouldn't gain anything from that. And therefore you have nothing to cheat or whatever. So you have no reason to be strategic.
Another interesting aspect of this mechanism is that it converges to this mechanism.. the revenue from this mechanism converges to the monopolistic revenue. So in some sense you are getting as high revenue as possible and you roughly get the maximum that you could. Okay.

So how would you adapt this to bitcoin? User specified a maximum fee, which is not like the current one where they actually pay what they put in the transaction, but rather that they may pay this. Miners would... so that's kind of tricky. Miners would include all of those mempool transactions... and the block hash is used to randomly partition the bids required by this mechanism using a PRNG and only the transactions that win according to the RSOP mechanism are considered valid. There are two problems. The first problem is that the blocks are huge if you include all transactions in the block then it becomes very impractical. Another concern is that miners can cheat in some sense. As we have said, the revenue from the miners converges to one, to the optimal one as you go from infinity, and there's a simple strategy so that they can ... cheat, and then the users can cheat, and the argument kind of collapses.

What about the monopolistic pricing mechanism proposal? It uses again a specified maximum fee by each bid. If a block contains b1 up to b_n, then all users pay b_n, right? So the minimum transaction for the block fully determines the fee which everyone pays. So what would the miners do if this is the case? First of all just like the current bitcoin works, there's a cap on the block size. So there is still a cap on block size, but it's just an upper bound, but they could use smaller blocks of course. So what could they do? They would calculate the monopolsitic prices, if the block space can support m transactions, and if it's, you know, turns out to be less than m, the block wouldn't be full. And uh, our result applying to something which we call new .. users.. which are only interested in being included in the next block. And uh, and the concern here is that even in patient users, making little, by recoding or not being truthful. SO what 'were interested in is understanding how little it is. And the way they are being stratyegic is that they are reducing their fees and their goal is to decrease their monopolistic price. So let's see an example to make it clear what i'm talking about ((excised)).

We show that if the distribution from each of the transactions, if the fees are sampled, there is finite support, then the discount ratio goes to zero as the number of ... grows. The main concern is what how fast does it tend to zero and-- we had some assumptions like finite support, what happens if there are is no finite support? We would want to evaluate this empirically. What you see here are seven distributions for the synthetic ones and 3 which are .. blockchain or whatever you like. On the x axis is number of users, and on the y axis is the maximal discount ratio among all the players that took part in that. And each point here is the average over 100 experiments. As you cna see, all of these, for example, theis is a discrete distribution and as you can see this kind of increases linearly which is nice. This is kind of a worst case distribution we call it a .... distribution, we won't explain exactly what it is. But you have to add some conditions for here's an exact count, to the conjecture that in all cases, it should drop to zero. That's force, right? As you can see, it does not decrease at all. So you have to have some assumptions on the distribution. We have some other distributions like, hash normal distribution which isn't bounded, but it decreases kind of nice. And the more, the real blockchain data what we did is we took, some transactions from I don't remember, a few months of data, and took the sumo f all the inputs from all the transactions and we picked the trandom ransactions at random and how did we say the person is willing to make the transaction pay? We didn't really have a good guest, so one thing we could say that the user would probably be willing to wait a constant fraction out of it, so that's one of our distributions, and then another one is the square root of it, and rich people tend to pay less for this kind of thing. And the other more, you could kind of, make like, log of this sum, and all of this are, decreasing linearly, but there are some differences. If you are looking at 1000 users, roughly one to 10%, that's kind of the manipulation they can do, depending on the distribution. And everything her is on a log scale, I hope that's clear.
That's it. I think the main or the most interesting open problem is... you know, where does, we want to buy security. We want to have fees so that it's harder to attack to double spend essentially. Let's maximize it, let's buy as much security as we can. But it could be that perhaps we are buying too much security. NMaybe the design would be different and we should estimate how much security we should buy and then somehow adapt our mechanism to reach that goal. But I don't have any good answers for how to estimate it, and certainly not in a distributed manner for what the goal should be. So that's the first point.

Another kind of, not sure if it's criticism, but the first reaction that I get when I try to explain this paper, some people say it looks like an intervention and the free market is the current way to do it, and I'm kind of intervening at least according to critiques. This is kind of an illusion. Of course I agree that the current mechanism works and we have confidence in it, much more than the one that I am proposing, but still there is nothing more natural about that like the current protocol than the auction mechanisms I am proposing. All of them are kind of mechanisms that are trying to do something and there is nothing more natural or free about one or the other. It's not the free market that we currently use... I am interested in finding ways or ... I don't know, real data, on the willingness to pay. tohe distribution to use... is it power law? Is it .. a normal distribution? What is the real willingness to pay for transactions as a function of transaction size? And perhaps.. and actually, I had some discussion with some people here, maybe there are ways to make the RSOP mechanism more applicable for bitcoin.

