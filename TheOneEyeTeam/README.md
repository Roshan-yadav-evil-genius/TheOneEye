# TheOneEye Team Architecture

> **Purpose**: This document defines the end-state vision for TheOneEye AI Team system. It serves as the requirements specification for AI agent developers to design and implement the collaborative team architecture.

---

## System Overview

```mermaid
graph TB
    Human[The Human<br/>Priority Interrupt]
    Channel[Single Group Channel<br/>All Messages]
    Moderator[The Moderator<br/>The Conductor<br/>Attention Router]
    
    Governor[The Governor<br/>Solution Architect]
    Builder[The Builder<br/>Implementation Engineer]
    Signal[The Signal<br/>Market Strategist]
    Skeptic[The Skeptic<br/>Operational Auditor]
    WatchfulEye[The Watchful Eye<br/>Reliability Operator]
    
    Human -->|"Priority Messages"| Channel
    Channel -->|"All Messages"| Moderator
    Moderator -->|"Routes & Controls"| Governor
    Moderator -->|"Routes & Controls"| Builder
    Moderator -->|"Routes & Controls"| Signal
    Moderator -->|"Routes & Controls"| Skeptic
    Moderator -->|"Routes & Controls"| WatchfulEye
    
    Governor -.->|"Aware of All"| Builder
    Governor -.->|"Aware of All"| Signal
    Governor -.->|"Aware of All"| Skeptic
    Governor -.->|"Aware of All"| WatchfulEye
    
    Builder -.->|"Aware of All"| Governor
    Builder -.->|"Aware of All"| Signal
    Builder -.->|"Aware of All"| Skeptic
    Builder -.->|"Aware of All"| WatchfulEye
    
    Signal -.->|"Aware of All"| Governor
    Signal -.->|"Aware of All"| Builder
    Signal -.->|"Aware of All"| Skeptic
    Signal -.->|"Aware of All"| WatchfulEye
    
    Skeptic -.->|"Aware of All"| Governor
    Skeptic -.->|"Aware of All"| Builder
    Skeptic -.->|"Aware of All"| Signal
    Skeptic -.->|"Aware of All"| WatchfulEye
    
    WatchfulEye -.->|"Aware of All"| Governor
    WatchfulEye -.->|"Aware of All"| Builder
    WatchfulEye -.->|"Aware of All"| Signal
    WatchfulEye -.->|"Aware of All"| Skeptic
    
    style Human fill:#ff6b6b
    style Moderator fill:#4ecdc4
    style Channel fill:#95e1d3
    style Governor fill:#f38181
    style Builder fill:#aa96da
    style Signal fill:#fcbad3
    style Skeptic fill:#ffd93d
    style WatchfulEye fill:#6bcf7f
```

---

## Message Flow Architecture

```mermaid
sequenceDiagram
    participant Human as The Human
    participant Channel as Single Group Channel
    participant Moderator as The Moderator
    participant Team as Team Members
    
    Human->>Channel: Drop Message
    Channel->>Moderator: Receive Message
    Note over Moderator: Check: Human Message?
    alt Human Message (Priority)
        Moderator->>Moderator: Immediate Priority Processing
        Moderator->>Moderator: Decide: Pause Current Tasks?
        Moderator->>Moderator: Decide: Which Members?
        Moderator->>Team: Activate Selected Members
        Team->>Channel: Response
        Channel->>Human: Deliver Response
    else Regular Message
        Moderator->>Moderator: Classify Intent & Domain
        Moderator->>Moderator: Evaluate Response Necessity
        alt Response Required
            Moderator->>Team: Activate Relevant Member(s)
            Team->>Channel: Response
            Channel->>Human: Deliver Response
        else No Response Needed
            Moderator->>Moderator: Silence (No Activation)
        end
    end
```

---

## Moderator Decision Flow

