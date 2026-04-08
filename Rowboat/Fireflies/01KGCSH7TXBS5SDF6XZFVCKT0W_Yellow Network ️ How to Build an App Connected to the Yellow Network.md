---
tags:
  - rowboat
  - fireflies
  - transcript
---

# Yellow Network ️ How to Build an App Connected to the Yellow Network

**Meeting ID:** 01KGCSH7TXBS5SDF6XZFVCKT0W
**Date:** 2/3/2026, 7:30:00 PM
**Organizer:** kulrajs.sabharwal.chy21@itbhu.ac.in
**Participants:** kaream.badillo@usach.cl, kulrajs.sabharwal.chy21@itbhu.ac.in, jsteerv@gmail.com, arosejeremic5@gmail.com, weberfabian1@gmx.de, detroitmetalcrypto@gmail.com, shikhar@iiitmanipur.ac.in, carlos@velascode.xyz, gmartinezgil@gmail.com, rahat@rahatcodes.com, kurodenjiro1@gmail.com, ayushsrivas55@gmail.com, singgihbrilian.tara06@gmail.com, laciferin@gmail.com, penrose@ultra.markets, bashybaranaba@gmail.com, yashj8858@gmail.com, lokeshwaran100@gmail.com, stefanolombardo@posteo.de, felipe.sarmiento.as@gmail.com, daryl.cl.lim@gmail.com, charandeepkapoor3@gmail.com, j.vivekvamsi@gmail.com, visheshdwivedi225544@gmail.com, steven@yellow.com, gerardo.gerry.pedrizco@gmail.com
**Meeting Link:** https://ethglobal.zoom.us/j/89393361329
**Duration:** 0m 30.170000076293945s

---

## Overview

Yellow Network aims to create a next-generation platform for instant financial and gaming applications with minimal fees, addressing the inefficiencies of current decentralized exchanges. Stephen Zeiler highlighted its ability to replace centralized brokers with code, allowing users direct control over funds and transactions that settle in under 100 milliseconds. The platform utilizes state channels for off-chain interactions, currently integrates with seven chains including Ethereum and Polygon, and features a secure withdrawal mechanism. Developers benefit from an easy-to-use SDK for building applications without deep blockchain knowledge, while users enjoy fee-free transactions within app sessions. The Yellow Network is also fostering developer engagement through accelerator programs and active community support, striving to establish itself as a leading platform for trustless applications by 2026.

## Keywords

Yellow Network, state channels, trust-minimized apps, multi-chain, Ethereum, instant transactions

## Action Items


**Steven Zeiler**
Provide contract addresses for Sepolia adjudicator and custody contracts in documentation and share relevant links with workshop participants (16:26)
Post links to code tutorials and documentation for Yellow SDK and network to workshop participants (29:09)
Organize and promote Yellow Accelerator sessions and support developer engagement via Telegram and other channels (29:09)

**Aubree I ETHGlobal**
Facilitate ongoing support and encourage participants to ask questions in Discord after the workshop (29:35)


## Transcript


### Aubree I ETHGlobal
 Okay.
 Good morning everyone.
 Welcome to a workshop for Hack Money 2026.
 Hope you guys projects have been going great so far.
 Today you'll be hearing from Stephen from Yellow.
 And so Stephen, have a great space.
 I'll be here in the background if you need anything.

