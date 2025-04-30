# 🛡️ Smart Contract Audit Report – FundTracker.sol

## 🔎 Summary

- **Contract Name**: FundTracker
- **Lines of Code**: ~50
- **Audit Type**: Manual Static Review
- **Date**: 2024-04-30
- **Author**: Hasan
- **Repository**: [solidity-projects](https://github.com/hasan-23/solidity-projects/blob/main/contracts/FundTracker.sol)

---

## ✅ Audit Findings Summary

| Severity | Count |
|----------|-------|
| Critical | 0 |
| High     | 0 |
| Medium   | 0 |
| Low      | 1 |
| Gas      | 1 |
| Info     | 2 |

---

## 🧠 Detailed Findings

### [F1] `deposit()` accepts zero ETH  
- **Severity**: Low  
- **Location**: Line 17  
- **Description**: The function allows deposits of 0 ETH, which can clutter logs or mislead analytics.  
- **Recommendation**: Add a check like `if (msg.value == 0) revert InvalidDeposit();`.

---

### [F2] Gas inefficiency in owner check  
- **Severity**: Gas  
- **Location**: Line 23  
- **Description**: The `owner` is read from storage multiple times inside `withdraw()`, slightly increasing gas usage.  
- **Recommendation**: Cache `owner` in a local variable before comparison and transfer.

---

### [F3] No ownership event  
- **Severity**: Info  
- **Description**: There is no event to log ownership assignment in the constructor.  
- **Recommendation**: Emit an `OwnershipTransferred(address(0), msg.sender)` event in the constructor (optional).

---

### [F4] No receive or fallback function  
- **Severity**: Info  
- **Description**: The contract does not implement a `receive()` function, so it won't accept plain ETH transfers.  
- **Recommendation**: Consider adding `receive() external payable {}` to support direct ETH transfers.

---

## 🔚 Final Notes

The `FundTracker` contract is functionally solid for ETH tracking and withdrawal with basic access control.  
It uses custom errors efficiently and emits proper events.  
No major vulnerabilities were found. The suggestions above improve gas efficiency and developer clarity.

