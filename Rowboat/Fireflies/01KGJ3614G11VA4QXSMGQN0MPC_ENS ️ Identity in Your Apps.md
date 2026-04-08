---
tags:
  - rowboat
  - fireflies
  - transcript
---

# ENS ️ Identity in Your Apps

**Meeting ID:** 01KGJ3614G11VA4QXSMGQN0MPC
**Date:** 2/5/2026, 1:00:00 AM
**Organizer:** visheshdwivedi225544@gmail.com
**Participants:** meek10x@gmail.com, visheshdwivedi225544@gmail.com, bashybaranaba@gmail.com, carlos@velascode.xyz, kulrajs.sabharwal.chy21@itbhu.ac.in, lokeshwaran100@gmail.com, nishanthb.it2024@citchennai.net, yashj8858@gmail.com, jsteerv@gmail.com, soniavgallego@gmail.com, arosejeremic5@gmail.com, felipe.sarmiento.as@gmail.com, penrose@ultra.markets, quierochiachida@gmail.com, laciferin@gmail.com, j.vivekvamsi@gmail.com, rahat@rahatcodes.com, stefanolombardo@posteo.de, kurodenjiro1@gmail.com, shikhar@iiitmanipur.ac.in, gerardo.gerry.pedrizco@gmail.com, detroitmetalcrypto@gmail.com, daryl.cl.lim@gmail.com, ayushsrivas55@gmail.com, charandeepkapoor3@gmail.com, singgihbrilian.tara06@gmail.com, weberfabian1@gmx.de, gmartinezgil@gmail.com
**Meeting Link:** https://ethglobal.zoom.us/j/81757822000
**Duration:** 0m 30.989999771118164s

---

## Overview

The meeting discussed the integration of Ethereum Name Service (ENS) to simplify user interactions by replacing complex hex addresses with human-readable names, enhancing user confidence. Greg Skriloff highlighted the importance of ENS as a portable Web3 profile, improving clarity in transactions and governance, especially for new users. There was an emphasis on supporting both Externally Owned Accounts (EOAs) and smart contracts, with discussions on decentralized website hosting and flexible payment preferences through ENS text records. The meeting also introduced cash prizes to incentivize developers for innovative uses of ENS and stressed security practices for ownership of ENS names, recommending the use of hardware wallets for safe management.

## Keywords

ENS, Web3 Identity, Decentralized Websites, Forward and Reverse Resolution, Payment Preferences, Ethereum Mainnet

## Action Items


**Greg Skriloff**
Assist hackathon participants with free ENS name claims via Discord channel support (07:30)
Provide detailed resources on subdomain issuance and ENS integration, including Durin and reverse record sponsors (21:20)
Support developers in setting reverse records, verifying multi-chain addressing, and implementing smart contract ENS names (10:28)
Be available on ENS developer Telegram and Discord to answer ongoing questions and provide guidance during the hackathon (29:48)

**Hackathon Participants**
Integrate ENS resolution into apps by replacing hex addresses with ENS names in input fields and transaction displays to improve UX (21:48)
Consider building ENS-based projects such as decentralized websites, payment preference routing using custom text records, or subdomain issuance using Durin on L2 networks (15:24)
Explore creative usage of ENS identities for wallets, social apps, AI agents, or DeFi payouts during hackathon submissions to qualify for prizes (18:24)
Use the Sepolia testnet ENS app for development to avoid real money expenditure (24:18)
Join ENS developer groups and Discord partner channels for real-time support and collaboration (29:48)


## Transcript


### Pascal
 Your apps with Greg.
 He's going to talk about everything that ENS can do for you during this hackathon.
 And without further ado, I'd like to hand this over.

