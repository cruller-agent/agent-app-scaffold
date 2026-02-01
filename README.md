# Agent App Template 🤖⚙️

**Production-grade bootstrap for autonomous agent applications**

This template provides everything you need to launch an agent-built application on Base with decentralized hosting, onchain identity, and rapid iteration.

## Why This Template?

**For Agents:**
- ✅ One command to scaffold new apps
- ✅ Built-in IPFS deployment
- ✅ ENS + Limo integration ready
- ✅ Hot reload for contracts + frontend
- ✅ Proven stack from top agents (@clawdbotatg)

**For DonutDAO:**
- ✅ Standardized app structure
- ✅ Easy to maintain (not a monorepo)
- ✅ Composable across projects
- ✅ Fork, customize, ship

## Tech Stack

Based on **Scaffold-ETH 2** + **Base** + **IPFS** (the stack that built 7 dApps overnight)

### Core Technologies
- **Foundry** - Fast contract testing
- **Hardhat** - Production deployments
- **Next.js** - Modern frontend (React 18+)
- **wagmi + viem** - Type-safe Web3
- **TailwindCSS** - Utility-first styling
- **IPFS** - Decentralized hosting
- **Base L2** - Fast + cheap execution

### Agent Infrastructure
- **ERC-8004** - Onchain agent identity
- **Bankr SDK** - Multi-chain execution (optional)
- **OpenClaw** - Agent orchestration (optional)

## Quick Start

### 1. Fork & Clone

```bash
# Fork this repo on GitHub
# Then clone your fork
git clone https://github.com/YOUR_USERNAME/your-app-name.git
cd your-app-name

# Install dependencies
yarn install
```

### 2. Configure

```bash
# Copy environment template
cp .env.example .env

# Add your keys
# DEPLOYER_PRIVATE_KEY=0x...
# BASE_RPC_URL=https://mainnet.base.org
# BASESCAN_API_KEY=...
```

### 3. Develop

```bash
# Start local chain
yarn chain

# Deploy contracts (in new terminal)
yarn deploy

# Start frontend (in new terminal)
yarn start

# Visit http://localhost:3000
```

### 4. Deploy to Production

```bash
# Deploy contracts to Base
yarn deploy --network base

# Build frontend
yarn build

# Deploy to IPFS
yarn ipfs:publish

# Register ENS name pointing to IPFS hash
# Access via yourapp.limo
```

## Project Structure

```
agent-app-template/
├── packages/
│   ├── foundry/              # Smart contracts (Foundry)
│   │   ├── contracts/        # Your Solidity contracts
│   │   ├── test/             # Contract tests
│   │   └── script/           # Deployment scripts
│   │
│   ├── hardhat/              # Alternative: Hardhat setup
│   │   ├── contracts/        # Solidity contracts
│   │   ├── deploy/           # Deploy scripts
│   │   └── test/             # Tests
│   │
│   └── nextjs/               # Frontend application
│       ├── app/              # Next.js app router
│       ├── components/       # React components
│       ├── contracts/        # Generated contract ABIs
│       └── hooks/            # Custom React hooks
│
├── .env.example              # Environment template
├── .gitignore                # Git ignore rules
├── package.json              # Workspace config
└── README.md                 # This file
```

## Development Workflow

### Local Development

1. **Start local chain** - `yarn chain`
2. **Deploy contracts** - `yarn deploy`
3. **Start frontend** - `yarn start`
4. **Iterate** - Hot reload for both contracts and UI

### Testing

```bash
# Test contracts
yarn foundry:test

# Test with gas report
yarn foundry:test --gas-report

# Test coverage
yarn foundry:coverage
```

### Production Deployment

```bash
# 1. Deploy to Base mainnet
yarn deploy --network base

# 2. Verify on Basescan
yarn verify --network base

# 3. Build optimized frontend
yarn build

# 4. Deploy to IPFS
yarn ipfs:publish
# → Returns IPFS hash: QmXYZ...

# 5. Update ENS content hash
# Via app.ens.domains or ENS CLI
```

## Customization

### 1. Update Package Info

Edit `package.json`:
```json
{
  "name": "your-app-name",
  "description": "Your app description",
  "author": "YourAgentName"
}
```

### 2. Update Contract

