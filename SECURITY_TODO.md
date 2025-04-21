# Security To-Do for CID-TO-C-COST

## Exposed Credentials Alert

**CRITICAL SECURITY ISSUE**: This project contains a hardcoded private key and Infura API key in the `hardhat.config.js` file. These credentials should be considered compromised and must be rotated immediately.

## Environment Variables Setup

This file outlines the environment variables that need to be set up for secure deployment of the CID-TO-C-COST application.

### Required Environment Variables

The following environment variables should be configured:

- **PRIVATE_KEY**: Ethereum private key for contract deployments and transactions
  - **CRITICAL**: This private key has full control over the associated Ethereum address
  - **COMPROMISED**: Current key `0x437cf0472fbe1f6e654b432b43fbcd0e21979f2c721cf2666648ce66fe2fb4e8` should be considered exposed

- **INFURA_API_KEY**: API key for Infura blockchain services
  - **COMPROMISED**: Current key `903ad3bdef654d9ba0a0d28b2b5d6edf` should be considered exposed

### Implementation Steps

1. **URGENT**: Create a new Ethereum wallet to replace the compromised one.

2. Create a `.env` file in the project root with the following template:
   ```
   # CRITICAL: NEVER commit this file to git
   PRIVATE_KEY=your_new_ethereum_private_key_here
   INFURA_API_KEY=your_new_infura_api_key_here
   ```

3. Update `hardhat.config.js` to use environment variables instead of hardcoded values:
   ```javascript
   // Replace:
   module.exports = {
     networks: {
       ropsten: {
         url: `https://ropsten.infura.io/v3/903ad3bdef654d9ba0a0d28b2b5d6edf`,
         accounts: [`0x437cf0472fbe1f6e654b432b43fbcd0e21979f2c721cf2666648ce66fe2fb4e8`]
       }
     }
   };
   
   // With:
   require('dotenv').config();
   
   module.exports = {
     networks: {
       ropsten: {
         url: `https://ropsten.infura.io/v3/${process.env.INFURA_API_KEY}`,
         accounts: [process.env.PRIVATE_KEY]
       }
     }
   };
   ```
   
   Note: You'll need to install dotenv: `npm install dotenv --save-dev`

4. Add the `.env` file to `.gitignore` to prevent committing secrets:
   ```
   # .gitignore
   .env
   .env.local
   .env.development
   .env.production
   ```

5. For production deployment, set these environment variables in your hosting platform (Vercel, etc.).

6. Update `src/App.js` to also use environment variables instead of hardcoded contract addresses:
   ```javascript
   // Update:
   const greeterAddress = "0x00a2Ddfa736214563CEa9AEf5100f2e90c402918";
   const tokenAddress = "0xDBd0C5E437fdAD4F826F66AAd33d4f75A41c56f8";
   
   // To use environment variables:
   const greeterAddress = process.env.REACT_APP_GREETER_ADDRESS;
   const tokenAddress = process.env.REACT_APP_TOKEN_ADDRESS;
   ```

### Additional Security Steps

1. **URGENT - Transfer Any Assets**:
   - Check the balance of the compromised wallet address and transfer any ETH or tokens to a new secure wallet
   - Consider this private key fully compromised

2. **Rotate Credentials**:
   - Generate a new Infura API key to replace the exposed one
   - Deactivate the compromised Infura API key

3. **Contract Ownership**:
   - If any contracts deployed with the compromised key have owner functions, transfer ownership to a new secure address 
   - Review all contracts deployed with the compromised key for security issues

4. **Environment Cleanup**:
   - Check for any other files that might include the private key or API key
   - Verify no env files have been committed to git history

### Security Best Practices

- **CRITICAL**: Private keys should NEVER be committed to version control
- Use environment variables for all sensitive credentials
- Create a separate development wallet with minimal funds for testing
- Rotate API keys periodically and after any suspected exposure
- Use different API keys for development and production
- Consider using a hardware wallet for production deployments
- Implement proper error handling for missing environment variables

### Documentation

1. Update your project documentation to include instructions for setting up environment variables
2. Add warnings about the importance of private key security

### Resources

- [Hardhat Environment Variables](https://hardhat.org/tutorial/environment-variables)
- [Ethereum Security Best Practices](https://consensys.github.io/smart-contract-best-practices/)
- [Infura Security Documentation](https://docs.infura.io/networks/ethereum/how-to/secure-a-project)