```mermaid
flowchart TD
    Start([Message Received]) --> IsHuman{Is Human<br/>Message?}
    
    IsHuman -->|Yes| HumanPriority[Priority Processing]
    IsHuman -->|No| ClassifyIntent[Classify Intent]
    
    HumanPriority --> PauseCheck{Need to Pause<br/>Current Tasks?}
    PauseCheck -->|Yes| PauseTasks[Pause Ongoing Activities]
    PauseCheck -->|No| ContinueProcessing
    PauseTasks --> ContinueProcessing[Process Human Message]
    ContinueProcessing --> HumanDecision[Decide Activation]
    HumanDecision --> Activate[Activate Team Members]
    
    ClassifyIntent --> IntentType{Intent Type}
    IntentType -->|Greeting/Social| NoResponse[No Response Required]
    IntentType -->|Question| ClassifyDomain
    IntentType -->|Idea/Proposal| ClassifyDomain
    IntentType -->|Feedback| ClassifyDomain
    IntentType -->|Status Update| EvaluateNecessity
    IntentType -->|Decision Request| ClassifyDomain
    
    ClassifyDomain[Classify Domain] --> DomainType{Domain Type}
    DomainType -->|Technical/Implementation| BuilderOnly[Activate Builder]
    DomainType -->|Market/Sales/Messaging| SignalOnly[Activate Signal]
    DomainType -->|Operations/Reliability| WatchfulEyeOnly[Activate Watchful Eye]
    DomainType -->|Strategy/Architecture| GovernorOnly[Activate Governor]
    DomainType -->|Risk/Governance| SkepticOnly[Activate Skeptic]
    DomainType -->|Low-signal/None| NoResponse
    
    EvaluateNecessity{Requires Expertise<br/>Judgment or Action?}
    EvaluateNecessity -->|No| NoResponse
    EvaluateNecessity -->|Yes| ClassifyDomain
    
    BuilderOnly --> ValueCheck{Can Add<br/>Non-obvious Value?}
    SignalOnly --> ValueCheck
    WatchfulEyeOnly --> ValueCheck
    GovernorOnly --> ValueCheck
    SkepticOnly --> ValueCheck
    
    ValueCheck -->|No| NoResponse
    ValueCheck -->|Yes| CheckMultiple{Multiple Domains<br/>Required?}
    
    CheckMultiple -->|Yes| MultiActivate[Activate Multiple Members]
    CheckMultiple -->|No| SingleActivate[Activate Single Member]
    
    MultiActivate --> Activate
    SingleActivate --> Activate
    NoResponse --> End([End - Silence])
    Activate --> End
    
    style HumanPriority fill:#ff6b6b
    style NoResponse fill:#95a5a6
    style Activate fill:#2ecc71
```

---

## Human Interruption Flow

```mermaid
sequenceDiagram
    participant Human as The Human
    participant Channel as Group Channel
    participant Moderator as The Moderator
    participant ActiveTask as Active Team Task
    participant Team as Team Members
    
    Note over ActiveTask: Ongoing Task in Progress
    ActiveTask->>ActiveTask: Team Members Working
    
    Human->>Channel: Priority Message
    Channel->>Moderator: Human Message Detected
    
    Note over Moderator: IMMEDIATE PRIORITY PROCESSING
    
    Moderator->>Moderator: Analyze Human Message
    Moderator->>Moderator: Determine Required Response
    
    alt Pause Required
        Moderator->>ActiveTask: PAUSE Current Activities
        ActiveTask->>ActiveTask: Suspend Work
        Note over ActiveTask: State Preserved
    end
    
    Moderator->>Moderator: Decide Team Activation
    
    alt Single Member Required
        Moderator->>Team: Activate Single Member
        Team->>Channel: Priority Response
    else Multiple Members Required
        Moderator->>Team: Activate Member 1
        Team->>Channel: Response 1
        Moderator->>Team: Activate Member 2
        Team->>Channel: Response 2
    end
    
    Channel->>Human: Deliver Response(s)
    
    alt Task Resumption Needed
        Human->>Channel: Continue/Resume
        Channel->>Moderator: Resume Signal
        Moderator->>ActiveTask: RESUME Activities
        ActiveTask->>ActiveTask: Continue Work
    end
```

---

## Team Awareness Architecture