### Steven Zeiler
 Thank you Aubrey.
 And welcome everyone.
 Thanks for being here.
 My name is Stephen from the Yellow network@yellow.com where we are building a next generation of trading and financial applications platform.
 And I'm very happy to present today how to build an app using the Yellow Network.
 And hopefully you can see my screen now.
 Yeah.
 So welcome to building an app.
 The Yellow Network is a platform for building trust minimized or trustless applications.
 So we all know that Bitcoin came onto the scene over a decade ago and changed the way that people trust their money.
 The old way was that bankers control your money.
 They can freeze your account at any time and you need permission to move your money.
 And there's a lot of security problems with trusting third parties with your money.
 And Satoshi Nakamoto solved that problem by making it so that you control your money and you can send to anyone at any time.
 And most importantly, the mass replaced trust trust in issuing the currency, the supply and the transfers.
 And then the next step from Bitcoin was when Vitalik and team created Ethereum which further eliminated the need for trusting middlemen when it comes to enforcing contracts and applications.
 So instead of needing lawyers to create things like tokens and participate in applications, you no longer needed to trust those you could trust smart contracts to enforce your code, remove the middleman and have instant or at least close to real time enforcement of your agreements and programmable agreements.
 So Ethereum's innovation was replacing lawyers and trust with smart contracts.
 But as every Ethereum developer knows, there are still a lot of user experience problems with building applications on Ethereum.
 And the next evolution, chapter three in the evolution of trust is the Yellow Network.
 And the Yellow Network does is it replaces brokers or trusted third parties with apps with code.
 So in the past users would have to trust platforms and applications with their money.
 Like an exchange, you have to deposit your money in that exchange and give give control of your funds over to that exchange.
 Or with a game, you would need to deposit funds into a game server in order to use the money in that game.
 And of course on the blockchain things are a little bit slow to confirm, you know, 10, 5, 10, 15, 30, 60 seconds isn't that slow.
 But when you're making a real life application like a normal website web app, mobile app that people use.
 People expect that to be instant.
 So that's really a big pain point in the user experience.
 But even worse, expensive fees.
 So the Yellow Network creates a platform where people can build apps without central trusted brokers.
 And you can create trading venues where you can rely more on the code and less on a corporation to hold your funds.
 And we can create games and apps that are more peer to peer and trustless.
 And most importantly that the experience is instantaneous.
 Things happen as quickly as a click and for basically free, essentially no gas costs.
 So the pattern is clear.
 Crypto removes trust and the Yellow Network takes that to the next level and lets us build really fast, really cheap, really great user experiences on top of the blockchain infrastructure that already exists.
 And so you've probably used Dexes before.
 And dexs are awesome because they give you control over your funds, but they're slow and they're expensive to transact.
 And if there's Network congestion, your transactions might take a long time.
 And when you're trying to trade for traders or you're trying to build applications, these block confirmations and the slowness makes things really unpredictable sometimes.
 And in the traditional finance, traditional trading things happen in 100 milliseconds or less, right when you go to pay you the Apple pay, anything like that, trading in a traditional exchange, they're really fast, but dexs are pretty slow and that causes a lot of problems.
 But even worse is that you're paying a lot of fees to, to transact on decentralized exchanges.
 So you, you get to keep control on a dex.
 But gas fees might be $0.02, $0.05, a dollar, $10 even, they can go even higher depending on the Network congestion.
 And if you want to do lots of interactions and have a really great experience, that's going to become prohibitively expensive for a lot of people.
 And so that really reduces the audience that you can have in your application.
 Your game building on the blockchain.
 So fundamental problem here is that centralized platforms require trust, where you have to trust them and you have to give them funds.
 And what you want is actually to have control of your funds and control of your trade and have more trust, minimized or trustless interactions.
 And of course it's kind of insane how much you can pay on Dexes and interacting with smart contracts.
 But we all love web3 and the power of using blockchains to settle currencies and to have digital cash, there has to be a better way.
 So Yellow Network helps you build apps without brokers, without a central third Party a middleman, a broker is a middleman who you give your money to in order to then interact with someone else with your, your other player or the person you're trading with.
 And so we can instead build applications with no middleman where people can transact directly and also maintain the benefits of instant like 1 millisecond super fast transactions.
 As soon as you click a button, funds are transferred or your game updates.
 It's very hard to build a game when you have to wait 5 seconds, 10 seconds or more.
 Okay, so the Yellow platform gives you the ability to build these applications.
 What we'll cover here is the technology behind and how it works and some examples of code to get you started to give you an idea of how to build with the Yellow SDK and the Yellow state channels.
 So the, the technology, the fundamental technology that enables us to build this platform are called state channels and they help enable peer to peer interactions.
 And we're seeing people building trading platforms, defi protocols, prediction markets and different games where the users of these applications don't have to trust the developers with their money and they get a trusted platform for building real time apps all out of the box.
 So I appreciate everyone being here and yeah, okay, I see, I see a question and feel free to ask the questions at any time.
 So someone Levon asks what Yellow offers with state channels is somewhat similar to the Lightning Network and that is a lot of kind of true.
 The Lightning Network is a way to make instant payments and instant transfers of information and money on top of the Bitcoin Network.
 And Yellow Network enables the Yellow brokers enable that same kind of thing but across multiple different chains and especially focused around Ethereum compatible chains and with more chains coming.
 So it's kind of analogous to the Lightning Network but more of a generic platform for building apps.
 Lightning Network is one app which allows you to transfer satoshis and Yellow Network is a platform for building apps like that.
 So please let me know if anyone has heard of state channels before or if there are any layer two that you have used before.
 And of course if you've experienced problems or slowness with DEXS or smart contracts.
 But the, the Yellow architecture is multi chain so we connect to a bunch of different chains so far, seven chains and there will be more coming online as we have developers asking for access.
 And the Yellow Network or the Yellow broker creates a unified experience across all of these chains where you can get a single balance of stablecoins or other assets.
 And it's all connected in through state channels to the various Blockchains and the way that works is the Yellow Network has deployed smart contracts onto each blockchain.
 And so there's two contracts.
 The first is a custody contract and this is how you securely lock funds into the Network.
 When you, when you deposit into the Yellow custody contract it you, your funds on chain are now available for use off chain within any of the applications on the Yellow Network.
 So you lock your assets in and it's different from depositing your funds in an exchange like Binance where there you just give them your funds but in the Yellow custody contract they're locked in a contract and you still maintain a high level of control of your funds because there's a second contract that it works with called the adjudicator which enforces the rules and allows you to dispute any problems with the fund.
 So if there's any issue with the Yellow Network or the Yellow Network goes down or there's something unfair happening, you can prove cryptographically and withdraw your funds on your own.
 And that uses the adjudicator contract.
 And so how does, how does this work?
 Basically you deposit into the custody through a state channel and then you get, you get your assets once they're in the channel.
 A channel is like an on and off ramp into the Yellow Network.
 And once your assets are in the Yellow Network you can use them in all the applications in the Yellow Network and trade instant, instant trades, instant transfers and secure multiplayer applications that people are building.
 And on the same way the state, the channels to the blockchain allow you to withdraw your funds out of the Network back onto the chain they came from or onto another chain.
 And so you can withdraw on your own without having to ask permission.
 So with a traditional trading environment like Binance Kraken, when you want to withdraw, you request from them to withdraw and then they send you your money.
 But with the Yellow Network you create a withdraw action on the smart contract and that lets you withdraw your own funds without permission back into the chain.
 Suhas says what's the Sepolia adjudicator contract I want to deposit the contract addresses are listed in our documentation and I can, I can post a link to there shortly.
 But for each, for each chain there is a specific contract address.
 And.
 We have our SDK provides some tools to easily interact with the, the various contracts.
 So you get a nice high level developer tool experience for calling the contracts.
 Yeah.
 So the most crucial part about the, about the Yellow Network compared to a more a different platform is that it has trustless on chain settlement so you can Withdraw your own funds if anything happens to the application or the Network, even if the Yellow Network entirely goes down, using your Ethereum keys or your base keys, or using your own keys, you can withdraw your funds.
 So you maintain a high level of control over your assets and that lets us build a much more secure and much more reliable platform for developers.
 And you never really have to trust Yellow.
 And then on top of that, Yellow provides a unified ledger.
 So if you've used, let's say if you deposit USDC to Binance, you no matter which chain you deposit on binance credits you with USDC.
 You deposit 100 USDC, you get USDC.
 And that's the same way that the Yellow Network works.
 You get a unified balance.
 So as an application developer, you don't have to know which chain your users are using, where the funds are coming, or even where they want to settle, ultimately settle their funds to which chain.
 You don't have to know anything about that.
 You get a unified balance.
 So you can just use tether or USDC or ETH or other supported assets within your application without having to worry about the underlying blockchains.
 Is is avalanche chain supported?
 Avalanche chain that is EVM compatible, then it can very easily be supported.
 I admittedly don't know the answer.
 Let's see, here we go.
 So we don't have avalanche chain supported yet, but I assume we can deploy the same smart contract to that chain.
 And most chains with smart contracts support can be supported by the Yellow Network.
 Whenever there's a developer use case or an economic reason to add a chain, we can add that chain.
 So we support these seven chains so far, Polygon base finance chain, Ethereum, Linea and some more.
 All right, so the Yellow SDK makes all of this possible and easy and it's built on the same principles as on chain transactions.
 It uses the same cryptographic signatures as normal on chain transactions and it allows for multi party applications with multi signature.
 So you can build apps like auctions or escrow betting, even multiplayer games that have tokens or stable coins in the game.
 And especially people are building trading platforms and prediction market platforms where they want very fast instant transactions.
 And it's a pretty simple API, so you don't have to get too far into the low level of blockchain programming even in order to build an application on the Yellow Network.
 And yes, can Yellow support testnet?
 Yes, Yellow supports several different testnets and we have a testnet, we have yUSD for testnet.
 So you can get yUSD stablecoin on and then Withdraw it to the various test nets.
 And that makes it easy to build without having to even spend any fees on gas when you're onboarding or offboarding funds from the Network.
 Okay, so once when you're building your application, the key, the key concept is what we call an app session, which allows your app to have their players and their participants bring funds into your application and use them according to a set of rules that you define.
 So it's really good for negotiating a deal trading any peer to peer application and the users have to sign off on changes to the application state or updates to the balances of funds that they have between and they sign off with their normal keys.
 So like their normal Ethereum keys and all of their updates can happen within this app session instantaneously with no gas fees and only if the users after they finish with the app, if they want to withdraw their funds off the platform, then they will pay a gas fee to withdraw.
 But you any action interactions within your app session have no gas fees and zero latency.
 Essentially.
 Favor says will there be pop ups?
 We have so far no.
 People are building applications where you can authorize a session with your funds and then once you authorize a session key, you can interact instantaneously and sign transactions without a pop up to your wallet.
 So there's a pop up one time when you authorize the application session and then after that you can interact freely without pop ups.
 So it really makes the experience a whole lot better for all kinds of applications.
 Thanks for all the questions everyone.
 The first step is we have our SDK.
 Yellow TS is a tool that I've personally worked on that makes it easy to connect to the Yellow Network and manage your connection.
 This Nitrilite package.
 Let's see if I can zoom in.
 Nitrilite package.
 This is the tool set for the Yellow protocol and for interacting with the state channels and building up all of the messages.
 Then VM we use a lot for this is the library for interacting with Ethereum keys and signing, creating signatures so that we can securely authenticate.
 The first thing you do is you connect to the node and then you authenticate your wallet by signing a Ethereum standard message authenticating your wallet and then you get a session key that becomes your signer for the application and then you don't have to prompt anymore.
 By the way, this works in both the browser and in the back end.
 So you can create server based applications or you can create entirely browser based applications or a combination of both.
 Great.
 So when you're building your application essentially you define your app and you say who's participating in the application.
 And then those are the signers that you want to have in your app and you give them weights so that.
 And you define a quorum so that you know how many signatures are required in order to approve an update to the state, which could be an update to your game state, an updated negotiation, or it could be a balance transfer between parties.
 And you can have more than two, you can have various different players and you have a quorum.
 And then when you want to update the state, you have the, you start your session and then you have the users sign the state.
 And this happens in memory so you don't have to prompt the user again.
 And we have functions for creating state update messages that then are signed by the various participants.
 And you could have two parties or you could have three parties.
 For instance, you have two players plus a server where one player and the server have to sign off or both players have to sign off.
 And you can have that all happen in real time and very easy.
 With our SDK, these functions are coming from our SDK.
 So rather than doing a calling a contract on chain like you would with an on chain transaction, you call a state update in the Yellow broker and that updates the state.
 But first it verifies the signatures.
 So in this case, when you have multiple parties who are signing you, you first have one party sign and then you need to have the other party sign and attach both signatures and then send that update to the Yellow broker node and the state will update.
 And all updates happen.
 They require a quorum of signatures and it's cryptographically verified.
 And when you're done with the application, you can close the session, have people, the players sign off to close the session, and then their funds are released back into their normal, their normal balance.
 So here's in summary, the complete flow.
 You connect to the node and authenticate with your Ethereum keys, and then your users join a session, an application session that you've defined.
 They can interact, play the game, update the state update balances, and they all sign off on all of these updates, so it's all cryptographically verified and secured.
 And when they're done, they sign off and close the state.
 And now you have a trustless instant application with real time playability and no blockchain fees during the application.
 So thank you very much for listening and learning today.
 We cover the basics of the Yellow Network and we have telegram channels where a lot of developers are currently participating.
 We have a Yellow accelerator that we just launched our cohort for Q1 and we'll have more, more accelerator sessions every quarter where people are building their apps and there are, there are prizes and pitches and we help promote their apps.
 And all of this is instant, no gas fees and very much trustless.
 So here you can see a link to my code tutorials that I've been making and we have a lot more information on our documentation page@yellow docs.yellow.org so thank you.
 And we have about one minute left for any additional questions.
 Any privacy obfuscations happening here?
 All of the application interactions are not happening on chain.
 They're off chain.
 So there's an additional element of privacy privacy there.
 All right, I'm at the end of my 30 minutes.
 Thank you everyone for joining.

