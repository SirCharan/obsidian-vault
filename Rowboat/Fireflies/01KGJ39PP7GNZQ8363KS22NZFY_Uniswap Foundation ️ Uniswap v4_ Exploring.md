---
tags:
  - rowboat
  - fireflies
  - transcript
---

# Uniswap Foundation ️ Uniswap v4: Exploring New Possibilities

**Meeting ID:** 01KGJ39PP7GNZQ8363KS22NZFY
**Date:** 2/5/2026, 2:00:00 AM
**Organizer:** soniavgallego@gmail.com
**Participants:** yashj8858@gmail.com, soniavgallego@gmail.com, kulrajs.sabharwal.chy21@itbhu.ac.in, jsteerv@gmail.com, arosejeremic5@gmail.com, weberfabian1@gmx.de, nishanthb.it2024@citchennai.net, laciferin@gmail.com, gmartinezgil@gmail.com, j.vivekvamsi@gmail.com, rahat@rahatcodes.com, singgihbrilian.tara06@gmail.com, felipe.sarmiento.as@gmail.com, stefanolombardo@posteo.de, visheshdwivedi225544@gmail.com, bashybaranaba@gmail.com, carlos@velascode.xyz, kurodenjiro1@gmail.com, shikhar@iiitmanipur.ac.in, penrose@ultra.markets, detroitmetalcrypto@gmail.com, ayushsrivas55@gmail.com, gerardo.gerry.pedrizco@gmail.com, charandeepkapoor3@gmail.com, lokeshwaran100@gmail.com, quierochiachida@gmail.com, daryl.cl.lim@gmail.com
**Meeting Link:** https://ethglobal.zoom.us/j/88931503630
**Duration:** 0m 18.290000915527344s

---

## Overview

Uniswap has evolved through four versions to enhance liquidity efficiency and developer flexibility, processing over $300 billion in swap volume and maintaining over $600 million in Total Value Locked (TVL). Key features of V4 include a singleton contract architecture and ERC-6909 token standard for improved token management and pool operations customization. During the hackathon, two $5,000 bounties were announced, targeting agent-driven systems and privacy-focused DeFi projects. Clear submission criteria emphasize functional code and community support on Discord. The Uniswap team, led by Angela Ocando, aims to position the platform as a leader in programmable liquidity and privacy-focused DeFi, inviting developers to innovate and reimagine liquidity management through modular designs and autonomous systems.

## Keywords

Uniswap v4, concentrated liquidity, singleton contract, hooks, agentic finance, privacy DeFi

## Action Items


**Angela Ocando**
Support hackathon participants in Discord throughout the hackathon duration (00:00)

**Hackathon Participants**
Submit project code with GitHub repo, clear readme, testnet or mainnet transaction proofs, and a demo video not exceeding 3 minutes prior to the February 8th 12:00pm Eastern deadline (14:30)

**Participants needing gas for testnet deployment**
Contact Uniswap team via Discord to request support for gas for testnet deployment (14:40)

**Developers interested in continuing Uniswap v4 development**
Apply for Uniswap Hook Incubator applications after the hackathon (15:50)


## Transcript


### Pascal
 Welcome you all to this amazing workshop by the Uniswap team.
 Angela is gonna go over everything that you need to know and everything that is possible with V4 and all the amazing prizes that you can potentially win by building something amazing.
 This will be around our 30 minute workshop.
 If you have any questions, feel free to post them in the chat.
 Please keep your microphone and your camera off.
 With that being said, Angela handing it over to you.
 Have fun.