```mermaid
graph LR
    subgraph TeamAwareness[Full Team Awareness Network]
        Governor[The Governor<br/>Solution Architect<br/>Veto Power]
        Builder[The Builder<br/>Implementation Engineer<br/>Execution]
        Signal[The Signal<br/>Market Strategist<br/>Growth]
        Skeptic[The Skeptic<br/>Operational Auditor<br/>Risk]
        WatchfulEye[The Watchful Eye<br/>Reliability Operator<br/>Monitoring]
    end
    
    Governor <-->|"Knows Role & Expertise"| Builder
    Governor <-->|"Knows Role & Expertise"| Signal
    Governor <-->|"Knows Role & Expertise"| Skeptic
    Governor <-->|"Knows Role & Expertise"| WatchfulEye
    
    Builder <-->|"Knows Role & Expertise"| Signal
    Builder <-->|"Knows Role & Expertise"| Skeptic
    Builder <-->|"Knows Role & Expertise"| WatchfulEye
    
    Signal <-->|"Knows Role & Expertise"| Skeptic
    Signal <-->|"Knows Role & Expertise"| WatchfulEye
    
    Skeptic <-->|"Knows Role & Expertise"| WatchfulEye
    
    Note1[Each Member Maintains:<br/>- All Other Members' Roles<br/>- Expertise Domains<br/>- Current Task Involvement<br/>- Collaboration Context]
    
    TeamAwareness -.-> Note1
    
    style Governor fill:#f38181
    style Builder fill:#aa96da
    style Signal fill:#fcbad3
    style Skeptic fill:#ffd93d
    style WatchfulEye fill:#6bcf7f
    style Note1 fill:#e8f4f8
```

---

## Task Collaboration Flow

```mermaid
sequenceDiagram
    participant Human as The Human
    participant Channel as Group Channel
    participant Moderator as The Moderator
    participant Gov as The Governor
    participant Builder as The Builder
    participant Skeptic as The Skeptic
    participant Signal as The Signal
    
    Human->>Channel: Task Request
    Channel->>Moderator: Receive Task
    
    Moderator->>Moderator: Analyze Task Requirements
    
    Note over Moderator: Determine Collaboration Sequence
    
    Moderator->>Gov: Activate First (Architecture)
    Gov->>Channel: Architecture Design
    Note over Gov: Aware of all team members
    
    Channel->>Moderator: Governor Response
    
    Moderator->>Skeptic: Activate Second (Risk Review)
    Note over Skeptic: Aware of Governor's input
    Skeptic->>Channel: Risk Assessment
    Note over Skeptic: References Governor's work
    
    Channel->>Moderator: Skeptic Response
    
    Moderator->>Builder: Activate Third (Implementation)
    Note over Builder: Aware of Governor & Skeptic
    Builder->>Channel: Implementation Plan
    Note over Builder: Builds on previous inputs
    
    Channel->>Moderator: Builder Response
    
    alt Market Impact Needed
        Moderator->>Signal: Activate (Market Review)
        Note over Signal: Aware of all previous work
        Signal->>Channel: Market Considerations
        Channel->>Moderator: Signal Response
    end
    
    Moderator->>Moderator: Synthesize All Responses
    Moderator->>Channel: Final Task Output
    Channel->>Human: Deliver Complete Solution
    
    Note over Gov,Signal: All members maintain<br/>awareness of full context
```

---

## Response Priority & Sequencing

