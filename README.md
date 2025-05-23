
# 💸 sBTC-TipVerse

**sBTC-TipVerse Enhanced** is a decentralized tipping smart contract built on the Stacks blockchain. It enables users to send and receive tips in STX (and optionally BTC), track tipping statistics, earn reward points, and register verifiable usernames. Designed with scalability, transparency, and enhanced UX in mind, it provides an open platform for supporting creators, developers, and contributors.

---

## 📜 Features

* **Decentralized Tipping**: Users can send STX/BTC tips to others with automatic fee deduction.
* **Reward System**: Frequent tippers earn reward points if tipping exceeds the reward threshold.
* **Username Registry**: Users can register a verifiable username that links to their wallet address.
* **Detailed Stats**: Track total tips sent, received, and accumulated reward points.
* **Tip History Logging**: Transparent record of tipping activity.
* **Admin Controls**: Platform owner can adjust reward points manually (within limits).
* **Secure Validation**: Ensures valid transfers, token types, usernames, and permissions.

---

## 📦 Contract Constants

| Constant                  | Description                                           |
| ------------------------- | ----------------------------------------------------- |
| `CONTRACT_OWNER`          | Admin wallet authorized to make special updates       |
| `PLATFORM_FEE_PERCENTAGE` | Fee taken from each tip (default: 5%)                 |
| `MAX_TIP_AMOUNT`          | Maximum allowed per tip (1000 STX)                    |
| `REWARD_THRESHOLD`        | Minimum amount per tip to qualify for rewards (1 STX) |
| `REWARD_RATE`             | Points earned per qualifying tip (10 pts)             |
| `ALLOWED_TOKENS`          | Currently allowed: STX, BTC                           |
| `MAX_REWARD_RATE`         | Cap for manually updated reward rate                  |

---

## ⚠️ Error Codes

| Code  | Meaning                 |
| ----- | ----------------------- |
| `u1`  | Insufficient funds      |
| `u2`  | Invalid tip amount      |
| `u3`  | Transfer failed         |
| `u4`  | Failed to update reward |
| `u5`  | Invalid recipient       |
| `u6`  | Unauthorized action     |
| `u7`  | Invalid reward rate     |
| `u8`  | Invalid username        |
| `u9`  | Invalid username length |
| `u10` | Username already taken  |
| `u11` | Invalid token type      |
| `u12` | Invalid user            |

---

## 🛠️ Functions Overview

### Public Functions

* `tip(recipient, amount, token-type)`
  Tip another user using a valid token. Auto deducts platform fee and updates all stats.

* `update-user-reward-points(user, reward-rate)`
  Admin-only: manually updates a user's reward points.

* `set-user-identity(user, username)`
  User-only: register a verifiable and unique username.

### Read-Only Functions

* `get-user-tip-stats(user)`
  View total tips sent, received, and reward points.

* `get-user-identity(user)`
  Retrieve a user’s registered username.

* `get-total-tips-sent(sender)`
  View total tips sent by a user.

* `get-total-tips-received(recipient)`
  View total tips received by a user.

* `get-reward-points(sender, amount)`
  Simulate reward point update if user tips a specific amount.

* `get-tip-amount(amount)`
  Validate a tip amount.

* `get-updated-platform-stats(sender, amount)`
  Preview a sender's stats after a hypothetical tip.

* `get-tips-recieved(recipient, amount)`
  Calculate actual tip amount after fee deduction.

* `get-transaction-logs(sender, recipient, amount, fee, token-type)`
  Check log entry for a specific tip.

---

## ✅ Validation & Rules

* Users cannot tip themselves or the contract owner.
* Tip amount must be < 1000 STX and user must have sufficient balance.
* Only `STX` and `BTC` are accepted (for now).
* Usernames must be 3-20 characters and unique.
* Only contract owner can call `update-user-reward-points`.

---

## 🔐 Security Considerations

* All token transfers are wrapped in `try!` to avoid silent failures.
* All access control checks are enforced using `asserts!`.
* Invalid operations revert with descriptive error codes.

---

## 📈 Example Workflow

1. Alice sets her username via `set-user-identity`.
2. Bob sends 5 STX to Alice via `tip`, paying a 5% fee.
3. Bob earns 10 reward points since the tip exceeded 1 STX.
4. The contract logs this transaction, and both users' stats are updated.

---

## 🧪 Testing Tips

* Try tipping with 0.5 STX and 2 STX to test reward logic.
* Register usernames and ensure uniqueness constraints are enforced.
* Simulate reward point updates with the read-only functions before calling public ones.

---
