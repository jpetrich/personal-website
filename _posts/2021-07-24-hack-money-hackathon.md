---
title: "Building Openhouse at the ETHGlobal HackMoney Hackathon"
published: true
---

I've been interested in cryptocurrency, and especially Ethereum, for a few
years, but never made the time to learn the technical side of it. I understood
the basics of smart contracts, and the differences between Bitcoin and Ethereum,
but, having followed the Ethereum ecosystem more closely for a few months, I
decided I wanted to dive deeper into Ethereum, smart contracts, and web3 tools.
I got permission from my company to participate, and signed up for the 2021
[ETHGlobal HackMoney hackathon](https://hackathon.money/)!

## Getting started

ETHGlobal has an interesting sign-up system for their hackathons. In addition to
an application (which seemed designed mainly to weed out bots and low-effort
submissions), upon approval, participants must "stake" a small amount of ETH.
This is done by logging into their site with an Ethereum wallet, and clicking on
a button which prompts you to authorize the transfer of the ETH to the
hackathon's address. Participants receive their stake back at the end of the
hackathon, as long as they complete required checkins and submit anything at the
end of it. This really appealed to me, despite losing the [gas
cost](https://ethereum.org/en/developers/docs/gas/), because it provided an
incentive to complete the hackathon and not bail out without finishing
something.

## Finding a team

After signing up, I was able to join the ETHGlobal Discord server, and verify
that I was a participant in the hackathon, again, using my Ethereum wallet.
There were channels for making introductions and finding teams. I joined without
knowing anyone else participating, and had planned on hacking solo unless I
could find a project that was really compelling and willing to take on someone
like me, with no Ethereum programming experience. I was surprised to find many
such teams! Some teams I talked to included the teams behind
[Pods](https://www.pods.finance/) and [PWN](https://pwn.finance/).

In my introduction, I mentioned my interest in building identity and
authorization solutions based on Ethereum wallets. While I found these, and
other DeFi projects, interesting, I am personally more interested in the future
of web3, where users control their digital identities completely by identifying
themselves with their private keys, and therefore have the ability to reset
their identities at any point by generating new keys. Projects like
[ENS](https://ens.domains/) that make it easy for users to associate
human-readable information with their private key really appeal to me, and I
think the future of the web will rely on systems like that. I hope that I will
one day be able to log in to pay my taxes or manage my healthcare with my keys
secured by my hardware wallet, that I will be able to engage with friends and
strangers on social media by logging in with a browser extension wallet, and
that I might have yet another wallet with a small amount of ETH, Bitcoin, or
stablecoins that replaces my leather wallet full of cards and cash today.

My introduction resonated with another participant, Chris, who had experience
with web3 livestreaming technology, and was interested in building web3
solutions to help facilitate online communities in a decentralized manner.
Through talking with him, we refined our ideas, and agreed to work together
after recruiting Drew, and, eventually, Prabhu, two more software engineers. By
the start of the hackathon we were ready to start building what we called
Openhouse, a video meeting platform with web3 login and access controlled
through
[ERC721](https://ethereum.org/en/developers/docs/standards/tokens/erc-721/)
tokens.

## Hacking away

This was my first experience participating in a virtual hackathon, and I wasn't
sure what to expect. I had participated in in-person hackathons before: 48 hour
endeavors with little time to sleep, let alone think! I found the pace of a 3
week hackathon much more enjoyable, and I appreciated the ability to work with
teammates across many timezones asynchronously. The pace gave me the opportunity
to study Solidity, SvelteKit (the JavaScript framework we used), Jitsi (the
open-source video conferencing software we used), and various other SDKs,
understand them, and make conscious architecture decisions that led to a much
more readable and improvable final product than we could have accomplished in a
48 hour sprint. I'm not sure yet whether we'll keep working on Openhouse after
the hackathon, but if we do, or anyone else wants to, our GitHub is in a good
state to pick up and keep on hacking.

## Final thoughts

Our submission for Openhouse is on the [ETHGlobal showcase
site](https://showcase.ethglobal.co/hackmoney2021/openhouse). At least for now,
you can also play with it at openhouse.joepetrich.com, where it's live on
Polygon. The code is on [GitHub](https://github.com/openhouse-project), and the
smart contract address on Polygon is
[0x151A051FE0a9414950Ef0B34030294cEaB6F043a](https://polygonscan.com/address/0x151a051fe0a9414950ef0b34030294ceab6f043a#code).

I learned a ton about web3 and Ethereum smart contracts in just thre weeks by
participating in this hackathon, and I'd encourage any web2 developers to give a
future ETHGlobla hackathon a try. By the end of the Hackathon, I had a better
understanding of multisig wallets, Solidity, ERC721 tokens, web3.js, and ENS.
The haze of terminology and only superficially understood technology that
clouded my understanding of web3 before has now been lifted, and I feel
confident to continue developing on top of Ethereum in the future.