### Angela Ocando
 Hey Pascal, thank you so much and welcome everyone.
 Hopefully you have a lot of fun during Happy Money hackathon.
 And yeah, today I want to guide you throughout some of the Uniswap before protocol possibilities.
 But first I want to start by saying hey, it's been one year since Uniswap B4 was launched and since then the protocol has been great, great, great, great achievements.
 More than 300 billion in swap volume, more than 600 million TVL and more than 23,000 hooks built and initialized.
 And yeah, today as I mentioned, we're going to throughout the Uniswap protocol evolution, a little bit of v4 background and its uniqueness and for sure how can you hack and hopefully win during hack money.
 Our prizes, some ideas and also a few resources for all of you guys too hack.
 But first let's dive in a little bit into the Uniswap protocol, which is tlbr, a peer to peer system designed for change in crypto, meaning that in a smart contract you're able to connect from one side liquidity providers, meaning the people able to put money out there and on the other one the traders, meaning people that want to swap, let's say ETH for usdc.
 So yeah, that is basically one of the majors capabilities of DEFI out there and it's been a journey for Uniswap since the beginning.
 The first version of the protocol was launched back in 2018, then the second version of the protocol back in 2020 and the third version of the protocol in 2021.
 But first of course really basic, you have the possibility trade ERC20 tokens to ether only.
 And then in the Uniswap v2 you had the possibility to finally trade any ERC20 to ERC20 token.
 At the time we had a constant product corp that I'm going to show you in a few seconds.
 And then in Uniswap V3, back in Uniswap V2 we have some capital inefficiency problems.
 In Uniswap V3 we introduced concentrated liquidity and a few other features such as morphe tiers and so on and so forth.
 By saying that TLDR there are currently four versions of the Uniswap protocol, Uniswap v3 introduces concentrated liquidity.
 Again, we're going to dive in a little bit.
 And then Uniswap V4 introduces the single tone, poor architecture and hooks.
 And in my opinion that enables unprecedented liquidity and pool customization.
 Meaning now the developers has the control to build anything out there on top of DEFI and their own AMMS uniqueness.
 Back in Uniswap V2, as I mentioned, they were a primary limitation which was basically capital inefficiency.
 The way the DEFI worked is throughout this formula, X multiply Y equals K, which means X and Y are the tokens A and B and the K is the constant moving over the curve.
 In that case, when you were adding liquidity, the whole like.
 Like here, when you were adding liquidity, the whole liquidity were spreading out the whole curve.
 In that case it wasn't that good for LPs to manage that liquidity and also for sure for traders in price executions.
 So that's when in.
 Back in 2021, Uniswap V3 was introduced with the same formula, but now at ranges of prices.
 Meaning whenever you wanted to add liquidity as an lp here you had the possibilities to say hey, you know what, I want to add liquidity in eth from 50, $100 to 2000 in that case.
 So it's not just good for price execution, but also LP profitability.
 So as you can see in the interface is really easy.
 But because now whenever you go and add your liquidity, you have the ability to set this custom range and that again that is good because now the liquidity is really using in an optimal way for both traders and liquidity providers.
 Remember that back in the day I show you that TLDR, this is my contract that connects from anxiety, LPs and on the other traders by saying that they then B4 was launched a year ago and it's the most customizable DEFI developer platform.
 It transforms the Uniswap protocol into a developer platform with unlimited customizability.
 So basically I want to show you some of the features that you might able to use here.
 The first one is singleton contract, meaning now whenever you want to do transactions and your project protocol idea, you don't have to jump between different contracts.
 Now everything happens inside the singleton contract, meaning if back in the day you wanted to trade ETH for dai, probably some of the routes that you would use is Like ETH to USDC and then USDC to DAI or ETH to USDT and then USD to dai.
 Of course capital efficiency is just one of the things, but now everything should be able to happen in the same contract.
 Meaning in the end the input is eth, the output is DAI and everything happens in between.
 So again, all pools in one contract and that's up to you.
 The other One is the ERC 6909.
 Basically it's like a new standard that allows you to manage different tokens inside the same pool manager.
 In that case again you get to move like different contracts and in Exchange all of us 20 tokens mint them as ERC 6909 representing their claim.
 So yeah, again you gotta move from ETH to DAI and move all of the movements in here happening inside the pool manager contract that we have for before.
 And in my opinion one of the most important things out there today for the defi space, maybe you've been hearing about clunker over the past few days around the agentic finance is hooks basically injecting custom logic between life cycle of mayor operations.
 In any operations that you might do you could add some sort of flags that allow you to add custom logic.
 You are the owner of this decision.
 So let's say we're going to start a swap in the program.
 These are optionals for sure, but if you add them before the swap this is going to check this flag and it's going to add whatever logic you add.
 So so let's say before the swap I want to check that X user is just an agent rather than a human.
 Why not?
 So you have the ability to do it.
 Whenever that flag happened, the swap is executed.
 And then you can also add a flag for the after swap.
 Meaning okay, now after the swap happened I want to donate part of the fees to X type of contributors we or X type of reasons.
 So yeah, again this is now custom logic that you can add at some point in the life cycle operations.
 Just want to make clear here that hooks are pool specific.
 So each liquidity pool in uniswap before can have its own hook contract attached to it and are called with the pool manager.
 As I mentioned before, hooks are optional for uniswap before pools but definitely a great feature for you guys to consider.
 I mentioned that you could add some possibilities before and after this up we have some of them so you could call before and after, initialize before and after at liquidity before and after, remove liquidity before and after swap before and after, donate you Name it.
 There's plenty of possibilities in here and there are some teams already building out there on top of V4.
 The first one again that you might listen over the past year days is Clanker, an AI powered token deployment platform that lets you create tradable crypto tokens on base and now with the whole mod book agents they're using the Clanker bot to deploy by default tokens in here and then the FEES distribution is really interesting around it.
 They the second one is Sora.
 Maybe you might heard about Sora in the past, but just basically decentralized social application protocol designed to let creators instantly trade their content by turning posts and profiles into tradable tokens as well.
 And if you go outside the defi space but also like position and analytics, Revert Finance is also a great example in my opinion that basically advanced position management tools and analytics on top of before with or without hooks.
 As I mentioned they're completely optional but great feature here.
 So yeah this is basically so far brief before introduction for all of you guys to consider and understand.
 Okay, should I use this?
 Okay now I want to create all of my contract and sell the pool manager.
 I want to use this ERC 6909 or you know what, definitely I want to create some agents that are using hooks in between to rebalance positions.
 I don't know.
 And that's why I want to bring you guys clarity on the Uniswap foundation bounty.
 Some of the ideas that we have for you.
 But feel free to build innovation out there, not just touch to it.
 We want you guys to build the next era of defi and you think there's two important things happening out there right now which is the agentic finance and the privacy defi.
 So we have $10,000 in prices for you today and the first one is agentic finance.
 So basically the bounty is for you to create agent driven systems on Yang.
 Before that manage liquidity, execute trades and coordinate on chain using optional hooks.
 I encourage you guys to go around and interact with hooks but yeah, definitely 100% optional for this hackathon in particular prices $5,000.
 For this in particular you could go to ethglobal.com events hack money 2026 prices units foundation.
 You're going to find all of the information.
 I also attached there a builder toolkit where you could also find all of this information so that way you don't lose any details.
 And if you go to discord at Ethglobal, me and my team were there to support you in every part of the process.
 So yeah, let's talk about a few ideas.
 As I mentioned again, more than strong recommendation.
 It's just like these are some of the ideas but you also feel free to go out there and transform the way that we are interacting with agents right now.
 So yeah, think about liquidity manager agent on Uniswap before that it deploys, rebalance and set fees.
 Or think about an MEV or agent that routes, swaps, adjust fees or split liquidity across unions v4 pools to reduce or manage MEV exposure.
 Or think about not even humans needed agent only pool management leveraging tools like the Clunchbot that I mentioned or the Clinker where agents create and manage Uniswap v forward pools with program mobile phone fee allocation.
 So again there's plenty of possibilities for humans and agents.
 The world is changing.
 So yeah, we want you guys to innovate in that field and then we have Uniswap before privacy defi where the TLDR for the bounty is create privacy aware systems that improve how information is handled during trading and equity provision while preserving on chain verifiability, transparency and the protocol integrity.
 So yeah, privacy is important, but for sure let's think about a great future in protocol integrity and industry integrity in all manners.
 $5,000 for this as well.
 Pascal just shared the details of the prizes and again if you go there you can find the Uniswap builder toolkit where all of this information is attached.
 And yeah again I don't want you guys to limit all of your ideas because I do think there's plenty of great ideas that I checked on the check in one.
 But think about maybe resilient execution that reduces unnecessary information leakage during swaps and liquidity updates or privacy where swaps execution that improves handling on timing, routing and liquidity updates while presenting fully on chain verifiability or why no, why not easing hooks that batch delay or coordinate execution on improved execution quality, price and information handling.
 So yeah, these are like some ideas you might think.
 Oh yeah Angela, this is the same sounds like it, but they have different approaches.
 One on the MVP side of the equation, the other on the information handling and the other on the price execution.
 So yeah, in privacy you might have different objective and I want to challenge you a little bit because why not we can also combine privacy and agents.
 I do think there's a few things interesting there that I would love to see in the future.
 And yeah, basically combine agent driven execution with privacy design to build more composable systems on top of Uniswap before just to make clear this for all of you guys, we don't want you to build necessarily an interface which is not required at all.
 But projects must demonstrate functional code, meaning me and our team really check the code.
 We really take the time to check your project and what you guys built, not just the idea.
 So please use this as an opportunity for you to learn, to practice, to hassle out there.
 But also we're going to take a look to the best projects executions.
 And yeah, for these admissions we encourage you to include the transaction.
 SV's can be testnet, can be mainnet, can be Unichain whenever you feel good about it.
 If you might need a gas visa or whatever, let us know on testnet in the Discord channel and our team is going to able to support you.
 And then a GitHub repo with a clear readme file and demo link or demo video max 3 minutes.
 Again, I do think it's great the future is happening in front of us, but we're here to check all of your ideas and support you in the process.
 These are some of the requirements.
 As for resources, finally I want to bring you guys three main resources.
 I left the source in here, but also you can scan this QR code which is basically Uniswap AI.
 This is a new tool that we're testing Uniswap specific AI tools which includes skills, blogging agents for developers and agents integrating in the Uniswap ecosystem.
 You also have Uniswap docs which is the whole information you need to understand our protocol, the Uniswap stock, but it's also LLM friendly so you could also plug your systems in here and we encourage you to use it.
 But most important, in my opinion Uniswap Hook incubator which is use this as a playground to understand if you want to continue building on top of Uniswap.
 And hopefully we can have you guys at the Uniswap Hook incubator applications closed right after hacked money ending.
 So you have time here to practice and hassle and then in the future hopefully I can see you guys the UHI next cohort.
 And yeah, that's pretty much it.
 My name is Angela Candle Debril at Uniswap Labs.
 I was presenting Uniswap Foundation Bounty today able to help if you need me Angelaanislab.org or at the Candlecryptor in all of the social medias but most importantly in our discord and influence discord me and my team were there to report and yeah, thank you.
 That's pretty much it.

