---
tags:
  - rowboat
  - fireflies
  - transcript
---

# Sui ️ Building on Sui DeFi and DeepBook

**Meeting ID:** 01KG3ADMYRD5Q9H98G3VMWC5MS
**Date:** 2/3/2026, 8:30:00 PM
**Organizer:** shikhar@iiitmanipur.ac.in
**Participants:** vasu_k@ee.iitr.ac.in, shikhar@iiitmanipur.ac.in, charandeepkapoor3@gmail.com, bashybaranaba@gmail.com, nishanthb.it2024@citchennai.net, yashj8858@gmail.com, felipe.sarmiento.as@gmail.com, stefanolombardo@posteo.de, visheshdwivedi225544@gmail.com, lokeshwaran100@gmail.com, kulrajs.sabharwal.chy21@itbhu.ac.in, carlos@velascode.xyz, singgihbrilian.tara06@gmail.com, gmartinezgil@gmail.com, rahat@rahatcodes.com, jsteerv@gmail.com, detroitmetalcrypto@gmail.com, kurodenjiro1@gmail.com, weberfabian1@gmx.de, gerardo.gerry.pedrizco@gmail.com, penrose@ultra.markets, ayushsrivas55@gmail.com, laciferin@gmail.com, j.vivekvamsi@gmail.com, arosejeremic5@gmail.com
**Meeting Link:** https://ethglobal.zoom.us/j/85088068959
**Duration:** 0m 31.65999984741211s

---

## Overview

DeepBook leverages SUI’s object-centric blockchain to enable scalable, parallel trading without transaction contention. The protocol features a fully on-chain central limit order book that utilizes shared objects, allowing multiple trading pools to operate independently and in parallel. This design results in lower latency and higher throughput for order matching. Users create a balance manager object to manage funds and trade, which supports various coin types and enhances control over their trading experience. Programmable transaction blocks (PTBs) allow users to bundle multiple operations into a single atomic transaction, improving efficiency and reducing costs. Margin trading is integrated seamlessly, enabling leveraged positions without separate liquidity fragmentation. The developer ecosystem is fostered through straightforward tools and open communication channels, encouraging innovation and collaboration.

## Keywords

DeepBook, Sui, Central Limit Order Book, Programmable Transaction Block, Flash Loans, Balance Manager

## Action Items


**Aslan Tashtanov**
Provide workshop participants with his Telegram contact for asynchronous questions and support (26:54)
Support and brainstorm hackathon projects around DeepBook including frontend apps, margin trading, market making, and skill integrations (27:29)

**Andrew Dunscomb**
Ensure workshop recording is uploaded to East Global YouTube channel for later access (27:19)
Facilitate communication by pointing participants to Sui team Discord channels for hackathon support (30:45)

**Unassigned**
Participants encouraged to experiment with DeepBook SDK on testnet/mainnet for swaps, margin trading, and flash loans following example code shared (00:00)


## Transcript


### Andrew Dunscomb
 Okay, we're going to start this workshop.
 We have a 30 minute workshop today.
 You're here with Aslan from SUI and the name of this workshop is Building on Sui, Defi and deepbook.
 You'll have an opportunity to put questions in the chat and we can also cover questions at the end.
 So with that I will hand it off to Aslan and have a great workshop.

