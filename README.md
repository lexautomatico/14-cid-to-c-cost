# 14-CID-TO-C-COST
# FreeWeb3 & Evidencer Ecosystem

![Ecosystem Logo](logo-sm.png)

## Overview

Welcome to the FreeWeb3 & Evidencer ecosystem - an integrated suite of Web3 applications focused on legal technology, evidence management, and dispute resolution. This monorepo contains over 25 specialized applications that work together to provide a comprehensive solution for legal professionals, organizations, and individuals engaging with digital evidence and smart contracts.

## Ecosystem Architecture

The ecosystem consists of two major product lines:

### FreeWeb3 Platform
A collection of foundational Web3 utilities enabling secure file management, encryption, and cross-chain communication.

### Evidencer Platform
Legal-focused applications built on top of FreeWeb3, providing specialized tools for evidence collection, claim management, and dispute resolution.

## Core Technologies

- **React & Next.js**: Modern frontend frameworks
- **Material UI**: Consistent design system with light/dark mode
- **IPFS Integration**: Decentralized file storage
- **Encryption**: Client-side AES-256 encryption
- **Ethereum & EVM Chains**: Smart contract functionality across multiple blockchains
- **Chainlink CCIP**: Cross-chain interoperability
- **TypeScript**: Type safety and improved developer experience

## Installation

Each application can be run independently or as part of the integrated ecosystem:

1. Navigate to the specific application directory
2. Install dependencies: `npm install`
3. Start development server: `npm start` or `npm run dev`
4. Build for production: `npm run build`

## Security

- All applications use environment variables for sensitive configuration
- Private keys should never be hardcoded (see SECURITY_SECRETS_INVENTORY.md)
- Each application has a SECURITY_TODO.md file with specific security requirements

## Deployment

All applications are configured for deployment on Vercel:

1. Each application has its own vercel.json configuration
2. Applications are deployed to various domains including:
   - freeweb3.com
   - evidencer.io

## Domain Structure

Applications are distributed across domains based on their purpose:

- **freeweb3.com**: Core Web3 utilities and foundational services
- **evidencer.io**: Legal tech applications and forms

## License

All projects are licensed under the terms specified in their individual LICENSE files.

---

This monorepo is maintained by the FreeWeb3 & Evidencer team. For questions or support, please contact: support@evidencer.io