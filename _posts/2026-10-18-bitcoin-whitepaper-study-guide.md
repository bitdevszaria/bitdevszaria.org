---
layout: post
type: whitepaper
title: "Bitcoin Whitepaper Reading: 30 Study & Discussion Questions"
date: 2026-10-18
---

To kick off our technical study sessions ahead of our monthly Socratic Seminars, the BitDevs Zaria community held a chapter-by-chapter reading circle on Satoshi Nakamoto's 2008 foundational paper: [Bitcoin: A Peer-to-Peer Electronic Cash System](https://bitcoin.org/bitcoin.pdf).

Below is our comprehensive 30-question discussion guide. Each section includes first-principles questions and core technical takeaways used during our group discussion.

---

### Abstract

**1. What does Satoshi identify as the main weakness when using digital signatures alone for electronic cash?**
- *Discussion*: Digital signatures prove authorization and chain of custody, but cannot prevent double-spending without a trusted third party. If a central authority is still needed to stop double-spends, the primary benefit of peer-to-peer cash is lost.

**2. According to the Abstract, what does the "longest chain" prove to all participants in the network?**
- *Discussion*: The longest chain proves two things: first, the chronological sequence of transactions witnessed by the network; second, that it originated from the largest pool of CPU/hash power.

---

### 1. Introduction

**3. Why does the trust-based banking model make completely non-reversible transactions impossible?**
- *Discussion*: Intermediaries cannot avoid mediating disputes and processing chargebacks. Because reversals are always a possibility, trust must spread across all parties, forcing merchants to collect sensitive customer identity data.

**4. How does the cost of mediation by banks affect small, casual transactions on the internet?**
- *Discussion*: Handling disputes and fraud requires overhead costs, which leads to flat transaction fees and percentage cuts. This overhead cuts off small casual payments and micro-transactions.

**5. When you pay someone with physical cash in person, there is no double-spending. Why does that guarantee disappear when you try to pay someone over an internet communications channel?**
- *Discussion*: Physical bills are matter that cannot exist in two places at once. Digital data is information that can be copied infinitely with zero cost, requiring an unforgeable timestamped sequence to determine which spend happened first.

---

### 2. Transactions

**6. Satoshi defines an electronic coin as a "chain of digital signatures." Walk us through how one owner transfers a coin to the next owner under this definition.**
- *Discussion*: The owner signs a hash of the previous transaction and the public key of the next owner, adding this signature to the end of the coin. The payee can verify signatures to trace ownership back to the origin.

**7. Why can a payee not simply look at a signed coin and be certain that they actually received valid funds?**
- *Discussion*: The signature proves the payer owned the coin, but does not prove whether that same coin was already signed over to someone else earlier.

**8. In the traditional mint model, how did the central mint stop double-spending, and what fatal flaw did Satoshi point out with that approach?**
- *Discussion*: Transactions had to be returned to the mint to be cancelled and reissued. The fatal flaw is central control: the entire monetary system depends on the entity running the mint.

---

### 3. Timestamp Server

**9. What does a cryptographic timestamp server prove about a piece of data?**
- *Discussion*: It proves that the data existed at that point in time, because computing the hash is impossible without having the data.

**10. Why does each timestamp hash include the previous timestamp inside it, and what historical example did Satoshi cite for publishing hashes widely?**
- *Discussion*: Including the previous hash creates a tamper-evident chain where each new block reinforces all previous blocks. Satoshi cites Stuart Haber and Scott Stornetta's work, who famously published root hashes in public newspapers (such as *The New York Times*).

---

### 4. Proof-of-Work

**11. What mathematical property of cryptographic hashing (like SHA-256) makes proof-of-work work so well for distributed consensus?**
- *Discussion*: Computational asymmetry. Finding a valid nonce that produces a hash beginning with a required number of zero bits requires brute-force guessing (exponential work), but verifying that a solved hash meets the difficulty target takes a single hash calculation (instant).

**12. Why did Satoshi choose "one-CPU-one-vote" instead of "one-IP-address-one-vote" for majority decision making?**
- *Discussion*: IP addresses are trivial to acquire, spoof, or allocate in large quantities (Sybil attack). Proof-of-work anchors consensus to real, scarce physical energy and hardware.

**13. Why does Bitcoin need a moving average difficulty adjustment? What would happen if difficulty was permanently fixed and mining hardware became 1,000 times faster?**
- *Discussion*: Difficulty dynamically retargets to maintain an average block interval of roughly 10 minutes. Without adjustments, faster hardware would produce blocks in seconds, causing network fragmentation, extreme chain reorganizations, and hyperinflation of the coin supply.

---

### 5. Network

**14. In Section 5, step 5 says nodes accept a block only if all transactions in it are valid and not already spent. What does this tell us about the relationship between miners and validating nodes?**
- *Discussion*: Miners cannot alter protocol rules or force invalid transactions on the network. Even if a miner invests massive compute to find a valid proof-of-work hash, full nodes reject the block if even a single transaction is invalid.

**15. If two miners discover two different valid blocks at the exact same moment, how does the network handle this temporary split without a central coordinator?**
- *Discussion*: Nodes work on whichever valid block they received first, keeping the alternate block saved as a branch. The tie is broken when the next block is found on one branch, making it longer; nodes then switch to the longer chain.

