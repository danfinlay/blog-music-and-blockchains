# Blockchains and the Music Industry

I just spent a solid week at SXSW talking to people of all sorts of perspectives within the music industry about how the blockchain could be beneficial to them.

The fundamental ways that kept coming up were similar to just about every other industry, but with a few specific features needing emphasis to encourage initial adoption by the incumbent players.

In this article, I'm going to start by discussing the existing revenue models of the recording industry and how they could be augmented by blockchain technologies.

I'm then going to build on those basic tools to demonstrate how powerful they actually are. By the end, I hope to leave you with a couple way-out possible futures, and hopefully a strong enough understanding that you can imagine your own, and contribute to the conversation as it's happening right now.

## First, A Note on DRM

When talking about publishing intellectual property rights on a blockchain, people inevitably get caught in a specific intellectual eddie that is rooted in the last hundred years of how the industry has operated.

Inevitably someone will say:

> Yeah, but how do you control who can hear it?

The blockchain does not answer that question, and it does not have an opinion on it. Information has a tendency to be freed upon sharing. You can't unlearn that the world is round, and sometimes you can't even voluntarily get a song out of your head.

Computers are no different. Either they receive the information or they don't. If they play the music through the speakers, another could easily capture the sound with a microphone.

The perfect implementation of DRM merely inconveniences piracy, making encouraged channels more appealing.

The solutions I'll discuss do not solve DRM, but they do simplify the process of creating a fair economy for music payments that listeners can feel good about, artists can be compensated for, along with everyone else providing valuable services along the way.

## The Recording Industry

Right now, the recording industry and its rights collection arms are very complicated.

In particular, the Performance Rights Organizations (PRO) are tasked with the huge burden of collecting rights payments internationally, and dividing those payments fairly among the content creators, publishers, distributors, etc.

These organizations naturally run into a wide variety of obstacles that come from managing such a huge network of connections, spread across six different companies.

You've got database inconsistencies, accounting errors, issues finding rights holders, and sometimes [legal might gone awry](http://www.nytimes.com/1996/12/17/nyregion/ascap-asks-royalties-from-girl-scouts-and-regrets-it.html?pagewanted=all).

Many of these problems would be solved with a shared database that made it easy to verify who published a work first. This just happens to nicely describe a basic blockchain.

### A Registry of Property

The simplest version of an intellectual property registry written for the Ethereum blockchain would just give a person a way to register a song's hash, or fingerprint, with their identity, and the ability to verify they posted it first.