### Aslan Tashtanov
 Thank you, Andrew, for the intro.
 Hi everybody.
 I'm Aslan.
 I lead DEFI at Miston Labs.
 I lead the DeepBook project as well.
 And I'm going to do a workshop.
 On DeepBook and how you can get started with the DeepBook SDK and a little bit about how SUI works and.
 The differences between SU and evm, the.
 Architectural differences, and kind of how you guys can start wrapping your mind around building on sui.
 I will say one thing, I believe.
 S Suite has probably the best devex ever.
 It's very simple, it's very nice, it's convenient.
 But the thing that I'll start with is briefly the main difference between evm, like the account based model of blockchains and the object centric model of sui.
 On sui, there are no blocks where.
 You compete for transaction inclusion.
 Instead, everything is an object.
 The state is just a bunch of different objects living in a bunch of different places.
 And your transaction just takes some input.
 And it mutates objects in the state.
 So to get started with DeepBook, I.
 Have three files that I'm going to run through.
 The first one is just, you know.
 Getting started with the DeepBook SDK and.
 We'Re going to read the order book for swe USDC.
 So before I get started, DeepBook is a fully on chain central limit order book.
 It has time and price matching for orders within the order book.
 Now what's unique here is, remember how I said each object is everything is an Object.
 Well, for DeepBook, for example, the SUI USDC pool is its own object.
 So if you want to trade in the SUI USDC pool, you only mutate one shared object.
 We call it a shared object because.
 Everybody has access to that object.
 And owned objects are objects that you.
 Have access to in your wallet and nobody else has access to it.
 So the SUI USDC shared object is what you use to trade.
 And the best part is if you.
 Are trading in, for example, the DEEP.
 USDC pool, your transactions do not compete.
 Whatsoever with the transactions that are trading.
 On the SWE USDC pool.
 And this is how we unlock parallelism and scalability.
 So if you think about it, you know, traditionally, for example On Ethereum, everybody competes for one block space regardless of what you're doing.
 On Chain for suite, if you are mutating objects that are, that don't touch.
 Each other in any way, then your.
 Transactions can be sequenced in parallel without any restrictions.
 Okay, so that is a brief on how sweet suite and Deep Book work here.
 I'm going to run through three examples.
 And we're going to probably spend the.
 Most time on the swap one because I will go into the details of how DeepBook works, specifically the balance manager.
 There's some how that gets set up.
 But first let's start with just an example where we look at the state of SWE usdc.
 Here we will get the by the.
 Way, Workshop client is.
 Let me go into this one real quick.
 This is just a wrapper of the Deep Book SDK.
 I just added a few extra things and then I added some functions to.
 Call the SDK underneath and then send.
 Some extra log statements.
 But this client is just a Wrapper of the DeepBook SDK.
 And let me double check the script here.
 Okay, one read.
 So let's see what's going to happen there.
 So, okay, so what we did here, by the way, I saw some people asking things in the chat.
 I think I'm supposed to be monitoring it.
 If I don't answer any questions like, you know, please.
 I'll also have my telegram at the end so you guys can like DM me async if you want to.
 Okay, this is all just AI conversations.
 Never mind.
 Okay, so what did we do here?
 We got the price of Sui.
 According to the SDK, it's on the.
 On the central limit order book on.
 On chain right now it is 1.$13.
 We also got the order book itself.
 So this is what the order book currently looks like.
 Looks like we got, you know, the best ask is at 1.1313.
 Best bid is at 1.1309.
 So the difference is like 0.4 cents.
 What is.
 Which is about like, like three basis points of spread here.
 Okay, Vault balance.
 So the vault is the SW USDC object itself.
 This is all the money that is.
 Held inside of this shared object.
 So all the participants that have placed orders.
 So whatever is making up this order book is, is.
 Is what's in this vault essentially.
 And trade params are.
 This is the taker fee, this is the maker fee, and this is the stake required.
 Stake required is, is.
 Is a DeepBook native feature where if you stake deep you get reduced taker fees as well as you know, maker rebates.
 But this is a, a quick example.
 Of how you query the chain.
 Let me go into the workshop client.
 To see to, to actually show you guys what ends up happening.
 So mid price, it simply goes into.
 The inner DeepBook client and gets the mid price.
 Now print book, what we have is get level 2 ticks from mid and what we put in here is 10.
 Ticks and it essentially got the mid.
 Price and then text 10 ticks above and below, you can modify this to, you know, increase the depth that you want to see and we simply just pretty printed it out.
 Vault balances similarly.
 We're just calling the inner client and yeah, that is all for now.
 And, and the trade params, it's probably.
 Actually we might have just done a direct call for trade print.
 Never mind, it's right here.
 Yeah, and that's, that's also a direct call.
 Okay.
 So that's a simple, you know, read the chain, read what's going on in on Deep Book on chain right now.
 Now let's go to swap.
 Before I go to swap, I'm gonna.
 Just quickly see if anybody ask the question.
 Okay.
 This same order book is also used by the DeepBook margin 2, right?
 Yes, exactly.
 So DeepBook Core is completely isolated from everything else.
 Okay.
 It is completely independent.
 Same with margin.
 Margin is an independent package and when.
 You borrow from the margin pools to place orders on DeepBook, you are placing orders the same way everybody else is, including users that are using DeepBook Core.
 Directly for spot trading or aggregators that route through deepbook.
 Everybody's kind of orders are all in one place.
 Margin does not have its own order book or anything like that.
 That's the main thing about how DeepBook works.
 It is very composable and it's designed.
 To be very modular.
 Let me see if there are any other questions.
 Okay, I don't.
 I think that's all the other ones.
 Are seem like they're AI so let's go to swap.
 Okay.
 This one's going to be the bigger one.
 First I'm going to go through.
 So here's what's going to happen.
 I'm going to go through the code and then we're going to run it.
 And then we're going to look on chain.
 I'm going to switch the screen share to Chrome.
 So we'll see if exactly what transactions.
 Were produced and then we'll do a.
 Little bit of a SUI vision thing.
 To understand how the Explorer works.
 So I have my private key in.
 The end file and we're setting everything.
 To mainnet and we're setting up the private key.
 And the first thing that we're going.
 To do is check the balances of.
 My address, like what money do I have in my wallet generally?
 Right, Right.
 Now here's the second step.
 To actually interact with DeepBook, what you need to do is create an object called a balance manager.
 Okay?
 And I think of this as like.
 An account that you create on, you know, like a different exchange, like on Hyper Liquid.
 You create an account and then you deposit money into that account and then you go trade.
 Right?
 This is not the same as Uniswap.
 Where you don't create any account, it just, you know, you just swap directly.
 But in this one, you do create.
 An account, but the key here is the account is super composable.
 So actually if you want the direct.
 Swap experience, you can generate a balance manager on the fly, deposit money, swap, and then destroy the balance manager on your way out.
 So the full Uniswap experience is also maintained here.
 But for this example, we're gonna create a balance manager and then we do a little bit of, you know, parsing.
 Of the transaction outputs here.
 Because what we're looking for is create results.
 The object changes that find.
 Okay, so we're looking for in the.
 Results in the transaction that's returned.
 We're looking for an object that was mutated and it has a tag of created.
 So a new object is being created on the blockchain.
 And if it's the type of balance manager, go ahead and extract the ID.
 Of that object that was created.
 Now when this balance manager gets created.
 It becomes a shared object, so everybody.
 Has access to it.
 But for ensuite, what you can do.
 Is just incorporate.
 Gating for specific actions.
 Within the balance manager.
 So if you submit funds into this.
 Balance manager, anybody can query and see how much money you have in there, but nobody can actually use your balance manager because there's a capability that restricts only the creator of this balance manager.
 Balance manager to actually place orders with it.
 So we create the balance manager and what we have to do then is recreate the client with the balance manager as one of the inputs.
 And then we're going to go into depositing money into the balance manager.
 And once we have money in the.
 Balance manager, we can actually place a market order, which is what we're going.
 To do right here.
 We're going to buy one sweep with USDC and that's going to be all.
 Okay, so we're going to run through.
 I know there Was a, a lot covered there.
 But just again, real quick, we're going.
 To check how much money we have in our wallet.
 We're going to create a balance manager.
 We're going to deposit 5 USDC and 10 deep into the balance manager and.
 Then we're going to execute a market order.
 Now I'm going to show you actually.
 Okay, so let's, let's do this sequentially here.
 First I'm going to run swap and let's see what happens.
 I checked my wallet, created a balance manager.
 Okay.
 I think I might have deposited too much money into the previous balance managers.
 Let's go ahead and drop.
 Let me actually check how much money.
 Is in the wallet.
 We might have been.
 Going too quickly here.
 Okay, what we're going to do is set this one to five and.
 Okay, let's try it again.
 In practice, you would just create one balance manager.
 You don't have to recreate new ones every single time.
 But I, I'm just trying to run.
 This example end to here.
 Okay, there we go.
 We deposited five USDC and ten deep.
 And our balance after is now five years DC and ten deep.
 And then we swapped and our balance after becomes one USDC and one sweet.
 3.87 USDC and 9.996 deep.
 Okay, we're going to go into this.
 Transaction digest in a bit to look at what actually happened on chain.
 But before we do that, let's just do a quick recap.
 These are raw numbers.
 I should have put them in decimal form.
 But what we ended up doing here is, okay, we created the balance manager and then we recreated the client with this balance Manager.
 We deposited 5 USDC and 10 deep.
 Now the 10 deep deposit here is simply because the DeepBook protocol takes trading fees in two forms, either the input token or deep.
 So you can actually use deep to pay for your trading fees.
 And there is a, an incentive to do that so you pay less trading fees when you use deep and slightly more when you use the input token.
 So we didn't necessarily have to deposit.
 The 10 deep here and we could have just used the 5 USDC directly.
 And it would just charge us a.
 Little bit more USDC to do the swap.
 And finally, the transaction digest has been.
 Produced and what I'm going to do now is I'm going to share my Chrome screen.
 Okay, question.
 Can you explain the difference between deep and sui?
 Are both of them coin type T?
 Yes, all coins are of type T. The type T is like a generic.
 So if you have a function in your move Smart contract that takes in.
 A type T. Actually I can show you an example.
 Then that smart contract can take any coin type.
 Okay.
 But you'll have to do some, some.
 Smart things with it.
 Let me show you an example of what I mean.
 Let's go to deep book sources.
 Balance manager.
 Okay, so this is a smart contract.
 For the balance manager itself.
 Right.
 And what, what we'll notice is.
 Let me go to the deposit function.
 Okay, this is new.
 This is what we actually call to.
 Create a balance manager.
 And the where's the deposit?
 Okay.
 And this is balance.
 This is what we actually use to query the balance.
 See, like this, we're using type T here to query balances.
 And if we just pass in the type of the coin that we want to query, it'll figure out on its.
 Own what number to return.
 Let me just show you guys the supply.
 Okay.
 Deposit.
 Okay, there we go.
 Deposit.
 We're depositing any coin.
 So see there is no distinction here.
 Between are we depositing?
 Depositing.
 Sweet.
 Deep usdc.
 We take any coin with any type and all that we do is just.
 Dereference the type and just create a new key in the bag object within.
 The balance manager and just have that point to the balance itself.
 So the balance manager is totally generic.
 It has no restriction on what kind.
 Of coins you can deposit or what you can do.
 So that is how this works.
 If you have coded and rust, then.
 This will feel very familiar.
 Great, let's go ahead and jump to the.
 Chrome browser.
 Okay, hopefully this is here, let me zoom in a little bit.
 Okay, So this was that swap from earlier where we swapped USDC to suite.
 And for what I do when I'm on suite vision is the first thing that I do.
 I just go and look at the.
 Events and there's a few events that are emitted here.
 The important ones are this order info object and this has all the details about, you know, what happened during the full entire process of this action.
 Then there's this order filled event that has like some details on the fill itself.
 This is what we, this is probably.
 The most important event.
 This is what we use to actually.
 Populate a lot of the dashboards and charts.
 And this is what we use for data tracking.
 And there, there are actually two order fill events, interestingly right, because we ended.
 Up filling multiple orders that were available.
 So there, there were two makers that.
 We ended up trading, trading against.
 Cool.
 There's this EWMA thing, but like that is more for an unrelated feature that DeepBook has.
 And here the transaction inputs these Actually.
 This show what happened under the hood.
 When we use this SDK, it combines.
 Two transactions into one.
 When we, for example, when we place this order.
 Yes, you can use SuiteVision on Testnet.
 And if you actually set the.
 Let me see here, let me show you.
 If you set the trader, if you set the environment to testnet, it'll interact.
 With the testnet contract.
 So you'll be able to see what's happening on testnet instead of mainnet.
 I just did mainnet because it's more reliable and less hiccups this situation.
 But let me point out something interesting here.
 Under the hood, the SDK actually combines.
 Two transactions into one.
 This is what we call a ptb.
 What did PTB stand for anyways?
 PTB is basically one atomic transaction that you just concatenate a bunch of different transactions into one.
 In the EVM world this exists, but what you have to do is you actually have to develop your own custom smart contract that does the different calls.
 So let's say you want to, you know, swap on Uniswap, take the output.
 Or let me, let me give a better example.
 Actually I'm going to show this by going to example three here, hold on one second.
 Programmable transaction block.
 Thank you.
 I'm going to go into the Flash Loan example to show you guys how the PTVs work.
 So flash loans is a feature that DeepBook has and it is designed in.
 A very interesting way.
 So you guys remember how in the first example we had this vault balances.
 So you would see all of the money that's inside of A one pool.
 What Flash Loans does is if, let's say the SUI USDC pool has, let's say, you know, 10 million SUI, then what you can do is go in and flash borrow, let's say 1000sui.
 Do whatever you want with it within your transaction.
 But at the end you return the Flash loan before the transaction completes.
 So it has to be atomic.
 Now, what's really cool about how Flash loans work, I'm going to kind of go into details here for a second.
 Let's see here.
 Okay.
 Borrow, Flash loan base.
 Check out what happens.
 So you go into the vault, you specify the quantity that you want to borrow and we just give you that coin.
 Here's the coin that you wanted.
 This is like real money.
 Here's that money and you can do whatever you want with it.
 The other thing that we give you is this thing called a flashlown object.
 Now the thing with this object is you'll notice that this, I'm sorry, The flashlown borrowed object.
 This is actually just for the event.
 Forget about that one.
 This is what's important.
 Notice how these other structs have attributes.
 This one has store, this one has copy drop.
 There's also one that has key balance Manager has key.
 Those attributes tell the object what it is capable of and what it can do.
 When an object has no attributes, then.
 That object cannot be alive on its own.
 It has to be consumed.
 So what ends up happening is this.
 Flash loan object that we return from.
 The borrow flashlown base call, this becomes a hot potato.
 Okay?
 If the return flash loan base is not called with that hot potato as input, then the whole transaction fails because.
 This hot potato cannot exist on its own.
 It has to be destroyed by the end of the transaction.
 And you'll see that we're destroying it here.
 So what ends up happening is the only way you can call borrow flashloan base is if at the end of your transaction you also call return flashloan base and the Flash loan itself also has exactly what pool did you borrow.
 From, how much, and the type of the thing that you borrowed.
 And then there's a validation that the.
 Coin that you're returning matches this exactly.
 And that's the only way that you can then destroy the Flash loan object here.
 Okay, so I am just going to run through the third example.
 And actually we're not really going to see any interesting results.
 But what's more important is what's here.
 And let me just.
 I know, I know we're at time.
 Here, but here's the example of how.
 We are combining different transactions in a.
 PTB without having to write any custom smart contracts.
 We can do this directly through the suite client SDK.
 We take a transaction, we do TX.
 Add and we append this transaction to borrow.
 So we're borrowing some deep.
 In this case, we're going to borrow one deep from the deep SWE pool.
 And then we're concatenating that with another transaction where we return that and you'll.
 See that we're returning the same flashlown object here.
 Then we're doing some transfer objects and.
 Then that's it, we are done.
 And if we look at the TX.
 Digest, I'm going to switch over to.
 Chrome one last time here.
 We got the Flash zone event here.
 But more importantly, check this out.
 So we have, we have four transactions that we combined whether we concatenated into one atomic transaction.
 And what's very cool here, and I don't have an example of this right.
 Now, what you can do is with the CLI directly, with the client directly, you can create one transaction that places.
 10 orders on the ask side and.
 10 orders on the bid side automatically with just one snapshot.
 Like it's just one transaction and you.
 Don'T pay the increased gas fees.
 And this is the reason why DeepBook.
 A fully on chain central limit order.
 Book actually works on suite because of these capabilities parallelization with the shared objects PTB so you don't have to place and cancel orders one by one and just low gas fees and very fast finality and all that good stuff.
 But yeah, that's it on my side.
 I know we're at time, let's see here.

