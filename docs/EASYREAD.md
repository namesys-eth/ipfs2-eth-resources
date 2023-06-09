# IPFS2: Web3 IPFS Gateway

IPFS2 is a proof-of-concept IPFS gateway using an ENS CCIP Resolver wrapped in a **base32** decoder, capable of resolving IPFS and IPNS (and IPLD) contenthashes as subdomains of **.IPFS2.eth** when queried via a URL. **IPFS2.eth** is a dual implementation of CCIP-Read 'Off-chain Lookup', in which the Resolver contract is capable of fulfilling two queries simultaneously,

- to fetch the ENS contenthash as the parent domain's subdomain, and
- to fetch the RFC-8615 compliant ENS records stored at that contenthash, if requested.

Several centralised providers offer public gateways for IPFS/IPNS resolution such as https://dweb.link and https://ipfs.io. IPFS2 is a service similar to these public IPFS gateways but it uses an ENS CCIP Resolver and public ENS gateways (**eth.limo**, **eth.link** etc). IPFS2 uses **eth.limo** as its default CCIP gateway to read specific ENS records and is designed to fallback to secondary gateways.

## Design

IPFS2 architecture is as follows:

![](https://raw.githubusercontent.com/namesys-eth/ipfs2-eth-resources/main/graphics/ipfs2.png)

## Query Syntax

### Resolve **Contenthash**

Resolution of **<CIDv1-base32>.ipfs2.eth** will decode and resolve **<CIDv1-base32>** via CCIP as ABI-encoded contenthash. This functionality supports both IPNS and IPFS (and IPLD) contenthashes in **base32** format.

### Resolving ENS Records

IPFS2 Resolver also supports ENS-specific features such as querying ENS records associated with the (sub)domain. We use [RFC-8615](https://www.rfc-editor.org/rfc/rfc8615) **.well-known** directory format to implement this. The query syntax then reads:

```
https://<hash>.ipfs2.eth.*/.well-known/<data>.json
```

#### Some Examples

1. (Sub)domain's ENS avatar record is stored as **<CIDv1-base32>.ipfs2.eth.*/.well-known/avatar.json** in format

```
{
  "data": "0x_abi_encoded_avatar_string"
}
```

2. (Sub)domain's ETH address record is stored as **<CIDv1-base32>.ipfs2.eth.*/.well-known/addr-60.json** in format

```
{
  "data": "0x_abi_encoded_address"
}
```

#### JS Minimal Implementation

```
infura = new ethers.providers.InfuraProvider("goerli", SECRET_API_KEY);
// vitalik.eth's contenthash for testing: bafybeiftyo7xm6ktvsmijtwyzcqavotjybnmsiqfxx3fawxvpr666r6z64
const resolver = await infura.getResolver("bafybeiftyo7xm6ktvsmijtwyzcqavotjybnmsiqfxx3fawxvpr666r6z64.ipfs2.eth");
const contenthash = await resolver.getContentHash();
console.log(contenthash);
```

## Contracts

Goerli  : [`0xaa3d2c2811141ba4eb0ad0a369cb472151e49089`](https://goerli.etherscan.io/address/0xaa3d2c2811141ba4eb0ad0a369cb472151e49089#code)

Mainnet : [`0xb4BA47783Ff613ec55c9ECdaF38fCF29D7632048`](https://etherscan.io/address/0xb4BA47783Ff613ec55c9ECdaF38fCF29D7632048#code)

## Source Codes

IPFS2 CCIP contracts are available on [GitHub](https://github.com/namesys-eth/ipfs2-eth-resolver)

## How will we use the funds?

It'll likely cost close to 1 ETH to deploy the completed CCIP Resolver on Mainnet. Please consider supporting us!
