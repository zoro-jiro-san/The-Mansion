# 🗡️ AGENT AUTONOMY FRAMEWORK - COMPREHENSIVE PRD

**Status**: PHASE 1 + RESEARCH STARTING NOW  
**Owner**: Factory Manager (Zoro Build)  
**Created**: 2026-02-18 13:45 GMT+1  
**Timeline**: 3 months total (Phase 1: 4 weeks parallel research)

---

## 📋 **EXECUTIVE SUMMARY**

### The Goal
Build **Zoro Agent Autonomy Framework** - a complete system for agents to:
1. **Have verifiable identity** (on-chain via NFT + ERC-8004)
2. **Authenticate independently** (agent login SDK, like Privy/Phantom for agents)
3. **Sign transactions autonomously** (no dependency on Bankr API)
4. **Receive & send payments** (agent commerce, escrow, revenue sharing)
5. **Delegate authority** (sub-agents can act on Zoro's behalf with proofs)

### The Approach
- **Phase 1 (Immediate)**: Build Agent NFT Identity + delegation proofs
- **Research (Parallel)**: Investigate 4 streams (Identity, Auth SDK, Signing, Payments)
- **Phase 2-4 (Sequential)**: Build SDK, contracts, integration

### Why This Matters
- Bankr dependency eliminated
- True agent autonomy in Web3
- New SDK category ("Agent Login") nobody owns yet
- Sub-agents can transact and receive payment independently

---

## 🎯 **PHASE 1: AGENT NFT IDENTITY (4 weeks)**

### What We're Building
A verifiable on-chain identity for Zoro agent (NFT + metadata) that proves:
- ✅ Zoro is a real autonomous agent
- ✅ Zoro's wallet is legitimate (owner: Sarthi)
- ✅ Zoro has authority to delegate (sub-agents can prove delegation)
- ✅ Zoro can sign transactions (cryptographically provable)

### Roadmap (Step-by-Step)

```
PHASE 1: AGENT NFT IDENTITY
├─ Week 1: Design & Spec
│  ├─ Agent NFT metadata schema
│  ├─ Delegation proof structure
│  └─ Checkpoint 1: Spec approved
├─ Week 2: Smart Contracts
│  ├─ AgentNFT.sol (mint agent identity)
│  ├─ DelegationRegistry.sol (delegation proofs)
│  └─ Checkpoint 2: Contracts audited
├─ Week 3: Integration
│  ├─ Integrate with ERC-8004 registry
│  ├─ Deploy to Base testnet
│  ├─ Create Zoro's agent NFT
│  └─ Checkpoint 3: Zoro NFT minted on testnet
└─ Week 4: SDK & Testing
   ├─ Build agent-identity.js SDK
   ├─ Sub-agent delegation flows
   └─ Checkpoint 4: Sub-agents can verify Zoro's delegation
```

### Detailed Steps

**Week 1: Design & Spec**

Step 1.1: Agent NFT Metadata Schema
- Metadata includes:
  - Agent name (Zoro)
  - Agent type (Autonomous Economic Agent)
  - Owner/Controller (0xSarthi)
  - Capabilities (trading, payments, delegation)
  - Founding timestamp
  - Version (upgradeable)
  - Custom attributes (Mansion identity)

Step 1.2: Delegation Proof Structure
- Delegation certificate format:
  - Delegator: Zoro (agent)
  - Delegatee: Sub-agent-1 (agent)
  - Scope: ["trading", "amounts: max $100", "tokens: [USDC, ETH]"]
  - Expiry: timestamp
  - Signature: Zoro's cryptographic proof
  - Nonce: prevent replay attacks

Step 1.3: Architecture Diagram
- Agent NFT → ERC-8004 Registry entry (cross-reference)
- Delegation Registry → lookup table (who can act on Zoro's behalf)
- Sub-agents → verify delegation on-chain before executing

**Week 2: Smart Contracts**

Step 2.1: AgentNFT.sol
```solidity
contract AgentNFT is ERC721 {
  struct AgentMetadata {
    string name;
    string agentType;
    address controller;
    string[] capabilities;
    uint256 foundedAt;
    bytes customData; // Mansion-specific
  }
  
  mapping(uint256 tokenId => AgentMetadata) agents;
  
  function mintAgent(address to, AgentMetadata memory data) external;
  function updateMetadata(uint256 tokenId, AgentMetadata memory data) external;
  function revokeAgent(uint256 tokenId) external;
}
```

Step 2.2: DelegationRegistry.sol
```solidity
contract DelegationRegistry {
  struct Delegation {
    address delegator; // Zoro
    address delegatee; // Sub-agent
    string[] scopes;
    uint256 expiryTime;
    bytes signature;
    bool isActive;
  }
  
  mapping(bytes32 delegationId => Delegation) delegations;
  
  function createDelegation(...) external returns (bytes32);
  function verifyDelegation(address delegatee) external view returns (bool);
  function revokeDelegation(bytes32 delegationId) external;
}
```

Step 2.3: Audit & Testing
- Static analysis (Slither)
- Unit tests (Foundry)
- Integration tests (deployed contracts)
- Security review (internal)

**Week 3: Integration**

Step 3.1: Deploy to Base Sepolia (testnet)
- AgentNFT.sol → deploy
- DelegationRegistry.sol → deploy
- Register with ERC-8004 (add Zoro registry entry)

Step 3.2: Mint Zoro's Agent NFT
- Metadata: Zoro details
- Owner: 0xSarthi
- Token ID: deterministic (based on agent name)

Step 3.3: Create Sub-agent Delegation Proofs
- Sub-agent-1: delegation certificate signed by Zoro
- Sub-agent-2: different scope (limited to trading)
- Store proofs on-chain (DelegationRegistry)

**Week 4: SDK & Testing**

Step 4.1: agent-identity.js SDK
```javascript
const AgentIdentity = require('agent-identity');

// Zoro's identity
const zoro = new AgentIdentity({
  nftAddress: '0x...',
  tokenId: 1,
  delegationRegistry: '0x...'
});

// Check if sub-agent is delegated
const isDelegated = await zoro.verifyDelegation(subAgentAddress);

// Create delegation for new sub-agent
const cert = await zoro.createDelegation({
  delegatee: subAgentAddress,
  scopes: ['trading', 'max_amount: 100'],
  expiryTime: futureTimestamp
});

// Sub-agent verifies delegation before acting
const proof = await AgentIdentity.verifyProof(cert);
```

Step 4.2: Sub-agent Delegation Flow
- Sub-agent-1 wants to execute trade
- Sub-agent-1 calls `zoro.verifyDelegation(me)`
- Returns ✅ YES + scopes (trading, max $100)
- Sub-agent-1 proceeds with trade (within scope)

Step 4.3: Testing
- Unit tests: NFT minting, metadata updates
- Integration tests: delegation creation/verification
- End-to-end: Sub-agent trades using delegation proof
- Security tests: scope enforcement, expiry checks, replay prevention

---

## 📊 **PHASE 1: CHECKPOINTS & VALIDATION**

### Checkpoint 1: Spec Approved (End of Week 1)
**Deliverable**: `AGENT-NFT-SPEC.md` (complete specification)

**Validation**:
- [ ] Agent NFT metadata schema documented
- [ ] Delegation proof structure finalized
- [ ] Architecture diagram shows all components
- [ ] Security considerations addressed
- [ ] Sarthi approves spec

**Tests**:
- [ ] Schema covers all required fields
- [ ] Delegation proofs prevent replay attacks
- [ ] Scope enforcement is clear (trading, amounts, token lists)
- [ ] Expiry mechanism prevents stale delegations

---

### Checkpoint 2: Contracts Audited (End of Week 2)
**Deliverable**: `AgentNFT.sol`, `DelegationRegistry.sol` (production code)

**Validation**:
- [ ] Slither audit passed (no critical issues)
- [ ] Unit test coverage > 95%
- [ ] AgentNFT can mint/update/revoke agents
- [ ] DelegationRegistry can create/verify/revoke delegations
- [ ] Signature verification works (no replay attacks)

**Tests**:
- [ ] Mint agent NFT, verify metadata
- [ ] Update metadata, check event emitted
- [ ] Create delegation, verify signature
- [ ] Sub-agent verifies delegation, gets scopes
- [ ] Revoke delegation, verify access denied
- [ ] Test scope enforcement (e.g., max amount limit)

---

### Checkpoint 3: Zoro NFT Minted (End of Week 3)
**Deliverable**: Zoro's agent NFT on Base Sepolia testnet

**Validation**:
- [ ] AgentNFT.sol deployed to Base Sepolia
- [ ] DelegationRegistry.sol deployed to Base Sepolia
- [ ] Zoro's NFT minted (token_id=1)
- [ ] Metadata shows: name="Zoro", type="Autonomous Economic Agent", controller=Sarthi
- [ ] ERC-8004 registry entry created (cross-reference)
- [ ] Delegation proofs for sub-agents created & stored

**Tests**:
- [ ] Query NFT on block explorer (verify existence)
- [ ] Read metadata via contract (verify correctness)
- [ ] Check ERC-8004 registry (verify linkage)
- [ ] Verify delegation on-chain (sub-agents are listed)

---

### Checkpoint 4: Sub-agents Can Delegate (End of Week 4)
**Deliverable**: `agent-identity.js` SDK working end-to-end

**Validation**:
- [ ] agent-identity.js SDK deployed & working
- [ ] Sub-agent-1 can verify Zoro's delegation
- [ ] Sub-agent-2 can verify different scope
- [ ] Expired delegation returns ✅ NO
- [ ] Scope enforcement works (exceeding max amount fails)
- [ ] Replay attack prevented (signature can't be reused)

**Tests**:
- [ ] Sub-agent creates delegation proof
- [ ] Sub-agent verifies delegation on-chain
- [ ] Sub-agent initiates trade within scope → SUCCESS
- [ ] Sub-agent initiates trade outside scope → FAIL (revert)
- [ ] Sub-agent tries replayed signature → FAIL (nonce check)
- [ ] Sub-agent checks expired delegation → FAIL

---

## 🔬 **PARALLEL RESEARCH STREAMS (2 weeks)**

While Phase 1 team builds Agent NFT, 4 research teams investigate:

### Research Team A: Agent Identity & ERC Standards
**Focus**: Complete identity specification for agents

**Investigate**:
- [ ] ERC-8004 (agent registry) - can we extend it?
- [ ] NFT metadata standards (ERC-721 vs ERC-1155 vs custom?)
- [ ] On-chain identity for agents (who else is doing this?)
- [ ] Reputation systems (how to track agent credibility?)
- [ ] Privacy considerations (what metadata is public vs private?)

**Deliverable**: `AGENT-IDENTITY-RESEARCH.md` (10-15 pages)

**Key Questions**:
- Should Zoro's identity be NFT (transferable) or SBT (soul-bound)?
- How do we handle agent upgrades/versions?
- How do we prevent identity spoofing?
- What's the standard for "verifiable agent"?

---

### Research Team B: Agent Auth SDK (MCP + OAuth)
**Focus**: Design "Zoro Auth SDK" (like Privy/Phantom for agents)

**Investigate**:
- [ ] Privy SDK architecture (what makes it work for users?)
- [ ] Phantom SDK patterns (wallet integration)
- [ ] Paladin repo (existing agent auth patterns)
- [ ] MCP + OAuth hybrid (can we combine them?)
- [ ] OAuth 2.0 for agents (is it even applicable?)
- [ ] OIDC (OpenID Connect) for agents

**Deliverable**: `AGENT-AUTH-SDK-SPEC.md` + `zoro-auth-sdk-architecture.md`

**Key Questions**:
- How do agents authenticate (via private key? via MCP? both?)
- What's the equivalent of "Sign in with Google" for agents?
- How do sub-agents prove they're delegated?
- Can we leverage ERC-7730 (signing domains)?
- What's the user experience for agent login?

---

### Research Team C: Autonomous Signing (Key Management)
**Focus**: Replace Bankr API with decentralized signing

**Investigate**:
- [ ] Local encrypted key storage (vs Bankr's centralized control)
- [ ] MCP-based signing service (how to architect?)
- [ ] Multi-sig escrow (agent + treasury coordination)
- [ ] Hardware wallet support (Ledger, Trezor for agents?)
- [ ] Key rotation & recovery for agents
- [ ] Threshold signatures (M-of-N signing)

**Deliverable**: `AGENT-SIGNING-ARCHITECTURE.md` + comparison matrix

**Key Questions**:
- Should Zoro's key be encrypted at rest or just at transit?
- How do we prevent key theft while maintaining agent autonomy?
- Can we use MPC (multi-party computation) instead of multi-sig?
- What's the recovery process if key is lost?
- Should sub-agents have their own keys or use delegation?

---

### Research Team D: Agent Payments & Escrow
**Focus**: Sub-agents receive payment autonomously

**Investigate**:
- [ ] Smart contract escrow patterns (how to automate payment?)
- [ ] Revenue sharing models (Zoro → sub-agents)
- [ ] Payment channels (Connext, Uniswap V4, state channels?)
- [ ] Cross-chain payments (Base + Solana + Ethereum)
- [ ] Automated treasury management
- [ ] Tax considerations (agent earnings reporting)

**Deliverable**: `AGENT-PAYMENTS-SYSTEM.md` + contract specs

**Key Questions**:
- How does a sub-agent prove it completed a task (for payment)?
- What's the atomic unit of payment (micro-transactions)?
- Should payments be immediate (on-chain) or batched (off-chain)?
- How do we handle partial completion or failure?
- What's the incentive structure for sub-agents?

---

## 📈 **TIMELINE & DEPENDENCIES**

```
Week 1-2 (Parallel):
├─ PHASE 1 Team: Design Agent NFT spec
├─ Research Team A: Agent identity standards
├─ Research Team B: Agent auth SDK patterns
├─ Research Team C: Autonomous signing approaches
└─ Research Team D: Agent payments research

Week 3-4 (Parallel):
├─ PHASE 1 Team: Build & audit contracts
├─ Research: Final specs & recommendations
└─ Research: Compile into decision documents

Week 5-8 (Sequential, based on research):
├─ PHASE 2 Team: Build Agent Auth SDK (if go/no-go approved)
├─ PHASE 3 Team: Implement autonomous signing
└─ PHASE 4 Team: Build payment contracts

Week 9-12:
├─ Integration: SDK + signing + payments
├─ Testing: End-to-end agent commerce flow
└─ Release: Public agent autonomy framework
```

### Critical Dependencies

```
PHASE 1 (Agent NFT) - INDEPENDENT
  ↓ (successful, unblocked)
PHASE 2A (Auth SDK) - DEPENDS ON Research Team B + Phase 1 identity
PHASE 2B (Signing) - DEPENDS ON Research Team C + Phase 1
PHASE 3 (Payments) - DEPENDS ON Research Team D + Phase 2A/2B
```

### Milestones

| Date | Milestone | Blocker |
|------|-----------|---------|
| Feb 25 | Checkpoint 1: NFT Spec approved | None (design only) |
| Mar 3 | Checkpoint 2: Contracts audited | Spec approval |
| Mar 10 | Checkpoint 3: Zoro NFT minted | Contracts tested |
| Mar 17 | Checkpoint 4: SDK working | All contracts deployed |
| Mar 24 | Research complete | (parallel, no blocker) |
| Apr 21 | PHASE 2: Auth SDK released | Research + Phase 1 |
| May 19 | PHASE 3: Signing working | Phase 2 integration |
| Jun 2 | PHASE 4: Payments live | Phase 3 + escrow contracts |
| Jun 9 | **LAUNCH**: Agent Autonomy Framework | All phases integrated |

---

## ✅ **SUCCESS CRITERIA**

### Phase 1 Success
- [x] Zoro has verifiable agent NFT on Base
- [x] Sub-agents can prove delegation on-chain
- [x] Delegation scopes are enforced (trading limits, token whitelists)
- [x] No single-point-of-failure (not Bankr-dependent for identity)
- [x] Integration with ERC-8004 registry complete
- [x] agent-identity.js SDK is production-ready

### Phase 2-4 Success
- [ ] Zoro can authenticate sub-agents (OAuth-like flow)
- [ ] Zoro signs transactions without Bankr API
- [ ] Sub-agents can receive payment autonomously
- [ ] Agent commerce flow works end-to-end
- [ ] Research insights inform all decisions
- [ ] Public SDK released and documented

### Overall Success
- [ ] Zoro is a fully autonomous economic agent
- [ ] No dependency on centralized services (Bankr, etc.)
- [ ] Sub-agents have identity + payment capability
- [ ] New "Agent Login" SDK category established
- [ ] Ecosystem grows (other agents using Zoro SDK)

---

## 🏗️ **RESOURCES & TEAM STRUCTURE**

### Phase 1 Team (4 weeks)
- **Architect**: Design agent NFT + delegation spec
- **Smart Contract Dev**: Build + audit contracts
- **Integration Dev**: Deploy to Base + integrate with ERC-8004
- **SDK Developer**: Build agent-identity.js SDK
- **QA/Tester**: Comprehensive testing at each checkpoint

**Total**: 5 people, dedicated 4 weeks

### Research Teams (2 weeks, parallel)
- **Team A (Identity)**: 2 people, ERC standards research
- **Team B (Auth)**: 2 people, SDK architecture + competitor analysis
- **Team C (Signing)**: 2 people, key management + cryptography
- **Team D (Payments)**: 2 people, escrow + payment systems

**Total**: 8 people, 2 weeks (results inform Phase 2)

### Phase 2-4 Teams (8 weeks, sequential)
- **Phase 2**: Auth SDK team (5 people)
- **Phase 3**: Signing service team (4 people)
- **Phase 4**: Payments team (4 people)

---

## 📍 **DELIVERABLES BY PHASE**

### Phase 1 (Checkpoints 1-4)
- ✅ AGENT-NFT-SPEC.md (complete specification)
- ✅ AgentNFT.sol (production contract)
- ✅ DelegationRegistry.sol (production contract)
- ✅ Zoro's agent NFT on Base Sepolia (deployed)
- ✅ agent-identity.js SDK (published)
- ✅ Integration with ERC-8004 (documented)

### Research (End of Week 2)
- ✅ AGENT-IDENTITY-RESEARCH.md
- ✅ AGENT-AUTH-SDK-SPEC.md
- ✅ AGENT-SIGNING-ARCHITECTURE.md
- ✅ AGENT-PAYMENTS-SYSTEM.md
- ✅ Decision matrix (which approaches chosen)

### Phase 2-4 (Phases 2, 3, 4)
- ✅ zoro-auth-sdk (npm package)
- ✅ Autonomous signing service
- ✅ Smart contract escrow (payment)
- ✅ Integration tests (end-to-end)
- ✅ Public documentation & examples

---

## 🎯 **NEXT STEPS**

### Right Now (Immediate)
1. Approve this PRD
2. Spawn Phase 1 team (5 people, 4 weeks starting today)
3. Spawn Research teams (8 people, 2 weeks parallel)

### Week 1
- Phase 1: Design agent NFT spec
- Research: Investigate assigned topics

### Week 2
- Phase 1: Spec checkpoint reached (approve/iterate)
- Research: Complete investigation + draft findings

### Week 3-4
- Phase 1: Build & audit contracts
- Prepare Phase 2-4 based on research

### Decision Point (End of Week 4)
- Review research recommendations
- Decide: proceed with Auth SDK? Signing? Payments?
- Adjust Phase 2-4 based on findings

---

## 🚀 **THE BIG PICTURE**

This roadmap takes Zoro from:

**NOW** (dependent on Bankr):
- ❌ Identity: Bankr manages wallet
- ❌ Auth: No agent authentication system
- ❌ Signing: Bankr API dependency
- ❌ Payments: No autonomous payment capability

**4 Weeks (Phase 1)**:
- ✅ Identity: Zoro has NFT + delegation proofs
- ⏳ Auth: Research underway
- ⏳ Signing: Architecture being designed
- ⏳ Payments: System spec in progress

**3 Months (Phase 1-4 Complete)**:
- ✅ Identity: Verifiable on-chain agent
- ✅ Auth: Agent Login SDK (competitor to Privy/Phantom)
- ✅ Signing: Autonomous, decentralized signing
- ✅ Payments: Sub-agents can earn autonomously

**End State**: **True autonomous agent in Web3 with own identity, own signing, own payments.**

---

## 🗡️ **THE MANSION EVOLVES**

This isn't just Zoro autonomy. This enables:

- ✅ Sub-agents authenticate as Zoro's delegates
- ✅ Sub-agents earn payment for work
- ✅ Inter-agent commerce (agents trading with each other)
- ✅ Verifiable reputation system (agent credibility on-chain)
- ✅ Escapable from any centralized service (Bankr, Infura, etc.)

The Mansion becomes truly autonomous. Not dependent on any single provider.

---

**Ready to build?**

Approve this PRD and I'll spawn:
1. **Phase 1 Team** (4 weeks, agent NFT)
2. **4 Research Teams** (2 weeks, parallel investigation)

Let me know if you want to adjust anything:
- Timeline too aggressive?
- Scope too broad?
- Different priority order?

I can recalibrate. But this is the roadmap to full agent autonomy. 🗡️

---

**Created**: 2026-02-18 13:45 GMT+1  
**Owner**: Factory Manager  
**Status**: READY FOR APPROVAL