### Andrew Dunscomb
 Yeah, we have, we can, we can take a few minutes.

### Aslan Tashtanov
 Okay.

### Andrew Dunscomb
 If anyone has any final questions.

### Aslan Tashtanov
 Yes please.
 If anybody has any other questions, let me know.
 Also I'll drop my telegram here.
 So you can hit me up on telegram as well for any questions.
 But yeah, I'll give it a little bit.

### Andrew Dunscomb
 Yeah.
 And also remember everyone that this is recorded and will be on the YouTube, the East Global YouTube.
 Ah, there's a question from Superno.

### Aslan Tashtanov
 Of course.
 Yes.
 All questions are allowed.
 Anything Deep book or SWE or defi.
 You know, all questions are allowed.
 What kind of apps are we expecting for the hack?
 Okay, a super easy one is like.
 A front end for example.
 Like a mobile trading front end would be cool.
 Anything that integrates margin would be cool.
 Pool.
 Something that's, that's maybe a little bit.
 Harder is like a market making bot for example.
 If you, if you figure out how.
 To you know, reduce the barrier to.
 Entry to market making, that would be interesting.
 Something that would be a little bit.
 New potentially is if anybody figures out.
 How to make it so you know how to skillify the deepbook stuff and make it so I can access, you.
 Know, do trades on DeepBook directly through like my cloth terminal or something through.
 Like a skill that would be something interesting to explore.
 I don't even know if that's like a, if that's a real thing.
 But yeah, ideas like that.
 I don't know if that, that's like too vague but happy to like hash out and.
 Brainstorm if you guys want to do that more.
 So the, the whole leverage thing.
 Okay, so for margin we have isolated margin.
 So you have to borrow, for example.
 You borrow USDC from a USDC pool to place long orders and the SUI deep or wall markets and then you borrow SUI from the sweet pool to place short orders in the SUI USDC market for example.
 So when you say are all these done on the same pool underneath?
 I'm not sure if you're asking about the actual liquidity pool where there are.
 Trades happening, but yes, if you borrow usdc, you end up just placing an order in the regular order book that DeepBook has.
 You don't place it in a different order book.
 How to pass arbitrary data between suite and EVM chains this is a hard one and I'll have to pull in some other folks to answer that question.
 Like zcashbot is ensuite.
 There's not really anything like that yet.
 I know there's some work being done on that topic, but I think that would be a cool one.
 To have anything related to privacy, anything that you want to build related to like private transactions or swaps or anything.
 Like that would be awesome to see.
 That we can actually leverage some of.
 The other suite infrastructure like Nautilus and Seal to to do some of the stuff if we need to hide certain operations.
 Yeah.
 So the actual liquidity pool is just one pool.
 One pool powers everything.
 Spot trading and margin trading and everything.
 Yes.
 All right.