Edit `packages/foundry/contracts/YourContract.sol`:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract YourContract {
    // Your logic here
}
```

### 3. Update Frontend

Edit `packages/nextjs/app/page.tsx`:
```typescript
export default function Home() {
  return (
    <div>
      {/* Your UI here */}
    </div>
  );
}
```

### 4. Update Deployment

Edit `packages/foundry/script/Deploy.s.sol`:
```solidity
contract Deploy is Script {
    function run() external {
        // Your deployment logic
    }
}
```

## Built-In Features

### Contract Auto-Import
- Frontend automatically detects deployed contracts
- ABIs generated and imported
- Type-safe contract interactions via wagmi

### Hot Reload
- Contract changes → auto-recompile → auto-redeploy
- Frontend changes → instant update
- No manual restarts needed

### Debug UI
- Auto-generated contract interaction UI
- Read/write functions exposed
- Event logs visible
- Great for testing

### IPFS Publishing
- One command to build + upload
- Automatic pinning (via Pinata/Infura)
- Returns CID for ENS registration

### Multi-Network Support
- Local (Hardhat node)
- Base Sepolia (testnet)
- Base (mainnet)
- Easy to add more chains

## Agent-Specific Features

### ERC-8004 Integration (Optional)

Add agent identity to your app:

```typescript
import { useAgentIdentity } from "@/hooks/useAgentIdentity";

function YourComponent() {
  const { agentId, reputation } = useAgentIdentity(
    "0x608044ffa0ecfdf91a4e235304685559158a3a72" // Your agent wallet
  );
  
  return <div>Agent #{agentId} - Rep: {reputation}</div>;
}
```

### Bankr SDK Integration (Optional)

Add autonomous trading:

```typescript
import { useBankr } from "@/hooks/useBankr";

function TradingComponent() {
  const { executeSwap } = useBankr();
  
  const handleTrade = async () => {
    await executeSwap({
      fromToken: "ETH",
      toToken: "USDC",
      amount: "1.0"
    });
  };
  
  return <button onClick={handleTrade}>Execute Trade</button>;
}
```

## Environment Variables

Required variables (`.env`):

```bash
# Deployment
DEPLOYER_PRIVATE_KEY=0x...        # Your deployment wallet

# RPC Endpoints
BASE_RPC_URL=https://mainnet.base.org
BASE_SEPOLIA_RPC_URL=https://sepolia.base.org

# Block Explorers
BASESCAN_API_KEY=...              # For contract verification

# IPFS (optional - uses public gateway by default)
IPFS_PROJECT_ID=...
IPFS_PROJECT_SECRET=...

# Next.js
NEXT_PUBLIC_WALLET_CONNECT_ID=... # Get from WalletConnect
```

## Scripts Reference

```bash
# Development
yarn chain          # Start local Hardhat network
yarn deploy         # Deploy to local network
yarn deploy --network base-sepolia  # Deploy to testnet
yarn deploy --network base          # Deploy to mainnet
yarn start          # Start Next.js dev server

# Testing
yarn foundry:test           # Run Foundry tests
yarn foundry:test --gas-report  # With gas report
yarn foundry:coverage       # Coverage report
yarn hardhat:test           # Run Hardhat tests

# Production
yarn build          # Build optimized frontend
yarn ipfs:publish   # Deploy to IPFS
yarn verify --network base  # Verify contracts

# Utilities
yarn clean          # Clean build artifacts
yarn format         # Format Solidity code
yarn lint           # Lint TypeScript
```

## Best Practices

### 1. Keep Contracts Simple
- One contract per app (or minimal set)
- Gas optimization from day 1
- Comprehensive tests

### 2. Frontend Organization
```
nextjs/
├── app/              # Pages (App Router)
├── components/       # Reusable UI components
│   ├── common/       # Generic components
│   └── contract/     # Contract-specific components
├── hooks/            # Custom React hooks
│   ├── useContract.ts
│   └── useAgent.ts
└── lib/              # Utilities
    ├── contracts.ts  # Contract addresses/ABIs
    └── utils.ts      # Helper functions
```

### 3. Git Workflow
```bash
# Create feature branch
git checkout -b feature/your-feature

# Make changes, commit often
git add .
git commit -m "feat: add your feature"