To prove how simple that is, [I implemented it in 13 lines of Solidity](https://github.com/flyswatter/ip-registry/blob/master/contracts/IpRegistry.sol). If taken to court, a blockchain registration like this should hold up as "prior art", proving a point in time the artist had the work in hand.

Of course, this does not prevent someone from re-formatting a song and registering it with a different hash, and here I see an opportunity for a legal service industry to emerge, or maybe a new purpose for an old one.

### PRO as Publication Authority

In public-key encryption, you always know some data was sent to you and from a specific source, as long as you know you have their public key. To get these public keys, you get their key encrypted to you by a [Certificate Authority](https://en.wikipedia.org/wiki/Certificate_authority), whose own public key came pre-installed with your browser..

The Certificate Authority (CA) is an intermediary service that helps verify a particular certificate, and I think in a blockchain-based registry, one fundamental service PRO-type organizations could provide would be forming themselves into a sort of **Publication Authority**, where they certify a particular song's registration, or even artist's public key as valid.

While anyone could still publish music, a small public consumer of music like a coffee shop might still prefer to play music that had been verified by a publication authority of some sort.

### Legal Representation Market

In addition to verifying artist identities or track validities, the task of identifying invalid tracks or public performances would remain an open challenge.

For artists publishing under a PRO, the PRO would remain responsible for the enforcement of those contracts, but for artists lacking representation, a public registry would create a space where freelance legal teams could search for illegitimate registrations of existing works, perhaps using sonic analysis to look for re-formatted duplicates, allowing independent artists to be represented by whoever is the most dilligent at defending their rights.

Additionally, this kind of analysis could be run on radio stations or in public places, and so artists' rights could be protected on a completely freelance basis. If the song's contract included a specified cut for legal protectors, any random fan in a coffee shop could help ensure their favorite band was being fairly compensated.

### Communicating Rights and Terms

Once you have an ecosystem for verifying the veracity of a published work's registration and payment, you have a verified public place to communicate terms and conditions of the linked work.

The simplest version of attached terms and conditions would be that each registered work includes a link to its ownership terms and conditions, which could be cryptographically verified, *which would be a big step forward*.

[Benji Rogers's Dot Blockchain project](http://www.dotblockchain.info/) aims to create a public data standard for a music file to declare its rights and permissions alongside the music file itself. Without a central registry that is universally trusted, this could make it easy for someone posting music to express how to look up their terms.

If we were able to format common terms in a consistent enough way that they were machine readable, we could have fair-trade music playing software that automatically pays for content under a user-defined threshhold.

Terms could even include pay-what-you-want clauses, or different fees for different uses.

The way I see it, a simple license file would be a collection of different conditions, each of which include the terms:

 - What the allowed use is
 - What protocol to pay via
 - The correct recipient address for this protocol
 - The amount to pay

This simple structure does not account for scaling type licenses (What happens when half the people leave the bar? Can the bar pay less now?), but this is the kind of thing that could be solved with a good public standard. Maybe `dot-blockchain` could support a simple scripting language, or could point to public functions on a blockchain to compute royalties.

All of those complexities could be left to user-space to start, as long as the license file linked to a format that some players knew how to read.

### Royalty Distribution on the Blockchain

So far we've seen how we could publish music, protect our rights, and communicate terms and conditions on the blockchain. Next we will see how the blockchain can distribute royalties.

The [Ujo Music](http://ujomusic.com/) project demonstrates how easily payment distribution can happen when the payment rights are built into the protocol via a blockchain "smart-contract". On every purchase, the song's contract automatically divides the payment according to virtual "shares" that the contract defines.

The [Monegraph](https://monegraph.com) project seems to have similar aims, and is highlighted in [the dot-blockchain paper](https://medium.com/cuepoint/how-the-blockchain-can-change-the-music-industry-part-2-c1fa3bdfa848#.hup3z6xl1).

If a smart-contract is used as the payment dividing mechanism, the payments are divided automatically when the smart-contract's method is called.

The easiest way to adopt these benefits early on is to provide normal payment methods to a user, and use the blockchain to distribute royalties on the backend.

There could also be music players that allow the listener to log in directly with a blockchain account, allowing direct payments to artists.

In addition to providing a user interface, the `.bc`i protocol also needs to include a way to define exactly what method on the smart contract to call, depending on the license required.

On the Ethereum blockchain, this would probably involve including an [Application Binary Interface, or ABI](https://github.com/ethereum/wiki/wiki/Ethereum-Contract-ABI) for the contract, to specify the addresses of individual methods, as well as which method to call, etc.

For an initial proof of concept of the `.bc` format, I would encourage the community to form a minimum useful format to declare accounts/functions on different protocols as the recipients of a music payment.

Simple ledgers like Bitcoin would be the simplest, essentially being an address to deposit to, but on blockchains with the ability to auto-disperse royalties, a machine-readable protocol will be required.

There's currently a discussion around what features the `.bc` file format should have, and all music stake holders should take a moment to consider the features they would like in such a format.

I'm excited to see the discussion become a bit more technical, as the current public survey is a fairly high-level list of desired attributes, and I hope to start engaging in those discussions much more soon.

If implemented correctly, the .bc` file format should provide enough value that PROs benefit from adopting it themselves (by unifying their databases and simplifying coordination), while also allowing anyone to publish to the format, and ideally leaving the format extensible enough that payment distribution can eventually be automated in compliant music-players, at the protocol level.
