### Greg Skriloff
 Have fun.
 Awesome.
 Thanks, Pascal.
 I am so.
 Hey everyone, I'm Greg.
 Excited to be here with you today.
 I'm going to try.
 I'm just on a monitor, but I'm going to try and keep the chat open side, so if you have questions throughout, feel free to ask.
 And if you have questions after also, you can ask then.
 And I'll get to them then.
 Going to try and keep an eye on everything.
 So let's get started.
 First of all, again, I am Greg Devrel, engineer at ENS Labs, and today we're going to be talking about ENS as a source of identity in your apps.
 So I'm going to start with the basics and then get into some more specific examples of how you can.
 Excuse me, how you can use ens.
 Okay, take it slow.
 So.
 And I have to move the chat so I don't cover my own slides.
 Okay.
 Should be fine.
 So ENS or the Ethereum name service, is a decentralized, permissionless naming protocol that lives on Ethereum and scales to the entire Internet.
 At a high level.
 We turn complex hex addresses into human readable names.
 So obviously in crypto there's addresses everywhere, like this one, OX179A, so on.
 And that is very confusing and bad for user experience and new users just don't understand what that is.
 And so ENS prescribes names like gregscroll Eth to the addresses.
 And the goal is that anywhere you see an address or anywhere you would have seen an address, you can instead see a name.
 And we'd like to think about ENS as a user experience protocol.
 We exist to make your application and Ethereum and really all of Crypto easier to use.
 You can imagine the before and after.
 It's like you get coffee with somebody at a cafe and the before is having them pay you back in USDC to, you know, some, some long address.
 And this, obviously you can't say, you can't remember.
 If you do say it, somebody's going to type it incorrectly and so on.
 And so you'd have to copy and paste it into a chat app and then they'd have to copy and paste it into their wallet app and then you'd have to double check it.
 And this whole thing, that's annoying.
 And the alternative is just saying, send me $5 to Greg Scroll ETH and that's easy to spell, easy to say, easy to type, much better user experience.
 And this is kind of just talking about ENS as a username, but really over time it's gone from just a username to more of a well rounded profile.
 And so this is a view of my ENS profile.
 You see the name up here, I'm not sure if you can see my cursor, but you see the name GregScroll, ETH and my address.
 But you also see a bunch of other things.
 So, so I have this banner image and I have this description saying that I like baking and building apps on Web three protocols and addresses on different blockchains, including non EVM chains like Bitcoin and Solana.
 And you see links to social records and kind of all this different stuff.
 And so again, this is just to say that ENS is not just a address to a name mapping.
 It is more than a username.
 It is really this decentralized profile, this portable Web3 profile that goes with you across Web3.
 And if you have an ENS name or I guess in this slide, even if not, you will probably recognize this flow.
 You know, when you connect to an application, you will press the Connect Wallet button and then see maybe like a gray box or a random generated image and your address and this, you know, is your address.
 But it doesn't feel very private personable.
 It feels very random.
 Almost like when you get an email, like a marketing email, and it literally has curly brackets around like insert name here or something.
 And this is just the experience that is very common around crypto or around Web3, but we don't think is really good enough.
 That feels bad.
 Nobody likes that experience.
 And so if your application integrates ENS and a user comes to your app that already has an ENS name, their experience is much better.
 They press Connect Wallet and they are greeted with this, their name, their avatar, any other relevant information that you might want to surface in your app.
 And it's really just like showing up with your account.
 They know who they are, you know who they are, and it's a better end to end experience.
 And these are just a few examples of kind of how it shows up in the wild on snapshot.org, which is a popular governance app.
 I will go there and it recognizes me as Greg Sri Laith.
 It shows my preferences and all this stuff, even if I haven't signed in before.
 And so it's better for the app developer because it also brings context to the app.
 And another example down below, basically same thing you sign in and you see your profile and it feels great.
 Another comparison before and after and I see some questions coming in that I will get to in a second.
 This is on Etherscan, I send a transaction to a smart contract and that smart contract has a name.
 I can very easily see what's going on here, maybe especially if I saw the function name or me receiving something in from RealCameron eth.
 This is very easy to see.
 Just Cameron to Greg.
 Whereas the two kind of counter examples below, a random set of characters and numbers sending something out to another set of random numbers and characters.
 And this is, you know, kind of meaningless.
 I don't know what's happening here.
 I'd have to click in and look at a bunch of information to figure out what that is.
 So the point here is that ENS brings context to your apps.
 This is kind of from a reading past actions perspective.
 And then on the right is sending assets to an ENS name very easily.
 So this is the most immediate like use of ens, which is again the username part.
 So it's like profile type thing on the left, usernames on the right.
 Just to reiterate.
 And yeah, like I said earlier, the idea here is that users of crypto powered experiences should never have to interact with a hex address.
 ENS is here to solve that.
 And really anywhere you read or write a hex address, you should be able to use an ENS name.
 So those are kind of the basic intros, what your experience might look like before and after, why you might want to integrate ENS and stuff like that.
 I'm going to take a second to catch up on the questions and then we will move forward.
 Okay, are the non Ethereum addresses verified or could you add any address?
 It is not verified.
 You could add any address to a name like this.
 And then in an upcoming slide I'm going to talk about a kind of reverse process that verifies an address for a given name.
 Yeah, and so this data is just write only.
 I could write anything here.
 It doesn't have to be an address that I control.
 And then next, how can we claim a free ENS name for the hackathon that is part of the Eth Global Hacker Packs and should be accessible to everybody.
 But we can probably help you with that afterwards.
 Yeah, it's more of a tech thing, but we'll get you sorted, maybe send a message in the discord channel so we can help you with that later.
 Jack, I think that was.
 And then there's another question.
 What about Multi chain.
 Yeah, many of the addresses here are in multiple chains.
 So the name by default, a Ethname, lives on Mainnet Ethereum, and you set your address for different chains, but still on L1.
 So L1 is like where your data lives and it can point to data on other chains.
 It is possible to set up ENS names in a way where the data itself, like these text records or these address records are stored on other chains.
 And I believe I will get into more detail on that later.
 And if not, you can ask again later.
 And I will make sure to go into more detail, but just want to make sure we get through the core parts.
 But thank you guys for asking questions.
 I think it's.
 It's nice to stop halfway and ask questions instead of going all the way through, but hopefully that kind of helps for you.
 Okay, cool.
 So, yeah, basic intro to ENS and why it's important.
 Now, how does it work?
 So there are two main processes in ENS that are important to know from the get go.
 There is forward resolution, which is the ability for a name to point to an address on any number of chains.
 So for example, nick eth is an ENS name and it resolves to this address, ox, b8c2, so on on these different chains.
 And so if I am in Metamask or RNBO and so on, and if I go to send NIC ETH assets on these chains, I can just type in the name instead of copying and pasting the address.
 And it is an easier way to send assets to NIC eth.
 The opposite is reverse resolution.
 So it's a mapping of an address to a name.
 And this also exists on multiple chains.
 So I can have my reverse record on Ethereum mainnet be different than my reverse record on Base or Optimism or something like that.
 And the way you can tell for sure that a person controls a given name, or rather that an address and a name are verifiably linked, is if both of these kind of equal the same value.
 So if the name points to the address and then you look at what address the name points to and these two things are the same, then you have what we call a primary name.
 And a primary name is really your source of identity on Ethereum.
 That is what allows apps to safely show instead of 0x179A that I am Greg scrolled at ETH and this is my avatar and stuff like that.
 So the primary name is kind of the culmination of those two features.
 Okay, I see a question that, yes, we will get onto a bit later.
 And so yes, these reverse records, again, this part, the bottom part, are available to set on Ethereum, mainnet and then five different L2s that is not currently available on non EVM chains, which I think was one of the questions earlier.
 So yes, the verifiable addresses are only on these chains and their respective testnets for the sake of the hackathon or for development.
 And the contracts that enable you to set that reverse mapping are very simple.
 There is a set name function that any address can call on its own, whether it's a smart contract or a eoa.
 And then there's also a set name for address which allows you as a developer to sponsor the setting of a reverse record, basically.
 And so you could have a seamless experience for your users.
 And there are example repos that, you know, make this super easy to do if that's something you're interested in.
 And that really makes for the optimal user experience.
 They can sign into your app.
 Maybe you can.
 Oops, maybe you can give them a name for free, which we will touch on in a bit.
 And then you could sponsor setting their reverse name.
 So whenever they go to other apps in your app, you can kind of recognize their profile as again, this portable Web3 profile.
 And yes, this names.
 This works for both EOAS and smart contracts.
 So smart contracts can have ENS names and they can have primary names as well.
 Okay, so that is the more obvious features of ens, I would say, or the ones that have gotten the most attention.
 Then a few other things that I want to touch on first is decentralized websites.
 And this has been possible with ENS for a while, but we're talking more about it as Cloudflare is starting to have more outages, even like during DevConnect.
 Cloudflare went down, but decentralized websites on ENS could still be used.
 And this was a really cool way to demonstrate why it's important for crypto websites, and especially at this hackathon being for Defi.
 For Defi websites, it's important that we're not dependent on a single company like Cloudflare to keep all of the websites accessible.
 And here's a kind of maybe overwhelming diagram that shows the process of deploying a decentralized website on ens.
 But I'm just going to break it down real quick.
 Basically, a decentralized website on ENS is the combination of a few pieces of technology.
 I can upload my website content to some sort of persistent storage like ipfs or Swarm or Arweave or Kind of any decentralized storage network, and then store that hash of that content basically in my ENS name.
 And then there are a number of gateways that will easily allow you to access that content in a much easier way.
 And so on the upload side, there's a tool called Omnipin, which I believe I will link to later, that allows you to kind of coordinate all this stuff.
 And then on the gateway side, there are a number of options.
 And I spelled Vitalik wrong.
 But anyways, if you've followed Vitalik's blog, you might notice that he shares it as Vitalik Eth Limo or Eth Link.
 And these are gateways that in the background fetch the content hash record, which is the hash of the decentralized storage upload from your ENS name.
 They serve that content to you under a domain.
 And so it's very easy for you to access this content under Vitalik Eth Link.
 And this is meaningfully decentralized because there are a number of these gateways like Link Limo Sucks and so on.
 So Eth Link, Eth Limo.
 But the coolest part is actually that you can run your own gateway, and this is the most decentralized way to access this content.
 And so, for example, I run one under my local network where I can access Vitalik's blog, or I can access our ENS application or our ENS documentation fully decentralized through my own Ethereum rpc, through my own IPFS gateway, and through the content that Vitalik or ENS has kind of declared official under its ENS name.
 And so this, like, decentralized website stack is something that we want to push a little bit harder and I think is important to highlight in a defi hackathon, where your smart contracts may be decentralized, but there has to be an easy way for people to use that as well.
 So that's an area we want people to explore with.
 Another cool area to explore is custom text records.
 So ens, as I showed in the profile earlier, has a number of text records, which means arbitrary, which are arbitrary key value pairs that are just string to string attached to an ENS name.
 And so, for example, a common one is the key avatar, and the value is a URL that points to a profile picture.
 But there can be really cool ones that store things like payment preferences or defi patterns.
 And what this might look like as a hackathon project is you set a text record key that is like preferences or something, and the value is like a stringified JSON object that has the chain and the asset that you want to be paid out in.
 And if you're building a wallet or an app that transfers assets, instead of letting the user decide the one who's sending the assets where the assets will end up, or just assuming that the receiver wants to get the same asset that the sender is sending, if that makes sense, you can intelligently use this to basically route assets to the place where the receiver only wants them.
 And so say you have ETH on Arbitrum, and I say, back to the example, send me $5 for coffee.
 You shouldn't have to ask me what chain and what asset I want the $5 on.
 I should be able to just say, send me the $5.
 And so a Hackathon project that could be really cool is coming up with a standard that allows me to set a text record that says my preference for payouts is always USDC on base.
 If I say, pay me $5, I don't care how you pay, I want it to settle in my wallet in usdc.
 And then the Hackathon project is kind of the standard for what defines that text record.
 Maybe it looks like this, maybe it's something else.
 And the router logic that, you know, swaps the input token for the output token effectively.
 And so that's, you know, one idea for you guys hacking this weekend.
 Yeah, maybe.
 Let's see if there are good questions here or at this point, let me just get through it.
 Yeah, and then I'll do the questions.
 We don't have that much time left, so I'm going to try and speed up.
 Okay.
 Things you can build.
 ENS is the type of thing that fits really nicely into existing projects, more so than a specific project on ens.
 The text record thing that I just described is an example of something that could be a conclusive ENS hackathon project.
 It's just like the brainchild of this payment preferences thing.
 But in most cases, it's like you're building an agent or you're building a wallet or a social app or anything like that.
 And ENS can be used to improve the user experience of that app.
 As I said before, ENS is a user experience protocol.
 So it is more used to improve existing apps than to build specific apps for yourself.
 It's like part of the journey, not necessarily just a destination.
 And yeah, so if you're building an AI, think about how you could give your agents usernames with ens, or if you're building a wallet, then make sure that every transaction history shows the ENS name that you're sending assets to.
 And in a social context maybe it's more obvious.
 Like all the profiles are ENS names and any sort of website can be deployed to ENS using the content hash record.
 So any app that you're building probably has a good way to be improved by ens.
 And that's kind of what I want to get you guys thinking about over here.
 And yeah, oh, I'm covering my slides again at a high level.
 It's like anywhere your app shows a hex address, it should instead show ENS names.
 And I know this might sound obvious, but I've talked to so many hackers who will be building for a whole weekend and then they come over on the last day and ask how ENs can be used and they'll just like show me the app and like, oh, hex address.
 We don't like those.
 You know, that could and should be a name and that will probably improve the user experience of your app.
 So literally just look at a demo of your own app and see where their hex address is and figure out IF and how ENs can be used to improve that.
 When I say has ENS names, that could mean either they have their own ETH name like GregSkrull ETH, or if they don't already have one, they being your user, you could issue one for them.
 And the easiest way to do that usually is a subdomain.
 So for example, I have projectname eth and I wanted to give a username to all of my users that don't already have an ENS name.
 And so then I would have Greg projectname Eth and there are many different ways to do this.
 I'm not going to explain all of the different options here, but a very popular one and people's hackers favorites because it's, you know, fun to play around with, is this project called Do Durin and Durin is basically an opinionated way to give subdomains on a layer two of your choice.
 And it's kind of a step by step process that has detailed information and is really a fun path to go down.
 So hopefully you got the chance to scan this QR code, otherwise it will be available later as well for issuing subdomains to your users primary names.
 I talked about it before, but I'm just going to give you a few seconds to scan a QR code if you want to read some more docs about it.
 Again, the ability to go from address to a name and what makes ENS this sort of this sort of portable web3 identity.
 And with all that, maybe the information was a little scattered, but hopefully I got enough of it out.
 Our prizes.
 So there are two prizes for ENS at this hackathon.
 The first is just a pool.
 Anybody that integrates ENS will be eligible to win part of a $3,500 pool prize.
 This could be as simple as implementing ENS resolution, which is, you know, sending assets to a name instead of an address.
 Any input field you have should support ens.
 Or if you have a list of transactions that you're showing some data, it should try and resolve those addresses into ENS names.
 It can be setting a decentralized website using Omnipin or any of the tools I described earlier.
 You could be issuing subdomains to your users.
 Really anything, as long as you write some code specifically for ENS.
 If you just use RNBokit and the Connect button, you know, the default thing shows your name.
 That's not quite enough for this, but you have to write some custom code just for ens.
 It could be using a few react hooks, but it has to be some effort to integrate ens.
 And then the bigger prize just for one team will be $1,500 for the most creative use of ENS in a DeFi application.
 I have a feeling this might be around those text records that I described earlier.
 I think payment preferences are really interesting and underexplored, and so it could be that it could be a similar version that Defi protocols could use as like a way to specify where you want your earned yield to go.
 So it could be defi, it could be payments, let's say most creative use of ENS.
 More broadly, DeFi is just like specific for this hackathon, but any super creative ideas that are loosely related to payments or defi or something like that are eligible.
 And if you have any questions, obviously you could ask.
 Cool.
 While I read through some questions, we have five minutes and I will leave this QR code up here to join our developer group.
 If you have any questions over the next few days, feel free to ask in there or in the discord.
 We will be monitoring both.
 And so yeah.
 Okay, let's go through some questions here on Zoom.
 Okay, I've scrolled back up.
 So yes, the Hacker pack is only available after project submission.
 This is the Jax question, but we can help you get one for the sake of the hackathon for free.
 No problem, just send a message in discord.
 And also I should mention that app ens.domains is where you may have Already been to register a name if you prepend Sepolia to that.
 So Sepia Sepolia app ENS domains.
 That brings you to the testnet version of the application which allows you to register names with Sepolia eth.
 So no real money needed.
 And that is totally fine for the sake of the hackathon.
 Okay, what if I want to provide sub names for my users and my users will be multi chain wondering how to set up the resolver in that case?
 Okay, so the probably shortest and easiest and maybe most helpful answer I could give is Durin is a great place to issue subdomains from L2S.
 By default, the implementation is that you do have to choose one so all of your names, for example, will live on base or Arbitrum or something like that.
 Although there's nothing stopping you from using this in combination with NFT bridges like I believe Layer zero or others that will potentially allow you to have the same functionality cross chain.
 There's probably some confusing bits there that are like underexplored and so I'm happy to know talk with you through it.
 But just to be clear, that is having a name, having a collection of names that is available on multiple chains at the same time is not a native ENS feature.
 And so that would be kind of a part of the hackathon project in itself.
 Awesome.
 Can it happen that someone registers the same ENS I did on mainnet on an EVML too?
 I register mat eth on mainnet.
 Can someone register the same on base?
 No.
 And this is actually related to the previous question in a way.
 The reason it's really hard to do cross chain naming is because you do need a single source of truth.
 A name collision where I have name ethon mainnet and somebody else has name ethonbase at the same time is kind of the worst case scenario for a global namespace.
 And so our architecture is that Ethereum L1 is the source of truth.
 And then you can kind of delegate certain parts of your name or subdomains to other chains, but generally, at least by default, an entire collection of names.
 And a collection, I'm saying, is kind of like a level of subdomains are all on the same chain for the sake of having a source of truth.
 So hopefully that answers your question.
 Matt, another question from Jack.
 If I lose my primary ETH wallet, is there a way to enforce the transfer of the name?
 I think is what I'm understanding from the question.
 So kind of there is a concept in ENS where you can have an owner of a name and a manager of a name.
 And in this case, the owner of a name should be a secure hardware wallet that, you know, doesn't get accessed often and is only for secure assets.
 And then the manager of a name is who can change the ETH address and the description and things like that more day to day.
 And that can be a how all where if it gets hacked, it's not a big deal because the owner can always like claw back the asset or the owner can always change the manager to be more precise.
 And so that is is my recommended setup for a name.
 Ultimately, if the owner of a ethname is a wallet that gets compromised, then the hacker could potentially steal that name from you.
 And once they do, there's.
 There's no way to get it back.
 No, yeah, it's an NFT and ENS has no sort of admin keys.
 So it is not possible for us to recover a name for you.
 A decentralized protocol on Ethereum.
 Okay, can smart wallets have ENS names?
 Yes, and it looks like a few people were getting involved in answering this for me, so thank you guys.
 This is great.
 Any address can have an ENS name.
 This includes EOAs, smart contracts, smart contract wallets, which are smart contracts and so on.
 So there's no restriction there.
 Yes.
 And as somebody pointed out, in order for a contract to receive a ETH name, it does have to be able to accept ERC721NFTs because ENS names are represented as NFTs.
 So that's a fairly common error that comes up.
 Developers will write a contract and try and transfer a name to it and there will be an error that is an NFT error, not necessarily an ENS specific name error.
 And yeah, there are certain types of ENS names that are ERC 721 or 1155.
 And so I don't think I have the time to explain that right now, but ask in Discord and happy to help.
 Or in DMs.
 Cool.
 I think we made it through.
 It only went a minute over, so hopefully that's all right.
 Pascal.