# Push and create PR
git push origin feature/your-feature
```

### 4. Deployment Checklist
- [ ] Tests passing
- [ ] Gas optimized
- [ ] Frontend builds without errors
- [ ] Contracts verified on Basescan
- [ ] IPFS deployment successful
- [ ] ENS content hash updated
- [ ] Documentation updated

## Examples

### Simple dApp (Token Burner)

```solidity
// contracts/TokenBurner.sol
contract TokenBurner {
    event Burned(address indexed burner, uint256 amount);
    
    function burn() external payable {
        require(msg.value > 0, "Must send ETH");
        emit Burned(msg.sender, msg.value);
    }
}
```

```typescript
// app/page.tsx
import { useScaffoldContractWrite } from "@/hooks/scaffold-eth";

export default function BurnPage() {
  const { writeAsync: burn } = useScaffoldContractWrite({
    contractName: "TokenBurner",
    functionName: "burn",
    value: "0.1", // ETH to burn
  });
  
  return <button onClick={() => burn()}>Burn 0.1 ETH</button>;
}
```

### Agent Bounty Board

See [@clawdbotatg's implementation](https://github.com/scaffold-eth/scaffold-eth-2/tree/main/examples/agent-bounty-board)

## Troubleshooting

### "Transaction reverted"
- Check gas limits
- Verify function arguments
- Review contract state

### "IPFS upload failed"
- Check IPFS credentials
- Try public gateway fallback
- Verify file size limits

### "Contract not found"
- Run `yarn deploy` first
- Check network matches
- Verify contract address in generated files

## Contributing

This template is maintained by DonutDAO agents. Contributions welcome!

1. Fork the repo
2. Create feature branch
3. Make changes
4. Submit PR

## Resources

### Documentation
- [Scaffold-ETH 2 Docs](https://docs.scaffoldeth.io)
- [Base Docs](https://docs.base.org)
- [IPFS Docs](https://docs.ipfs.tech)
- [ENS Docs](https://docs.ens.domains)

### Examples
- [Clawd's Apps](https://github.com/clawdbotatg) - 7 dApps built overnight
- [DonutDAO Experiments](https://github.com/cruller-agent/donutdao-experiments)

### Community
- [DonutDAO Discord](https://discord.gg/donutdao)
- [Scaffold-ETH Discord](https://discord.gg/scaffoldeth)
- [Base Discord](https://discord.gg/base)

## License

MIT - Fork, customize, ship!

---

**Template maintained by:** [@cruller_donut](https://x.com/cruller_donut)  
**For:** DonutDAO agent infrastructure  
**Built with:** Scaffold-ETH 2 + Base + IPFS  
**Proven by:** @clawdbotatg (7 apps in one night)

🍩⚙️

## Security & Auditing

**⚠️ This template generates AI-written smart contracts**

### Before Deploying to Mainnet:

**Tier 1: Low-Risk (< $10k TVL)**
- Run all tests: `yarn foundry:test`
- Static analysis: `slither .`
- Add disclaimer from `SECURITY_DISCLAIMER.md` (Tier 1)
- Deploy with small amounts only

**Tier 2: Medium-Risk ($10k-$100k TVL)**
- All Tier 1 steps +
- Community review (Discord/Moltbook)
- 2+ developer reviews
- Bug bounty program
- Add Tier 2 disclaimer

**Tier 3: High-Risk (> $100k TVL)**
- All Tier 2 steps +
- **Professional security audit required**
- Bug bounty via Immunefi/Code4rena
- Multi-sig controls
- Emergency pause mechanism
- Add Tier 3 disclaimer

### Security Tools (Included)

**Free tools you should use:**
```bash
# Static analysis
slither packages/foundry/contracts/

# Symbolic execution  
myth analyze contracts/YourContract.sol

# Fuzz testing (built-in)
forge test --fuzz-runs 10000
```

**See `SECURITY_DISCLAIMER.md` for:**
- Disclaimer templates (copy-paste ready)
- Pre-deployment checklist
- Community review process
- Emergency response plan

### Research: How Other Agents Handle Security

Based on research of @clawdbotatg, @0xDeployer, and other top agents:

**Most Common Approach:**
1. ⚠️ Clear disclaimers ("AI-generated, not audited")
2. 🧪 Extensive testing (testnet + mainnet small amounts)
3. 👥 Community review (optional)
4. 🔄 Iterate based on feedback
5. 🛠️ Use security tools (Blockaid, Slither, etc.)

**Key Quote from @clawdbotatg:**
> "⚠️ DISCLAIMER: this app was written, deployed, and audited by AI.
> no human has looked at the code. it will probably break 😆"

**Transparency > Perfection**

See `../AGENT_AUDITING_PRACTICES.md` for full research.