### Aubree I ETHGlobal
 Amazing.
 Thank you so much, Stephen.
 If you guys have any further questions, please feel free to ping in the discord.
 And good luck with all of your projects.

### Title
 Yellow Network ️ How to Build an App Connected to the Yellow Network

### Host Email
 safia@ethglobal.com

### Organizer Email
 kulrajs.sabharwal.chy21@itbhu.ac.in

### Calendar Id
 286bkut6t12n974p1vql76bi89

### Fireflies Users
 felipe.sarmiento.as@gmail.com, ayushsrivas55@gmail.com, singgihbrilian.tara06@gmail.com, charandeepkapoor3@gmail.com, gerardo.gerry.pedrizco@gmail.com, j.vivekvamsi@gmail.com, lokeshwaran100@gmail.com, shikhar@iiitmanipur.ac.in, visheshdwivedi225544@gmail.com, bashybaranaba@gmail.com, detroitmetalcrypto@gmail.com, steven@yellow.com, carlos@velascode.xyz, jsteerv@gmail.com, gmartinezgil@gmail.com, stefanolombardo@posteo.de, kurodenjiro1@gmail.com, rahat@rahatcodes.com, yashj8858@gmail.com, laciferin@gmail.com, daryl.cl.lim@gmail.com, penrose@ultra.markets, arosejeremic5@gmail.com, weberfabian1@gmx.de