**16. Why does Bitcoin's peer-to-peer network not require messages to be delivered reliably to every single computer on Earth?**
- *Discussion*: Bitcoin relies on best-effort broadcast. If a node misses a block due to dropped connections, it recognizes the gap upon receiving the subsequent block and requests the missing piece from peers.

---

### 6. Incentive

**17. What are the two distinct components that make up a miner's incentive in Bitcoin?**
- *Discussion*: First, the block subsidy (newly minted coins in the coinbase transaction). Second, transaction fees (the difference between transaction input values and output values).

**18. Why was the block subsidy necessary to distribute coins into circulation at the start of Bitcoin?**
- *Discussion*: There was no central issuer, company, or foundation to distribute coins. The continuous addition of new coins mimics gold mining, directly rewarding the participants expending resources to secure the network.

**19. Satoshi argues that an attacker who gathers more than 50% of the world's CPU power faces an economic dilemma. Why might this attacker choose to follow the rules rather than attack the network?**
- *Discussion*: Attacking the network by double-spending undermines confidence in the currency and destroys the market value of the attacker's own coins and hardware. Playing by the rules and earning the majority of block rewards is economically more profitable.

---

### 7. Reclaiming Disk Space

**20. How does a Merkle tree allow a Bitcoin full node to prune spent transactions from disk without altering or invalidating the block hash?**
- *Discussion*: Transactions are hashed into a Merkle tree, and only the Merkle root is committed into the block header. When outputs are fully spent, old transaction data can be pruned while preserving intermediate hashes to compute the root.

**21. Satoshi calculates that an 80-byte block header generated every 10 minutes amounts to roughly 4.2 MB per year. Why was this calculation critical for Bitcoin's feasibility?**
- *Discussion*: It showed that even if transaction history grows large, the cryptographic spine of the network (the block headers) easily fits entirely in RAM on everyday personal computers.

---

### 8. Simplified Payment Verification (SPV)

**22. What specific pieces of data does an SPV light wallet need to download from the network to verify that a payment was received?**
- *Discussion*: The wallet only needs to download the 80-byte block headers of the longest proof-of-work chain, along with the Merkle branch linking the specific transaction to the block's Merkle root.

**23. Why is an SPV client vulnerable if an attacker temporarily overpowers the network, and what defense mechanism did Satoshi propose for this?**
- *Discussion*: Light clients do not validate full consensus rules, only proof-of-work inclusion. An attacker with majority hashpower could mine an invalid block. Satoshi proposed network fraud alerts, where full nodes broadcast alerts upon spotting invalid blocks, prompting SPV wallets to download full blocks and verify them.

---

### 9. Combining and Splitting Value

**24. In a standard Bitcoin transaction, what are the inputs, and what are the two common outputs created?**
- *Discussion*: Inputs are unspent transaction outputs (UTXOs) from previous transactions. Outputs typically consist of one payment to the recipient and one change output returned to the sender.

**25. What happens to any leftover value if the sum of a transaction's inputs is larger than the sum of its outputs?**
- *Discussion*: The remaining difference automatically becomes the transaction fee, which is collected by the miner who mines that block.

---

### 10. Privacy

**26. How does Bitcoin's privacy model differ fundamentally from traditional banking privacy?**
- *Discussion*: Banks provide privacy by concealing all records behind institutional walls. Bitcoin makes transaction values and timings public, but maintains privacy by keeping public keys pseudonymous.

**27. What is the privacy risk of multi-input transactions, and what best practice did Satoshi recommend to maintain a firewall between transactions?**
- *Discussion*: Multi-input transactions reveal that the combined inputs are controlled by the same owner (common-input ownership heuristic). Satoshi advised generating a brand new key pair for every transaction to avoid linkage.

---

### 11. Calculations

**28. If an attacker successfully generates an alternate chain faster than the honest network, can they rewrite history arbitrarily, take coins that never belonged to them, or print infinite money? Why or why not?**
- *Discussion*: No. Attackers cannot forge digital signatures or alter validity rules. Honest nodes reject invalid blocks automatically. An attacker's power is strictly limited to attempting to double-spend transactions they personally made.

**29. Satoshi models the race between honest miners and an attacker as a Gambler's Ruin problem. Why does waiting for more block confirmations (z) cause the attacker's chance of catching up to plummet exponentially?**
- *Discussion*: Because honest miners control the majority of hashpower (p > q), their chain has positive drift. Each additional confirmation increases the honest lead, making the probability of a slower attacker catching up drop exponentially.

---

### 12. Conclusion

**30. In the final paragraph of the whitepaper, Satoshi states: "Nodes vote with their CPU power, expressing their acceptance of valid blocks by working on extending them and rejecting invalid blocks by refusing to work on them." What does this tell us about how consensus and rules are maintained in Bitcoin without a leader or central board?**
- *Discussion*: Bitcoin consensus is emergent. Nodes independently validate all rules against their local software. If any entity proposes an invalid block, other participants reject it and refuse to extend it, making consensus an ongoing, decentralized coordination game.

---

*BitDevs Zaria meets every last Saturday of the month in Zaria, Kaduna State, Nigeria. Socratic Seminars follow the Chatham House Rule.*
