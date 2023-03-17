# IPFS2: Web3 IPFS Gateway

IPFS2 is a proof-of-concept ENS Resolver capable of resolving IPFS/IPNS contenthash and records as subdomains of a parent name, and render associated ABI-encoded records when queried via a URL. Several centralised IPFS content providers offer IPFS/IPNS resolution of the form https://bafys0m3l0ngha5h0000000s3x.dweb.link → https://ipfs.io/ipfs/bafys0m3l0ngha5h0000000s3x (or similar). IPFS2 is a similar service with off-chain centralised resolvers replaced with on-chain resolvers. IPFS2 Resolver also supports additional features such as querying data records associated with the (ENS) contenthash in [RFC-8615](https://www.rfc-editor.org/rfc/rfc8615) compatible URL format.

## Query Syntax

To resolve **<data>** content stored at IPFS **<hash>**, i.e. https://ipfs.io/ipfs/bafys0m3l0ngha5h/.well-known/data.json, URL query is formatted as:

URL Syntax: https://**<hash>**.ipfs2.eth.**<gateway>**/.well-known/**<data>**.json

Example: https://bafys0m3l0ngha5h0000000s3x.ipfs2.eth.gate/.well-known/data.json

# Description

IPFS2.eth is a dual implementation of CCIP-Read 'Off-chain Lookup', in which the Resolver contract is capable of fulfilling two queries simultaneously,

- to fetch the ENS contenthash as the parent domain's subdomain, and
- to fetch the RFC-8615 compliant records stored at that contenthash, if requested.

IPFS2 currently supports **eth.LIMO**, **eth.CASA** and **eth.LINK** as ENS gateways and is designed to accept new gateways.

## Design

IPFS2 architecture is as follows:

![](https://raw.githubusercontent.com/namesys-eth/ipfs2-resources/main/graphics/ipfs2.png)

## Contracts

Testnet : [0x6418fc3db67e3c7a6aeafcb5a6416ccd6b75ef30](https://goerli.etherscan.io/address/0x6418fc3db67e3c7a6aeafcb5a6416ccd6b75ef30#code)

Mainnet : [Code audit in progress](https://github.com/namesys-eth/ipfs2-eth-resolver/blob/main/src/IPFS2.sol)

## Source Codes

IPFS2 CCIP contracts are available on [GitHub](https://github.com/namesys-eth/ipfs2-eth-resolver)