### Andrew Dunscomb
 With that we are pretty much at time.
 That was an awesome workshop.
 Aslan.
 Everyone remember you can reach Aslan.
 He posted his telegram in this chat.
 Aslan Tosh Telegram.
 You can also reach the sweet team in the Discord for to hack money.
 They have a channel and with that I want to thank Aslan for a great workshop and see everyone in Discord.

### Aslan Tashtanov
 Thank you all.

### Title
 Sui ️ Building on Sui DeFi and DeepBook

### Host Email
 safia@ethglobal.com

### Organizer Email
 shikhar@iiitmanipur.ac.in

### Calendar Id
 2s58vap0asiaqp3a7ulcc9i250

### Fireflies Users
 felipe.sarmiento.as@gmail.com, ayushsrivas55@gmail.com, singgihbrilian.tara06@gmail.com, charandeepkapoor3@gmail.com, gerardo.gerry.pedrizco@gmail.com, j.vivekvamsi@gmail.com, lokeshwaran100@gmail.com, visheshdwivedi225544@gmail.com, bashybaranaba@gmail.com, detroitmetalcrypto@gmail.com, carlos@velascode.xyz, jsteerv@gmail.com, gmartinezgil@gmail.com, nishanthb.it2024@citchennai.net, stefanolombardo@posteo.de, kurodenjiro1@gmail.com, rahat@rahatcodes.com, yashj8858@gmail.com, laciferin@gmail.com, penrose@ultra.markets, arosejeremic5@gmail.com, weberfabian1@gmx.de, kulrajs.sabharwal.chy21@itbhu.ac.in