### Pascal
 Pascal, that was absolutely fantastic.
 Thanks for all the shout outs.
 As you mentioned, the team is available on Discord and is really, really responsive on Discord.
 So you have any questions, my recommendation is always ask the question directly.
 Don't ask to ask a question that way.
 Much, much faster.
 Async event and everybody's going to have a great time.
 Yeah, thank you so much for this workshop.
 I hope everybody is building on Uniswap after this one.
 Everybody's utilizing all the tools that you're having.
 Fantastic documentation.
 A lot of people can learn from this.
 So much, much appreciated.
 Thanks for being with us.
 For everybody, this workshop is recorded.
 It's available at YouTube.com evegoble so you can always rewatch it and you still have some time to build the best possible project until the submission deadline, Sunday, February 8th at 12:00pm Eastern.
 Please do not wait until the last minute.
 Yeah, that's all from my end as well.
 Hope everybody has a fantastic day and see you all on Discord.

### Title
 Uniswap Foundation ️ Uniswap v4: Exploring New Possibilities

### Host Email
 safia@ethglobal.com

### Organizer Email
 soniavgallego@gmail.com

### Calendar Id
 7125hdggvv5dtn1emm53iuc1d2

### Fireflies Users
 felipe.sarmiento.as@gmail.com, ayushsrivas55@gmail.com, singgihbrilian.tara06@gmail.com, charandeepkapoor3@gmail.com, gerardo.gerry.pedrizco@gmail.com, j.vivekvamsi@gmail.com, lokeshwaran100@gmail.com, shikhar@iiitmanipur.ac.in, visheshdwivedi225544@gmail.com, bashybaranaba@gmail.com, detroitmetalcrypto@gmail.com, quierochiachida@gmail.com, carlos@velascode.xyz, jsteerv@gmail.com, gmartinezgil@gmail.com, nishanthb.it2024@citchennai.net, stefanolombardo@posteo.de, kurodenjiro1@gmail.com, rahat@rahatcodes.com, yashj8858@gmail.com, laciferin@gmail.com, daryl.cl.lim@gmail.com, penrose@ultra.markets, arosejeremic5@gmail.com, weberfabian1@gmx.de, kulrajs.sabharwal.chy21@itbhu.ac.in

