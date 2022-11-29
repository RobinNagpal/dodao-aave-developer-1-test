## Header
This is the course header. This will be added on top of every page. Go to [DoDAO.io](https://www.dodao.io) to know more.

 ---
 
 ## AAVE Smart Contracts
 
 
---

##### Select the correct option.  

- [ ]  Borrowing in Aave is undercollateralized
- [x]  Borrowing in Aave is overcollateralized
- [ ]  Depositing in Aave is overcollateralized
- [ ]  None of the above
  
Hint: NoHint
         
Explanation: Since cryptocurrency is highly volatile, borrowing in Aave demands overcollateralization.

Sub Topics: aave-smart-contracts-intro
 

---

##### When does a liquidation event occur?  

- [ ]  When the price of the collateral rises above the liquidation threshold
- [ ]  When the price of the collateral is equal to the liquidation threshold
- [x]  When the price of the collateral drops below the liquidation threshold
- [ ]  When the price of the collateral doubles the liquidation threshold
  
Hint: NoHint
         
Explanation: A liquidation event happens when the price of the collateral drops below the liquidation threshold.

Sub Topics: aave-smart-contracts-intro
 

---

##### What is Liquidation Bonus?  

- [ ]  The bonus paid to liquidators to encourage the purchase of specified collateral with a health factor more than one
- [ ]  The bonus paid to liquidators to encourage the purchase of specified collateral with a health factor equal to one
- [ ]  The bonus paid to liquidators to encourage the purchase of specified collateral with a health factor more than or equal to one
- [x]  The bonus paid to liquidators to encourage the purchase of specified collateral with a health factor less than one
  
Hint: NoHint
         
Explanation: Liquidation bonus is the bonus paid to liquidators to encourage the purchase of specified collateral with a health factor less than one

Sub Topics: terminology
 

---

##### What is the maximum borrowing capacity of a particular collateral known as?  

- [ ]  Liquidation Threshold
- [ ]  Liquidity Index
- [x]  Loan To Value
- [ ]  Liquidation Bonus
  
Hint: NoHint
         
Explanation: Loan To Value is the maximum borrowing capacity of a particular collateral. If a collateral has a Loan to Value of 75%, the user will be allowed to borrow 0.75 ETH of primary currency for every 1 ETH of collateral. The Loan To Value is represented in percentage points and is set per collateral.

Sub Topics: terminology
 

---

##### What do you understand by liquidation threshold?  

- [x]  The amount of a borrow position that must be liquidated because it is undercollateralized
- [ ]  The ratio of total collateral multiplied by the liquidation threshold to borrowed principal
- [ ]  The amount of a borrow position that must be liquidated because it is overcollateralized
- [ ]  The maximum borrowing capacity of a particular collateral
  
Hint: NoHint
         
Explanation: Liquidation Threshold is the amount of a borrow position that must be liquidated because it is undercollateralized. When a collateral has an 80% liquidation threshold, it signifies that the loan will be liquidated when the debt value equals 80% of the collateral value. The liquidation threshold is defined in percentage points and is specified per collateral.

Sub Topics: terminology
 

---

##### How many versions of the AAVE protocol have been released?  

- [ ]  One
- [ ]  Two
- [x]  Three
- [ ]  Zero
  
Hint: NoHint
         
Explanation: Aave has released three versions (v1, v2 and v3) as of now.

Sub Topics: versions
 

---

##### What is Health Factor?  

- [x]  The ratio of total collateral multiplied by the liquidation threshold to borrowed principal
- [ ]  The ratio of total collateral multiplied by the borrowed principal to liquidation threshold
- [ ]  The ratio of total collateral to borrowed principal
- [ ]  The ratio of total collateral to liquidation threshold
  
Hint: NoHint
         
Explanation: Health factor is the ratio of total collateral multiplied by the liquidation threshold to borrowed principal. When the Health Factor falls below one, the loan is considered undercollateralized and can be liquidated.

Sub Topics: terminology
 

---

##### Which contract has been decommissioned in Aave v2?  

- [ ]  LendingPoolAddressesProvider
- [ ]  LendingPool
- [x]  LendingPoolCore
- [ ]  LendingPoolAddressesProviderRegistry
  
Hint: NoHint
         
Explanation: LendingPoolCore has been decommissioned. Only LendingPool is used, which simplifies integrations and Aave v2 development.

Sub Topics: versions
 

---

##### Pick the correct option(s).  

- [x]  Many flash loans with varied parameters can now be performed in the same call
- [ ]  Many flash loans with varied parameters can not be performed in the same call
- [x]  You can now do a combination of 'conventional' flash loans that are paid back instantly and flash loans that incur debt
- [ ]  You can not do a combination of 'conventional' flash loans that are paid back instantly and flash loans that incur debt
  
Hint: NoHint
         
Explanation: Flash loans can now be executed in batches, which means that many flash loans with varied parameters can be performed in the same call. This opens the door to strong new use cases, such as repaying numerous assets and positions with a single flash loan transaction. You can now do a combination of 'conventional' flash loans that are paid back instantly and flash loans that incur debt (i.e. the flash loan is not paid back immediately).

Sub Topics: versions
 

---

##### Which contract is the main entry point into the Aave Protocol?  

- [ ]  LendingPoolAddressesProvider
- [x]  LendingPool
- [ ]  LendingPoolCore
- [ ]  LendingPoolAddressesProviderRegistry
  
Hint: NoHint
         
Explanation: LendingPool is the main entry point into the Aave Protocol. Most interactions with Aave will happen via the LendingPool.

Sub Topics: overview
 

---

##### Which contract can be used to obtain the most recent contract addresses?  

- [x]  LendingPoolAddressesProvider
- [ ]  LendingPool
- [ ]  LendingPoolCore
- [ ]  LendingPoolAddressesProviderRegistry
  
Hint: NoHint
         
Explanation: LendingPoolAddressesProvideris the protocol's primary addresses register for specific marketplaces. The most recent contract addresses should be obtained from this contract by making the necessary calls.

Sub Topics: overview
 

---

##### Which of the following methods is not included in the LendingPool contract?  

- [ ]  deposit()
- [ ]  borrow()
- [ ]  withdraw()
- [x]  scaledTotalSupply()
  
Hint: NoHint
         
Explanation: Most interactions with Aave will happen via the LendingPool, including deposit(), borrow(), repay(), swapBorrowRateMode(), setUserUseReserveAsCollateral(), withdraw(), flashloan(), liquidationCall().

Sub Topics: overview
 

---

##### Despite all of the new features added in v3, the overall gas cost of all functions fell. By what percentage did the gas cost fall?  

- [ ]  The overall gas cost of all functions fell by about 50%
- [x]  The overall gas cost of all functions fell by about 25%
- [ ]  The overall gas cost of all functions fell by about 2.5%
- [ ]  The overall gas cost of all functions fell by about 5%
  
Hint: NoHint
         
Explanation: explanation

Sub Topics: versions
 

---

##### Can any individual lend and borrow simultaneously via Aave?  

- [x]  Yes, any individual lend and borrow simultaneously via Aave
- [ ]  No, any individual can not lend and borrow simultaneously via Aave
- [ ]  Only possible when the price of the collateral drops below the liquidation threshold
- [ ]  Only possible when the price of the collateral rises above the liquidation threshold
  
Hint: NoHint
         
Explanation: An individual can lend and borrow simultaneously via Aave. The participants lending the tokens get interest on their loan and the participants borrowing the tokens pay interest.

Sub Topics: aave-smart-contracts-intro
 

---

##### What happens when the Health Factor falls below one?  

- [ ]  The loan is considered overcollateralized and can be liquidated.
- [ ]  The loan is considered undercollateralized and can not be liquidated.
- [x]  The loan is considered undercollateralized and can be liquidated.
- [ ]  The loan is considered overcollateralized and can not be liquidated.
  
Hint: NoHint
         
Explanation: Health factor is the ratio of total collateral multiplied by the liquidation threshold to borrowed principal. When the Health Factor falls below one, the loan is considered undercollateralized and can be liquidated.

Sub Topics: terminology
 

---

##### What is the ratio in which aTokens can be redeemed for the underlying token?  

- [ ]  aTokens can be redeemed for the underlying token in a 1:10 ratio
- [ ]  aTokens can be redeemed for the underlying token in a 11:1 ratio
- [x]  aTokens can be redeemed for the underlying token in a 1:1 ratio
- [ ]  aTokens can be redeemed for the underlying token in a 1:11 ratio
  
Hint: NoHint
         
Explanation: aTokens can be redeemed for the underlying token in a 1:1 ratio

Sub Topics: functions-1
 

---

##### Pick the correct option(s).  

- [x]  AAVE protocol does not employ an EIP-20 wrapper
- [ ]  AAVE protocol employs an EIP-20 wrapper
- [ ]  The deposit() method's amount parameter must match the transaction's msg.value parameter
- [ ]  The deposit() method's amount parameter may or may not match the transaction's msg.value parameter
  
Hint: NoHint
         
Explanation: Because the protocol does not employ an EIP-20 wrapper like wETH for ETH deposits, the deposit() method's amount parameter must match the transaction's msg.value parameter and be included in your deposit() call.

Sub Topics: functions-1
 

---

##### Which method allows the user's deposit to be used as collateral?  

- [ ]  deposit()
- [ ]  setUserUseDepositAsCollateral()
- [ ]  setUserReserveAsCollateral()
- [x]  setUserUseReserveAsCollateral()
  
Hint: NoHint
         
Explanation: setUserUseReserveAsCollateral() allows the user's deposit to be used as collateral. Users will only be able to disable deposits that are not being used as collateral at the time.

Sub Topics: functions-1
 

---

##### Which of the following statements about the repay() method is/are correct?  

- [ ]  A borrowed asset has to be repaid in whole
- [x]  A borrowed asset can be repaid in whole or in part
- [x]  A third-party can repay another user's debt on their behalf
- [ ]  A third-party can not repay another user's debt on their behalf
  
Hint: NoHint
         
Explanation: repay() method is used to repay a borrowed asset in whole or in part. The _onBehalfOf parameter can be used to repay a different user's debt. When a third-party repays another user's debt on their behalf, the third-party address must approve() the LendingPoolCore contract (which is separate from the LendingPool contract) with the _amount of the underlying ERC20 of the _reserve contract.

Sub Topics: functions-2
 

---

##### Which method changes the borrow rate modes of the msg.sender from stable to variable?  

- [ ]  rebalanceStableBorrowRate()
- [ ]  rebalanceBorrowRateMode()
- [ ]  swapStableBorrowRate()
- [x]  swapBorrowRateMode()
  
Hint: NoHint
         
Explanation: swapBorrowRateMode() changes the borrow rate modes of the msg.sender from stable to variable. rebalanceStableBorrowRate() rebalances the stable rate of _user

Sub Topics: functions-2
 

---

##### What happens when a liquidation is completed successfully?  

- [x]  The position's health factor is enhanced, bringing it above 1
- [ ]  The position's health factor is diminished, bringing it below 1
- [ ]  The close factor is enhanced, bringing it above 1
- [ ]  The close factor is diminished, bringing it below 1
  
Hint: NoHint
         
Explanation: When the liquidation is completed successfully, the position's health factor is enhanced, bringing it above 1. It does not affect the close factor.

Sub Topics: functions-2
 

---

##### What is the close factor?  

- [ ]  The ratio of total collateral multiplied by the liquidation threshold to borrowed principal
- [ ]  The maximum borrowing capacity of a particular collateral
- [x]  Determines how much collateral a liquidator can close
- [x]  It is the amount of the liquidation discount
  
Hint: NoHint
         
Explanation: A close factor determines how much collateral a liquidator can close. The current close factor is 0.5. In other words, liquidators can only liquidate up to 50% of the amount owing in a position. This is the amount of the liquidation discount.

Sub Topics: functions-2
 

---

##### What value of the purchaseAmount parameter can be set to proceed with the largest liquidation allowed by the close factor?  

- [ ]  uint(1)
- [x]  uint(-1)
- [ ]  uint(10)
- [ ]  uint(-10)
  
Hint: NoHint
         
Explanation: purchaseAmount parameter can be set to uint(-1) and the protocol will proceed with the largest liquidation allowed by the close factor.

Sub Topics: functions-2
 

---

##### Select the correct statement(s) about Flash loans.  

- [x]  Flash loans are also called One Block Borrows
- [x]  Borrowed amount has to be returned in the same transaction
- [ ]  There is no need to pay fees
- [ ]  User has to provide collateral prior to the transaction
  
Hint: NoHint
         
Explanation: Flash Loans are special transactions that allow you to borrow an asset as long as the borrowed amount (plus a fee) is returned before the transaction ends (also called One Block Borrows). These transactions do not necessitate the provision of collateral by the user prior to the transaction.

Sub Topics: 
 

---

##### Which of the following is the fee received by LP?  

- [ ]  FLASHLOAN_PREMIUM_TO_PROTOCOL
- [ ]  FLASHLOAN_PREMIUM_TOTAL
- [x]  FLASHLOAN_PREMIUM_TOTAL - FLASHLOAN_PREMIUM_TO_PROTOCOL
- [ ]  FLASHLOAN_PREMIUM_TOTAL + FLASHLOAN_PREMIUM_TO_PROTOCOL
  
Hint: NoHint
         
Explanation: Fee to LP = FLASHLOAN_PREMIUM_TOTAL - FLASHLOAN_PREMIUM_TO_PROTOCOL, Fee to Protocol = FLASHLOAN_PREMIUM_TO_PROTOCOL

Sub Topics: functions-3
 
