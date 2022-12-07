---
title: Governance guide for developer
subtitle: Learn how to propose a change through governance, council and technical committee on the Turing Network
author: christian
tags: [governance]
---

## Introduction

We can referenda `normal proposals` and `external proposals`.

Normal proposals require endorsers (some people stake tokens to support) to decide which proposals can be voted on in the next round of referendums.

![proposals](../../assets/img/governance-guide-for-developer/proposals.png)

**Usually, Only one proposal will be voted on per round of referenda.**

The council can propose an external proposal, Then this external will have priority in the next round of referendums.

![external-proposal](../../assets/img/governance-guide-for-developer/external-proposal.png)

There may be more than two referendas if the technical committee uses the "Fast track" to urgently process an `external proposal`.

![fast-track-referenda](../../assets/img/governance-guide-for-developer/fast-track-referenda.png)

## How to upgrade runtime through governance?

Take the external proposal as an example.

**1\. Compile the new version of the compressed wasm file**

It usually ends with `.compact.compressed.wasm`.

**2\. Submit a preimage**

Preimage is the content of a proposal that contains all the parameters of an extrinsic.

Anyone can submit the preimage.

![submit-preimage](../../assets/img/governance-guide-for-developer/submit-preimage.png)

![preimage-submission-form](../../assets/img/governance-guide-for-developer/preimage-submission-form.png)

Be sure to record the `preimage hash` before submitting.

**3\. Submit an external proposal**

Use the council member's account to submit an external proposal. 

![propose-external](../../assets/img/governance-guide-for-developer/propose-external.png)

![external-proposal-submission-form](../../assets/img/governance-guide-for-developer/external-proposal-submission-form.png)

Council members can vote on it. If the threshold is reached before the voting period ends, after clicking close button, the proposal will be moved to a external proposal list in democracy page.

![close-external-proposal](../../assets/img/governance-guide-for-developer/close-external-proposal.png)

![become-propose-external](../../assets/img/governance-guide-for-developer/become-propose-external.png)

We need to wait for the start of a new round of referenda, this proposal will go to referendum.

`LaunchPeriod` is in the upper right corner of the image. It is the duration of each round of referenda, it is `7` days in Turing.

**4\. Vote for proposal**

Users can vote during the voting period after the new round of referenda begins. `VotingPeriod` is `7` days in Turing.

![referenda](../../assets/img/governance-guide-for-developer/referenda.png)

After `VotingPeriod`, if the proposal wins the referendum, it will wait for the delay defined by `EnactmentPeriod` to execute. `EnactmentPeriod` is `8` days in Turing.

![dispatch-proposal](../../assets/img/governance-guide-for-developer/dispatch-proposal.png)

**5\. Fast track**

When an urgent upgrade or configuration is required, the technical committee can use the "Fast track" to make the external proposal submitted by the council immediately go to a short referendum, and can set a short delay time for scheduled execution time.

![fast-track-external-proposal](../../assets/img/governance-guide-for-developer/fast-track-external-proposal.png)

As shown in the figure below, a member of the technical committee submitted a Fast track proposal, setting the `voting period` to 20 blocks. When the voting is over, the proposal is executed after a delay of 1 block.

`voting period` must be greater than or equal to `FastTrackVotingPeriod` configured by pallet_democracy. `FastTrackVotingPeriod` is `3` hours in Turing.

![fast-track-proposal-submission-form](../../assets/img/governance-guide-for-developer/fast-track-proposal-submission-form.png)

When the threshold is reached, click close to move the proposal to referenda.

![close-fast-track-proposal](../../assets/img/governance-guide-for-developer/close-fast-track-proposal.png)

## How to do a configuration call through governance?

Similar steps as above：

1\. Submit a preimage. 

2\. Submit a normal proposal or external proposal.

3\. If the external proposal needs urgent processing, the technical committee can use the "fast track" to process it.

4\. conduct a referendum.

5\. When the voting period ends, the vote will be executed at the end of the enactment period.

![do-a-configuration](../../assets/img/governance-guide-for-developer/configuration-proposal.png)

## How to grant a third party using treasury funds?

We need to submit a proposal on the Treasury interface first, and then council members can vote on the council.

The Treasury's proposal can be approved by the council and does not need to be voted on by a referendum.

![treasury-proposal](../../assets/img/governance-guide-for-developer/treasury-proposal.png)

![submit-treasury-proposal](../../assets/img/governance-guide-for-developer/submit-treasury-proposal.png)

![vote-treasury-proposal](../../assets/img/governance-guide-for-developer/vote-treasury-proposal.png)

![treasury-proposal-approved](../../assets/img/governance-guide-for-developer/treasury-proposal-approved.png)

Treasury proposal is a way to allocate treasury funds within Council, and there are other ways: Tips, Bounties.

Tips allows anyone to submit a tip proposal, and Council members suggest how much to distribute.

Bounties is to carry out a job and entrust an agent to allocate funds according to the progress of the job completion.

## The outcome of the referendum

There are 3 ways to win or lose a referendum:

**1. Public Referenda**

The condition for winning the referendum:

![public-referenda](../../assets/img/governance-guide-for-developer/public-referenda.png)

```
approve - the number of aye votes

against - the number of nay votes

turnout - the total number of voting tokens (does not include conviction)

electorate - the total number of tokens issued in the network
```

A heavy super-majority of aye votes is required to carry at low turnouts

**2. Unanimous Council Referenda**

When **all members of the council agree on a proposal**, it can be moved to a referendum. 

The condition for winning the referendum:

![image](../../assets/img/governance-guide-for-developer/unanimous-council-referenda.png)

when the turnout rate is low, a super-majority is required to reject the proposal, which means a lower threshold of "aye" votes have to be reached

**3. Majority Council Referend**

When **agreement from only a simple majority of council members** occurs, the referendum can also be voted upon.

The condition for winning the referendum:

![image](../../assets/img/governance-guide-for-developer/majority-council-referenda.png)

## Votes of referendum

Polkadot utilizes an idea called Voluntary Locking that allows token holders to increase their voting power by declaring how long they are willing to lock up their tokens, hence, the number of votes for each token holder will be calculated by the following formula:

```
votes = tokens * conviction_multiplier
```

The conviction multiplier increases the vote multiplier by one every time the number of lock periods double.

| Lock Periods | Vote Multiplier |
| ---- | ---- |
| 0 | 1 |
| 1 | 1 |
| 2 | 2 |
| 4 | 3 |
| 8 | 4 |
| 16 | 5 |
| 32 | 6 |

Only the winning voter's tokens are locked.

## References

**Questions like how to count votes are very important and there are many ways to count votes, so please read the official article carefully.**

Governance

[https://wiki.polkadot.network/docs/learn-governance](https://wiki.polkadot.network/docs/learn-governance)

Treasury

[https://wiki.polkadot.network/docs/learn-treasury](https://wiki.polkadot.network/docs/learn-treasury)