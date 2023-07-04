# ZkSyncDepositScript
This script demonstrates how to deposit ERC20 tokens (such as USDT) from Ethereum to ZkSync using the ZkSync JavaScript library
const { ethers } = require("ethers");
const { Wallet } = require("zksync");

// Set up your ZkSync provider and wallet
const zkSyncProvider = ethers.getDefaultProvider("mainnet");
const privateKey = "your-private-key";
const zkSyncWallet = await Wallet.fromEthSigner(new ethers.Wallet(privateKey), zkSyncProvider);

// Specify the token and amount to deposit
const token = "USDT";
const amount = ethers.utils.parseUnits("1000", 6);

// Deposit funds to ZkSync
const deposit = await zkSyncWallet.depositToSyncFromEthereum({
  depositTo: zkSyncWallet.address(),
  token,
  amount,
});

// Wait for the deposit to be confirmed
const receipt = await deposit.awaitReceipt();

console.log("Transaction hash:", receipt.transactionHash);
console.log("Deposit complete!");
