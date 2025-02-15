# **Solana Raydium Sniper Bot** 

## **Contact**

[@midaBricoll](https://t.me/midaBricoll)

## **Features**  
- Sniping tokens with WSOL  
- Automated selling mechanism  
- Take Profit (TP) and Stop Loss (SL) functionality  
- Minimum liquidity filter  
- Liquidity burn and lock verification  
- Mint renounce check  
- High-speed transaction execution  

---

## **Setup Instructions**  

### **Prerequisites**  
1. Create a new, empty Solana wallet.  
2. Transfer SOL into the wallet.  
3. Convert some SOL into either USDC or WSOL, depending on the bot’s configuration.  

### **Configuration**  
1. Update the configuration file `.env.copy` and remove `.copy` from the filename once done.  
2. Set the following parameters:  
   - `PRIVATE_KEY`: Enter your wallet’s private key.  
   - `RPC_ENDPOINT`: Specify the HTTPS RPC endpoint.  
   - `RPC_WEBSOCKET_ENDPOINT`: Provide the WebSocket RPC endpoint.  
   - `QUOTE_MINT`: Choose the liquidity pool to snipe (USDC or WSOL).  
   - `QUOTE_AMOUNT`: Define the amount used for each token purchase.  
   - `COMMITMENT_LEVEL`: Set the transaction confirmation level.  
   - `CHECK_IF_IS_BURNED`: Enable liquidity burn verification.  
   - `CHECK_IF_IS_LOCKED`: Enable liquidity lock verification.  
   - `USE_SNIPE_LIST`: Restrict purchases to tokens listed in `snipe-list.txt`.  
   - `SNIPE_LIST_REFRESH_INTERVAL`: Set how frequently the bot updates the snipe list (in milliseconds).  
   - `CHECK_IF_MINT_IS_RENOUNCED`: Ensure the bot only buys renounced tokens.  
   - `MIN_POOL_SIZE`: Define the minimum liquidity pool size required for a transaction.  
   - `TAKE_PROFIT`: Set the take-profit percentage (default is 50%).  
   - `STOP_LOSS`: Set the stop-loss percentage (default is 30%).  
   - `BIRDEYE_API_KEY`: Obtain an API key from Birdeye for additional security checks (generate it at [Birdeye API Docs](https://docs.birdeye.so/docs/authentication-api-keys)).  

---

## **Installation and Execution**  
1. Install dependencies using:  
   ```sh
   npm install
   ```  
2. Start the bot by running:  
   ```sh
   npm run start
   ```  

---

## **Take Profit and Stop Loss**  

By default:  
- **Take Profit** is set at **50%**.  
- **Stop Loss** is set at **30%**.  

These values can be adjusted in the `.env` file.  

---

## **Auto-Sell Functionality**  

By default, the bot will automatically sell tokens. To disable this feature:  
1. Set `AUTO_SELL` to `false`.  
2. Adjust `MAX_SELL_RETRIES` to define how many times the bot should attempt selling.  
3. Configure `AUTO_SELL_DELAY` to introduce a delay before selling (in milliseconds).  

If `AUTO_SELL_DELAY` is set to `0`, the bot will sell the token immediately after purchase. There is no guarantee of profit or successful execution, and users assume all risk associated with this feature.  

---

## **Snipe List Usage**  

By default, the bot purchases any token that has a new liquidity pool open for trading.  
To restrict purchases to specific tokens:  
1. Set `USE_SNIPE_LIST` to `true`.  
2. Add token mint addresses to the `snipe-list.txt` file, with each address on a new line.  

The snipe list can be updated while the bot is running. The bot will check for updates at the interval specified by `SNIPE_LIST_REFRESH_INTERVAL`.  

**Important:** The token’s liquidity pool must not exist before the script starts. The bot will only execute a purchase when a new liquidity pool is created. Ensure the bot is running before the token’s launch if sniping a specific token.  

---

## **Troubleshooting Common Issues**  

### **Empty Transactions**  
If transactions appear empty on SolScan, try changing `COMMITMENT_LEVEL` to `finalized`.  

### **Unsupported RPC Node**  
If you receive the following error:  
```sh
Error: 410 Gone:  {"jsonrpc":"2.0","error":{"code": 410, "message":"The RPC call or parameters have been disabled."}, "id": "986f3599-b2b7-47c4-b951-074c19842bad"}
```  
This indicates that the selected RPC node does not support the required methods.  
**Solution:** Switch to a different RPC provider such as **Shyft, Helius, or QuickNode**.  

### **No Token Account Found**  
If you encounter this error:  
```sh
Error: No SOL token account found in wallet:
```  
It means your wallet does not have a USDC or WSOL token account.  
**Solution:** Swap some SOL to USDC/WSOL on a decentralized exchange (DEX). Once swapped, the token should appear in your wallet.  

For any additional issues, enable debugging mode by setting `LOG_LEVEL` to `debug` in the configuration file. If the issue persists, report it in the repository’s issue tracker.

