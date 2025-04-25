# 🔍 Audit Report – ModifierPractice.sol

**Auditor:** Hasan  
**Date:** [Insert Today’s Date]

---

## 🔐 Summary

| Severity | Count |
|----------|-------|
| High     | 1  
| Medium   | 1  
| Low      | 2  
| Informational | 1  

---

## 🟥 High Severity

### 1. Repeated Withdrawals Allowed via `reset()`

**Description:**  
The owner can reset a user's withdrawal status at any time. This enables authorized users to withdraw repeatedly if the owner keeps resetting.

**Impact:**  
Could lead to unintended abuse if not properly managed.

**Recommendation:**  
Add logging, access restrictions, or withdrawal cooldown logic to prevent misuse.

---

## 🟧 Medium Severity

### 2. Missing Event in `authorizeUser()`

**Description:**  
There's no event log when a user is authorized.

**Impact:**  
Lack of traceability in off-chain systems or audits.

**Recommendation:**  
Emit `event UserAuthorized(address user)` inside the function.

---

## 🟨 Low Severity

### 3. No Address Validation in `authorizeUser()`

**Description:**  
The function does not validate input.

**Impact:**  
The zero address could be authorized unintentionally.

**Recommendation:**  
Add: `require(_user != address(0), "Invalid address");`

---

### 4. No Logging in `withdraw()`

**Impact:**  
Difficult to trace when or how much a user withdraws.

**Recommendation:**  
Emit `event Withdraw(address user, uint amount);`

---

## 🟦 Informational

### 5. Function Naming Suggestion

**Description:**  
Consider renaming `reset()` to `resetWithdrawal()` for clarity and intent.

---

## ✅ Conclusion

The contract implements clear access control but would benefit from logging, validation, and improved traceability. A good foundation for security-aware development.
