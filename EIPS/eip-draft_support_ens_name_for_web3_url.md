---
eip: draft_support_ens_name_for_web3_url
title: Support ENS Name for Web3 URL
description: A mapping from an ENS name to the contract address in Web3 URL
author: Qi Zhou (@qizhou), Qiang Zhu (@qzhodl)
discussions-to: https://ethereum-magicians.org/t/eip-6821-support-ens-name-for-web3-url/13654
status: Draft
type: Standards Track
category: ERC
created: 2023-04-02
requires: 137, 4804
---

## Abstract

This standard defines the mapping from an name of an Ethereum name service (ENS) to an Ethereum address for [ERC-4804](./eip-4804.md).

## Motivation

ERC-4804 defines a `web3://`-scheme RFC 2396 URI to call a smart contract either by its address or a **name** from name service.  If a **name** is specified, the standard specifies a way to resolve the contract address from the name.

## Specification

Given **contractName** and **chainid** from a `web3://` URI defined by ERC-4804, the protocol will find the address of the contract using the following steps:

1. Find the `web3` text record on ENS resolver on chain **chainid**.  Return error if the chain does not have ENS or the record is an invalid ETH address.
2. If the `web3` text record does not exist, the protocol will use ETH address of **name**.

Note that `web3` text record may return an Ethereum address or an [ERC-3770](./eip-3770.md) chain-specific address.  If the address is an ERC-3770 chain-specific address, then the chainid to call the message will be overridden by the chainid specified by the ERC-3770 address.

## Rationale

The standard uses `web3` text record with ERC-3770 chain-specific address instead of contenthash so that the record is human-readable - a design principle of ERC-4804.  Further, we can use the text record to add additional fields such as time to live (TTL).

## Security Considerations

No security considerations were found.

## Copyright

Copyright and related rights waived via [CC0](../LICENSE.md).