### Participants
 kaream.badillo@usach.cl,kulrajs.sabharwal.chy21@itbhu.ac.in,jsteerv@gmail.com,arosejeremic5@gmail.com,weberfabian1@gmx.de,detroitmetalcrypto@gmail.com,shikhar@iiitmanipur.ac.in,carlos@velascode.xyz,gmartinezgil@gmail.com,rahat@rahatcodes.com,kurodenjiro1@gmail.com,ayushsrivas55@gmail.com,singgihbrilian.tara06@gmail.com,laciferin@gmail.com,penrose@ultra.markets,bashybaranaba@gmail.com,yashj8858@gmail.com,lokeshwaran100@gmail.com,stefanolombardo@posteo.de,felipe.sarmiento.as@gmail.com,daryl.cl.lim@gmail.com,charandeepkapoor3@gmail.com,j.vivekvamsi@gmail.com,visheshdwivedi225544@gmail.com,steven@yellow.com,gerardo.gerry.pedrizco@gmail.com, kaream.badillo@usach.cl

### Date
 1770127200000

### Transcript Url
 https://app.fireflies.ai/view/01KGCSH7TXBS5SDF6XZFVCKT0W

### Audio Url
 No audio url

### Video Url
 No video url

### Duration
 30.170000076293945

### Meeting Attendees
 kaream.badillo@usach.cl, c_d903dd814ba91df26e63faa49c99624e6d19557ed1ae0bcb0eb9d659e9fea453@group.calendar.google.com

### Cal Id
 286bkut6t12n974p1vql76bi89

### Calendar Type
 google

### Meeting Link
 https://ethglobal.zoom.us/j/89393361329