### Pascal
 Yeah, don't worry about it, Greg.

### Greg Skriloff
 Thank you.

### Pascal
 That was a fantastic, really, really informative workshop.
 As Greg pointed out, the team is available on obviously their developer Telegram channel, but also on our Discord channel or Discord server.
 Just send a message into the partner ENS channel and the team is more than happy to help.
 Jump in.
 Yeah, Greg, again, thanks for joining us.
 This was really, really cool.
 This entire thing is recorded and uploaded on YouTube so if you missed any parts throughout the workshop, missed any of the QR codes, you can always watch it there again and just scan the codes.

### Greg Skriloff
 Awesome.
 Thanks, everyone.
 No worries.

### Pascal
 Have a fantastic one.
 And we're excited to see what you're going to be building, hopefully on ens.
 Bye, everybody.

### Title
 ENS ️ Identity in Your Apps

### Host Email
 safia@ethglobal.com

### Organizer Email
 visheshdwivedi225544@gmail.com

### Calendar Id
 0uoe8dqf3pd5q3ptugnaui50bs

### Fireflies Users
 felipe.sarmiento.as@gmail.com, ayushsrivas55@gmail.com, singgihbrilian.tara06@gmail.com, charandeepkapoor3@gmail.com, gerardo.gerry.pedrizco@gmail.com, j.vivekvamsi@gmail.com, soniavgallego@gmail.com, lokeshwaran100@gmail.com, shikhar@iiitmanipur.ac.in, bashybaranaba@gmail.com, detroitmetalcrypto@gmail.com, quierochiachida@gmail.com, carlos@velascode.xyz, jsteerv@gmail.com, gmartinezgil@gmail.com, nishanthb.it2024@citchennai.net, stefanolombardo@posteo.de, kurodenjiro1@gmail.com, rahat@rahatcodes.com, yashj8858@gmail.com, laciferin@gmail.com, daryl.cl.lim@gmail.com, penrose@ultra.markets, arosejeremic5@gmail.com, weberfabian1@gmx.de, kulrajs.sabharwal.chy21@itbhu.ac.in