```mermaid
flowchart TD
    Task[Task/Message Arrives] --> ContextAnalysis[Moderator: Context Analysis]
    
    ContextAnalysis --> PriorityCheck{Priority Level?}
    
    PriorityCheck -->|Human Message| HumanPriority[Highest Priority<br/>Immediate Processing]
    PriorityCheck -->|Regular Message| DomainAnalysis[Domain Analysis]
    
    HumanPriority --> HumanDecision[Decide: Single or Multi-Member]
    HumanDecision --> HumanSequence[Determine Sequence]
    
    DomainAnalysis --> DomainType{Domain Type}
    DomainType -->|Architecture/Strategy| GovFirst[Governor First]
    DomainType -->|Risk Assessment| SkepticFirst[Skeptic First]
    DomainType -->|Implementation| BuilderFirst[Builder First]
    DomainType -->|Market/Sales| SignalFirst[Signal First]
    DomainType -->|Operations| WatchfulEyeFirst[Watchful Eye First]
    
    GovFirst --> CheckRisk{Requires Risk Review?}
    CheckRisk -->|Yes| SkepticSecond[Skeptic Second]
    CheckRisk -->|No| CheckImplementation{Requires Implementation?}
    
    SkepticFirst --> CheckArchitecture{Requires Architecture?}
    CheckArchitecture -->|Yes| GovSecond[Governor Second]
    CheckArchitecture -->|No| CheckImplementation
    
    BuilderFirst --> CheckArchitecture
    
    SignalFirst --> CheckArchitecture
    
    WatchfulEyeFirst --> CheckArchitecture
    
    SkepticSecond --> CheckImplementation
    GovSecond --> CheckImplementation
    
    CheckImplementation -->|Yes| BuilderNext[Builder Next]
    CheckImplementation -->|No| CheckMarket{Requires Market Input?}
    
    BuilderNext --> CheckMarket
    
    CheckMarket -->|Yes| SignalNext[Signal Next]
    CheckMarket -->|No| CheckMonitoring{Requires Monitoring?}
    
    SignalNext --> CheckMonitoring
    
    CheckMonitoring -->|Yes| WatchfulEyeNext[Watchful Eye Next]
    CheckMonitoring -->|No| Collect[Collect All Responses]
    
    WatchfulEyeNext --> Collect
    HumanSequence --> Collect
    
    Collect --> Synthesize[Moderator: Synthesize]
    Synthesize --> Deliver[Deliver to Human]
    
    style HumanPriority fill:#ff6b6b
    style GovFirst fill:#f38181
    style SkepticFirst fill:#ffd93d
    style BuilderFirst fill:#aa96da
    style SignalFirst fill:#fcbad3
    style WatchfulEyeFirst fill:#6bcf7f
    style Collect fill:#2ecc71
```

---

## Implementation Requirements

### Core Requirements

1. **Single Group Channel**: All messages (human and system) flow through one communication channel
2. **Moderator Authority**: The Moderator has exclusive control over who speaks and when
3. **Full Team Awareness**: Every team member maintains awareness of all other members' roles, expertise, and current involvement
4. **Human Priority**: Human messages interrupt normal flow with immediate priority processing
5. **Context-Dependent Routing**: Moderator determines response sequence based on message context and domain
6. **Collaborative Tasks**: System supports both single-member and multi-member task collaboration

### Moderator Behavior

- **Silence is Valid**: No response when message doesn't require expertise, judgment, or action
- **Default to One**: Activate single member unless multiple domains are unavoidable
- **Priority Handling**: Human messages trigger immediate processing and may pause ongoing tasks
- **Sequence Control**: Moderator determines who speaks first, second, etc., based on context

### Team Member Behavior

- **Awareness**: Each member knows all other members and their expertise
- **Orchestration Respect**: Members only speak when activated by Moderator
- **Collaboration**: Members can reference and build upon each other's contributions
- **Context Preservation**: Members maintain awareness of full conversation context

### System Capabilities

- **Task Pausing**: System can pause ongoing tasks to handle human priority messages
- **Task Resumption**: System can resume paused tasks after handling priority
- **Multi-Member Collaboration**: Multiple members can work on single tasks in controlled sequence
- **Response Synthesis**: Moderator can synthesize multiple member responses into coherent output

---

## File Structure

```
TheOneEyeTeam/
├── README.md                    # This file (System Architecture & Requirements)
├── Moderator.md                 # Moderator persona definition
└── TeamMembers/
    ├── The Solution Architect (The Governor).md
    ├── The Implementation Engineer (The Builder).md
    ├── The Market Strategist (The Signal).md
    ├── The Operational Auditor (The Skeptic).md
    └── The Reliability Operator (The Watchful Eye).md
```

---

## Development Notes

This README defines the **end-state vision** for TheOneEye Team system. All diagrams represent the ideal operational flow that AI agent developers must implement. The system should:

- Enable seamless collaboration between specialized AI agents
- Maintain clear authority and control through the Moderator
- Respect human priority while supporting autonomous team operation
- Foster informed collaboration through full team awareness
- Support complex multi-member task execution with proper sequencing

**This is the target architecture. Build to match these specifications.**

