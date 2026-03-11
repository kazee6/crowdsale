# Core Functionality of the Contract – Explanation
* Initialization:
Upon deployment, the contract requires two parameters: the funding goal (in wei) and the duration (in seconds). The deployer is automatically set as the campaign organizer.
* Donations:
Users can donate by calling the fund() function and sending ETH, or by directly transferring ETH to the contract address. The receive() function will automatically trigger fund() in the latter case.
* Withdrawal:
If the campaign ends successfully (i.e., the funding goal is met), the organizer can call withdrawFunds() to withdraw all collected funds.
* Refund:
If the campaign ends without reaching the funding goal, each donor can call refund() to reclaim their individual contribution.
* Security Measures:
Critical parameters such as the organizer address and funding goal are declared as immutable, preventing any post-deployment modification.
ETH transfers use the call method instead of the outdated transfer/send, providing greater flexibility with gas limits and improved compatibility.
Custom modifiers enforce correct timing and access control, preventing unauthorized or premature function calls.

### Summary
This crowdfunding contract is written in Solidity 0.8.20 and is compatible with mainstream compiler versions. Its core features include donation, withdrawal, and refund mechanisms, along with fundamental security protections.
For development environments, beginners are recommended to use Remix (online IDE), while advanced developers may prefer Hardhat (local setup). Crucially, ensure the compiler version matches the pragma declaration in the contract.
Key Security Aspects:
Access control: Only the organizer can withdraw funds.
Time control: Withdrawals and refunds are only allowed after the campaign ends.
Replay protection: Donation records are reset appropriately to prevent double-refunds or other replay attacks.