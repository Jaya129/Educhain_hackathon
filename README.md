# Educhain_hackathon
# 🎰 **Lottery Smart Contract**  

## 📌 **Overview**  
This project implements a **decentralized lottery system** on the Ethereum blockchain using Solidity. Participants enter the lottery by sending **0.00001 ETH**, and once at least **3 players** have joined, the contract owner (manager) can randomly pick a **winner** who receives the entire balance of the contract.

---

## 🚀 **Features**  
- **Entry Fee:** Participants must send exactly **0.00001 ETH** to join.  
- **Random Winner Selection:** Uses `keccak256` hashing with blockchain randomness.  
- **Secure Fund Handling:** Only the contract manager can access the balance and pick a winner.  
- **Automated Reset:** The lottery resets after a winner is selected.  

---

## 🛠 **Technology Stack**  
- **Smart Contract Language:** Solidity (`^0.5.0 < 0.9.0`)  
- **Blockchain:** Ethereum-compatible networks  
- **Tools:** Remix IDE, Hardhat, MetaMask, Ethers.js  

---

## 📜 **Smart Contract: `lottery.sol`**  

### **1️⃣ Contract Variables**
- `manager` → The deployer who controls the lottery.  
- `players` → A dynamic array storing participants.  

### **2️⃣ Entry Mechanism (`receive`)**
- Players send **0.00001 ETH** to enter.  
- The contract automatically adds them to the `players` list.  
- If incorrect ETH is sent, the transaction fails.  

### **3️⃣ Winner Selection (`pickWinner`)**
- Can only be called by the manager.  
- Requires **at least 3 players**.  
- Uses a pseudo-random number to select a winner.  
- Transfers the **entire contract balance** to the winner.  
- Resets the `players` array for a new round.  

---

## 📌 **How to Deploy & Use**  

### **1️⃣ Deploying the Contract**  
- Open **Remix IDE** and create `lottery.sol`.  
- Compile the contract using Solidity **0.8.x** compiler.  
- Deploy on **Ethereum Testnet (e.g., Sepolia, Goerli)** or **Local Hardhat Network**.  

### **2️⃣ Participating in the Lottery**  
- Send **0.00001 ETH** to the contract from **MetaMask** or a script.  

#### **Example using ethers.js**:  
```javascript
const signer = provider.getSigner();
const tx = await signer.sendTransaction({
    to: "0xYourContractAddress",
    value: ethers.utils.parseEther("0.00001") // Entry fee
});
await tx.wait();
console.log("Successfully joined the lottery!");
```

### **3️⃣ Picking a Winner**  
- Call `pickWinner()` (only the manager can do this).  
- Winner receives all ETH in the contract.  
- The lottery resets for a new round.  

---

## 🔐 **Security Considerations**  
- The contract **does not use Chainlink VRF**, so randomness is **not truly secure**.  
- A miner could manipulate `block.prevrandao` (previously `block.difficulty`).  
- This should **not be used for high-value lotteries** on mainnet.  

---

## 🏆 **Future Improvements**  
✅ Implement **Chainlink VRF** for fair randomness.  
✅ Add **automated winner selection** after a fixed time.  
✅ Support **multiple rounds** without requiring manual resets.  

---

## 📜 **License**  
This project is licensed under the **GPL-3.0** License.  

---

### 🚀 **Happy Coding & Good Luck with the Lottery!** 🎉
