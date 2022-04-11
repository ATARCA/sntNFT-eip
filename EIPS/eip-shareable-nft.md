---
eip: to-be-numberd
title: Shareable non-transferable non-fungible token standard
description: A standard interface for shareable non-transferable NFTs
author: ATARCA team
discussions-to: https://ethereum-magicians.org/t/shareable-non-transferrable-non-fungible-token-sntnft/8351
status: Draft
type: Standards Track
category: ERC
created: 2022-01-28
requires: 165
---

## Abstract

The following defines a standard interface for shareable non-transferable non-fungible tokens. The standard allows creation of tokens that can hold value, but cannot be exchanged for rival goods such as money, cryptocurrencies or other goods that hold monetary value. Minted tokens can be shared, or in this case re-minted, by their owners to new recipients to denote sharing of the token. The sharing and its associated events allow construction of a graph showing whom has shared what to which party.

## Motivation

Traditional NFT standards such as ERC-721 and ERC-1155 have been developed to introduce artificial digital scarcity and to capture rival value. NFT standards and implementations don't necessarily have to be exhibit scarcity and in certain use cases such as in ATARCA project we wish to avoid introduction of deliberate scarcity. 

In ATARCA project we attempt to capture positive externalities in ecosystems with new types of incentive mechanisms that exhibit anti-rival logic, serve as an unit of accounting and function as medium of sharing. 

These requirements have set us to define shareable non-transferable NFTs. These shareable NFTs can be “shared” in the same way digital goods can be shared, at an almost zero technical transaction cost. They are used to instantiate quantified anti-rival value, a medium of sharing. Hence, they work somewhat as money, being a store of value and a unit of account, but instead of being a medium of exchange, they are a medium of sharing.

Typical NFT standards such as ERC-721 and ERC-1155 do not define a sharing modality. Instead ERC standards define user interfaces for typical rival use cases such as token minting and token transactions that the NFT contract implementations should fulfil. The ‘standard’ contract implementations may extend the functionalities beyond the definition of interfaces. The tokens developed in the ATARCA experiments are designed to be token standard compatible at the interface level. However the implementation of token contracts may contain extended functionalities to match the requirements of the experiments such as the requirement of 'shareability'. In reflection to standard token definitions, shareability of a token could be thought of as re-mintability of an existing token. Contracts define re-mintable non-transferable tokens which retain some reference to previous tokens upon and after re-minting.

## Specification

The key words “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY”, and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

```solidity
import "@openzeppelin/contracts/utils/introspection/IERC165.sol";
import "@openzeppelin/contracts/token/ERC721/IERC721.sol";

interface IERCsntNFT is IERC165 {

  /// @dev This emits when a token is shared, reminted and given to another wallet that isn't function caller
  event Share(address indexed from, address indexed to, uint256 indexed tokenId, uint256 derivedFromtokenId);

  /// @dev Shares, remints an existing token, gives a newly minted token a fresh token id, keeps original token at function callers possession and transfers newly minted token to receiver which should be another address than function caller. 
  function share(address to, uint256 tokenIdToBeShared, uint256 newTokenId) external virtual;

} 
```

## Rationale

- our design choices, why did we pick up ERC-721, thinking behind why are we suggesting specific technical design choises

## Backwards Compatibility

## Reference Implementation

## Security Considerations

## Copyright

Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