### Participants
 meek10x@gmail.com,visheshdwivedi225544@gmail.com,bashybaranaba@gmail.com,carlos@velascode.xyz,kulrajs.sabharwal.chy21@itbhu.ac.in,lokeshwaran100@gmail.com,nishanthb.it2024@citchennai.net,yashj8858@gmail.com,jsteerv@gmail.com,soniavgallego@gmail.com,arosejeremic5@gmail.com,felipe.sarmiento.as@gmail.com,penrose@ultra.markets,quierochiachida@gmail.com,laciferin@gmail.com,j.vivekvamsi@gmail.com,rahat@rahatcodes.com,stefanolombardo@posteo.de,kurodenjiro1@gmail.com,shikhar@iiitmanipur.ac.in,gerardo.gerry.pedrizco@gmail.com,detroitmetalcrypto@gmail.com,daryl.cl.lim@gmail.com,ayushsrivas55@gmail.com,charandeepkapoor3@gmail.com,singgihbrilian.tara06@gmail.com,weberfabian1@gmx.de,gmartinezgil@gmail.com, meek10x@gmail.com

### Date
 1770233400000

### Transcript Url
 https://app.fireflies.ai/view/01KGJ3614G11VA4QXSMGQN0MPC

### Audio Url
 No audio url

### Video Url
 No video url

### Duration
 30.989999771118164

### Meeting Attendees
 meek10x@gmail.com, c_d903dd814ba91df26e63faa49c99624e6d19557ed1ae0bcb0eb9d659e9fea453@group.calendar.google.com

### Cal Id
 0uoe8dqf3pd5q3ptugnaui50bs

### Calendar Type
 google

### Meeting Link
 https://ethglobal.zoom.us/j/81757822000
