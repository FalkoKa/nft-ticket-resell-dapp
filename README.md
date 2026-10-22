# NFT Ticket Resell dApp

Event tickets as NFTs: organisers deploy their own event contract and earn a royalty on every resale.

**[Live demo](https://resell-dapp-frontend.vercel.app/)** · runs on the Sepolia testnet, needs MetaMask and Sepolia ETH

**Stack:** Solidity (ERC-721) · Hardhat · Next.js · TypeScript · Scaffold-ETH 2 (wagmi, viem, RainbowKit) · Tailwind · NestJS · MongoDB Atlas

Built in one week by a team of six as the final project of the [Encode Solidity Bootcamp](https://www.encode.club/solidity-bootcamps) (Q4 2023). Original repository: [bangtam1994/Re-sell-dapp](https://github.com/bangtam1994/Re-sell-dapp)

## My role

- **Frontend foundation:** set up the Next.js app on the Scaffold-ETH template with routing for all pages, and built the landing page, header and wallet-connected states.
- **Create-event flow:** built the page where organisers deploy their own `Event` contract from the browser with viem (price, ticket count, royalty slider), predict the contract address from the wallet nonce and register the event with the backend.
- **Event listing:** event card component and the event overview on the landing page.
- **Smart contract fixes:** fixed the ticket-quantity and resale-queue conditions in `Event.sol` and redeployed the contract to Sepolia.
- **Deployment and docs:** prepared the NestJS API for deployment, wrote the final README and screenshots.

## How it works

The project addresses the issue of event owners not benefiting from resales of their tickets on the secondary market.

An event creator can create an event, which deploys an `Event.sol` contract on-chain. The owner specifies the number of available tickets, the price per ticket and the royalty percentage they receive for each ticket sold on the secondary market.

A user can buy a ticket, which mints a ticket NFT if fewer tickets than the total have been minted. Once the event is sold out, a buyer gets the first ticket from the resale queue (an on-chain FIFO array), as long as a seller is waiting there.

A user can also resell their ticket. When it reaches the front of the queue and is bought, the royalty share of the price goes to the event creator automatically.

## Screenshots

### Events available

![Landing Page](./images/landing-page.png)
![Landing Page after connecting](./images/landing-page-wallet-connected.png)
After connecting a wallet, you see all events: the ones you created, the ones you attend (you own a ticket NFT) and all others.

### Create your event on-chain

![Create Event](./images/create-event.png)
Set a price, the number of tickets and your royalty for resales, then deploy the Event contract.

### Buy a ticket NFT

![Buy a ticket NFT](./images/event-page.png)

### Resell your ticket

![Resell Ticket](./images/after-buying-ticket.png)
![Resell Ticket Queue](./images/reselling-ticket.png)
Your ticket goes into the resale queue. Once it is first in line, the next buyer buys it from you and the event creator receives their share.

## Project structure

```
frontend/packages/hardhat   Solidity contracts (Event.sol) and deployment scripts
frontend/packages/nextjs    Next.js dApp (Scaffold-ETH 2)
backend/resell-dapp-api     NestJS REST API with MongoDB
```

## Run locally

```bash
# frontend (from frontend/)
yarn install
cp packages/nextjs/.env.example packages/nextjs/.env.local
yarn start

# backend (from backend/resell-dapp-api/)
npm install
cp .env.example .env   # add your own MongoDB connection string
npm run start:dev
```