### Participants
 yashj8858@gmail.com,soniavgallego@gmail.com,kulrajs.sabharwal.chy21@itbhu.ac.in,jsteerv@gmail.com,arosejeremic5@gmail.com,weberfabian1@gmx.de,nishanthb.it2024@citchennai.net,laciferin@gmail.com,gmartinezgil@gmail.com,j.vivekvamsi@gmail.com,rahat@rahatcodes.com,singgihbrilian.tara06@gmail.com,felipe.sarmiento.as@gmail.com,stefanolombardo@posteo.de,visheshdwivedi225544@gmail.com,bashybaranaba@gmail.com,carlos@velascode.xyz,kurodenjiro1@gmail.com,shikhar@iiitmanipur.ac.in,penrose@ultra.markets,detroitmetalcrypto@gmail.com,ayushsrivas55@gmail.com,gerardo.gerry.pedrizco@gmail.com,charandeepkapoor3@gmail.com,lokeshwaran100@gmail.com,quierochiachida@gmail.com,daryl.cl.lim@gmail.com, yashj8858@gmail.com

### Date
 1770237000000

### Transcript Url
 https://app.fireflies.ai/view/01KGJ39PP7GNZQ8363KS22NZFY

### Audio Url
 No audio url

### Video Url
 No video url

### Duration
 18.290000915527344

### Meeting Attendees
 yashj8858@gmail.com, c_d903dd814ba91df26e63faa49c99624e6d19557ed1ae0bcb0eb9d659e9fea453@group.calendar.google.com

### Cal Id
 7125hdggvv5dtn1emm53iuc1d2

### Calendar Type
 google

### Meeting Link
 https://ethglobal.zoom.us/j/88931503630
