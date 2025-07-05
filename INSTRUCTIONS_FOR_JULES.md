# Core Platform Bug Bounty Instructions - Jules

## Scope and Objectives

Conduct comprehensive security research on Core Platform/Orchain earning and asset management system. Focus on identifying vulnerabilities that could affect user funds, protocol integrity, or ecosystem security.

## Target Systems

### Smart Contracts

- Core Platform staking contracts
- Asset management protocols
- Cross-chain bridge implementations
- DeFi integration contracts
- Governance and voting mechanisms
- Reward distribution systems

### Infrastructure

- Node implementations
- API endpoints
- Oracle price feeds
- Multi-signature wallet systems
- Key management infrastructure

## Vulnerability Categories

### Critical Severity

- Direct theft of user funds
- Permanent freezing of assets
- Unauthorized minting/burning
- Flash loan attack vectors
- Reentrancy vulnerabilities
- Oracle manipulation attacks

### High Severity

- Temporary freezing of funds
- Privilege escalation
- Unauthorized access to admin functions
- Bypass of security mechanisms
- MEV extraction vulnerabilities
- Cross-chain bridge exploits

### Medium Severity

- Logic errors affecting rewards
- Incorrect fee calculations
- Slippage manipulation
- Governance vote manipulation
- Front-running vulnerabilities
- Gas griefing attacks

## Testing Methodology

### Static Analysis

```
TOOLS:
- Slither for Solidity analysis
- Mythril for symbolic execution
- Semgrep for pattern matching
- Custom rule sets for DeFi patterns

FOCUS_AREAS:
- Access control mechanisms
- Integer overflow/underflow
- Unchecked external calls
- State variable manipulation
- Token approval patterns
```

### Dynamic Testing

```
SETUP:
- Local fork of mainnet
- Isolated testing environment
- Mock oracles and price feeds
- Simulated market conditions

SCENARIOS:
- Flash loan attacks
- Sandwich attacks
- Price manipulation
- Liquidation scenarios
- Edge case transactions
```

### Code Review Targets

```python
# Priority areas for manual review
REVIEW_PRIORITIES = [
    "reward_calculation_logic",
    "asset_transfer_functions", 
    "access_control_modifiers",
    "external_call_patterns",
    "state_update_sequences",
    "emergency_pause_mechanisms"
]
```

## Specific Attack Vectors

### Flash Loan Attacks

- Identify lending pools that can be drained
- Test price manipulation via large trades
- Exploit arbitrage opportunities
- Manipulate collateral ratios

### Reentrancy Patterns

- Check for cross-function reentrancy
- Test read-only reentrancy attacks
- Verify state updates before external calls
- Analyze callback mechanisms

### Oracle Manipulation

- Test price feed dependencies
- Identify single point of failure oracles
- Exploit time-weighted average price (TWAP) delays
- Manipulate liquidity pool prices

### Access Control Issues

- Test role-based permissions
- Verify multi-signature requirements
- Check for privilege escalation paths
- Analyze emergency functions

## Testing Framework

### Environment Setup

```solidity
// Testing template
contract CorePlatformTest {
    function setUp() public {
        // Fork mainnet at specific block
        vm.createFork(MAINNET_RPC_URL, BLOCK_NUMBER);
        
        // Deploy test contracts
        // Initialize with realistic parameters
        // Set up attack scenarios
    }
    
    function testVulnerability() public {
        // Implement specific exploit
        // Measure impact
        // Verify state changes
    }
}
```

### Attack Simulation

```python
# Python script for complex attack scenarios
def simulate_attack():
    # Setup initial conditions
    # Execute attack steps
    # Measure financial impact
    # Document proof of concept
    
    return {
        "funds_at_risk": calculate_funds_at_risk(),
        "attack_complexity": "low|medium|high",
        "prerequisites": list_prerequisites(),
        "impact_description": describe_impact()
    }
```

## Reporting Requirements

### Proof of Concept

- Complete exploit code
- Step-by-step reproduction instructions
- Transaction traces and logs
- Impact assessment with specific dollar amounts
- Mitigation recommendations

### Report Structure

```markdown
# Vulnerability Report

## Summary
Brief description of the vulnerability

## Impact
- Financial impact: $XXX at risk
- Affected users: XXX
- Protocol functions compromised: XXX

## Technical Details
- Root cause analysis
- Code locations
- Attack prerequisites

## Proof of Concept
- Complete exploit code
- Reproduction steps
- Transaction logs

## Mitigation
- Immediate fixes
- Long-term solutions
- Prevention strategies
```

## Research Areas

### Core Platform Specific

- Staking reward calculations
- Asset management logic
- Cross-chain bridge security
- Governance mechanisms
- Fee distribution systems

### DeFi Integration Points

- Liquidity pool interactions
- Yield farming strategies
- Token swap mechanisms
- Collateral management
- Liquidation processes

### Infrastructure Security

- Node consensus mechanisms
- P2P network vulnerabilities
- API security issues
- Database access controls
- Key management systems

## Tools and Resources

### Security Tools

```bash
# Static analysis
slither contracts/
mythril analyze contracts/

# Dynamic testing
forge test --fork-url $MAINNET_RPC
hardhat test --network localhost

# Gas analysis
forge snapshot
hardhat-gas-reporter
```

### Monitoring Setup

```python
# Real-time monitoring for anomalies
def monitor_transactions():
    # Track large transactions
    # Monitor unusual patterns
    # Alert on suspicious activity
    # Log potential exploit attempts
```

## Submission Process

### Initial Validation

1. Verify vulnerability exists on target system
1. Confirm it’s not in known issues/audits
1. Assess actual financial impact
1. Document complete reproduction steps

### Report Submission

1. Submit via encrypted channels
1. Include complete proof of concept
1. Provide impact assessment
1. Suggest mitigation strategies
1. Maintain responsible disclosure timeline

## Success Metrics

### Bug Quality

- Exploitable vulnerabilities found
- Accurate impact assessment
- Clear reproduction steps
- Actionable mitigation advice

### Research Coverage

- Smart contract surface area reviewed
- Integration points tested
- Edge cases explored
- Attack vectors validated

-----

**Critical**: All testing must be performed on local forks or testnets. No mainnet testing permitted. Focus on high-impact vulnerabilities affecting user funds or protocol security.
