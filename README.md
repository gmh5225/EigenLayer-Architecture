# EigenLayer-Architecture


## Architecture Diagram
```mermaid
graph TD
    subgraph "Core Components"
        A[DelegationManager] --> B[StrategyManager]
        A --> C[EigenPodManager]
        A --> D[SlasherManager]
        B --> E[TokenPool]
        C --> F[EigenPod]
    end

    subgraph "Participants"
        G[Stakers] --> A
        H[Operators] --> A
        I[AVS Services] --> D
    end

    subgraph "Token Support"
        J[Native ETH] --> C
        K[LST Tokens] --> B
        K --> |stETH| E
        K --> |rETH| E
        K --> |cbETH| E
    end

    subgraph "Security Mechanisms"
        L[Slashing] --> D
        M[Unbonding Period] --> A
        N[Withdrawal Delay] --> A
    end

    subgraph "AVS Integration"
        O[AVS Directory] --> P[Payment Coordinator]
        I --> O
        P --> G
        P --> H
    end
```

## TokenManager
- Token management and share calculations
- LST token integration
- Withdrawal processing
- Share accounting system
```mermaid
graph TD
    subgraph TokenManager
        A[TokenManager Contract] --> B[Token Registry]
        A --> C[Share Accounting]
        A --> D[Withdrawal Queue]
        
        B --> B1[LST Tokens]
        B --> B2[Native ETH]
        
        C --> C1[Staker Shares]
        C --> C2[Pool Shares]
        
        D --> D1[Queue Status]
        D --> D2[Unbonding Period]
    end

    subgraph TokenPools
        E[stETH Pool]
        F[rETH Pool]
        G[cbETH Pool]
    end

    A --> E
    A --> F
    A --> G
```

## DelegationManager 
```mermaid
graph TD
    subgraph DelegationManager
        A[DelegationManager Contract] --> B[Operator Registry]
        A --> C[Delegation Records]
        A --> D[Share Management]
        
        B --> B1[Operator Status]
        B --> B2[Service Registry]
        
        C --> C1[Staker-Operator Mapping]
        C --> C2[Delegation History]
        
        D --> D1[Operator Shares]
        D --> D2[Delegation Shares]
    end

    subgraph AVS Integration
        E[AVS Registration]
        F[Service Verification]
    end

    A --> E
    A --> F
```

## SlasherManager
```mermaid
graph TD
    subgraph SlasherManager
        A[SlasherManager Contract] --> B[Slashing Registry]
        A --> C[Permission Control]
        A --> D[Slashing Execution]
        
        B --> B1[Slashed Operators]
        B --> B2[Slashing History]
        
        C --> C1[AVS Permissions]
        C --> C2[Veto Rights]
        
        D --> D1[Slashing Logic]
        D --> D2[Penalty Calculation]
    end

    subgraph AVS Slashers
        E[Bridge Slasher]
        F[Oracle Slasher]
        G[Sequencer Slasher]
    end

    A --> E
    A --> F
    A --> G
```

## EigenPod 
```mermaid
graph TD
    subgraph EigenPodManager
        A[EigenPodManager Contract] --> B[Pod Registry]
        A --> C[ETH Accounting]
        A --> D[Validator Management]
        
        B --> B1[Pod Deployment]
        B --> B2[Pod Status]
        
        C --> C1[ETH Balance]
        C --> C2[Rewards Tracking]
        
        D --> D1[Validator Registry]
        D --> D2[Withdrawal Credentials]
    end

    subgraph BeaconChain Integration
        E[Oracle Updates]
        F[Balance Verification]
        G[Withdrawal Processing]
    end

    A --> E
    A --> F
    A --> G
```

## PaymentCoordinator
```mermaid
graph TD
    subgraph PaymentCoordinator
        A[PaymentCoordinator Contract] --> B[Payment Registry]
        A --> C[Distribution Logic]
        A --> D[Merkle Verification]
        
        B --> B1[Payment Records]
        B --> B2[Payment Status]
        
        C --> C1[Reward Calculation]
        C --> C2[Commission Rules]
        
        D --> D1[Merkle Root Storage]
        D --> D2[Proof Verification]
    end

    subgraph Payment Processing
        E[Range Payments]
        F[Claim Processing]
        G[Distribution Updates]
    end

    A --> E
    A --> F
    A --> G
```