### Participants
 vasu_k@ee.iitr.ac.in,shikhar@iiitmanipur.ac.in,charandeepkapoor3@gmail.com,bashybaranaba@gmail.com,nishanthb.it2024@citchennai.net,yashj8858@gmail.com,felipe.sarmiento.as@gmail.com,stefanolombardo@posteo.de,visheshdwivedi225544@gmail.com,lokeshwaran100@gmail.com,kulrajs.sabharwal.chy21@itbhu.ac.in,carlos@velascode.xyz,singgihbrilian.tara06@gmail.com,gmartinezgil@gmail.com,rahat@rahatcodes.com,jsteerv@gmail.com,detroitmetalcrypto@gmail.com,kurodenjiro1@gmail.com,weberfabian1@gmx.de,gerardo.gerry.pedrizco@gmail.com,penrose@ultra.markets,ayushsrivas55@gmail.com,laciferin@gmail.com,j.vivekvamsi@gmail.com,arosejeremic5@gmail.com, vasu_k@ee.iitr.ac.in

### Date
 1770130800000

### Transcript Url
 https://app.fireflies.ai/view/01KG3ADMYRD5Q9H98G3VMWC5MS

### Audio Url
 No audio url

### Video Url
 No video url

### Duration
 31.65999984741211

### Meeting Attendees
 vasu_k@ee.iitr.ac.in, c_d903dd814ba91df26e63faa49c99624e6d19557ed1ae0bcb0eb9d659e9fea453@group.calendar.google.com

### Cal Id
 2s58vap0asiaqp3a7ulcc9i250

### Calendar Type
 google

### Meeting Link
 https://ethglobal.zoom.us/j/85088068959
