# TheOneEye Ai Team Group Discussion Architecture

---

## System Overview

```mermaid
graph TB
    Human[The Human<br/>Priority Interrupt]
    MainChannel[Main Channel<br/>High-Level Progress]
    BreakoutChannel[Breakout Rooms<br/>Technical Deep-Dives]
    Moderator[The Moderator<br/>The Conductor<br/>Dynamic Orchestrator]
    
    HiddenChannel[Hidden Channel<br/>Interrupt Bids]
    
    Governor[The Governor<br/>Solution Architect<br/>KPI: System Leverage]
    Builder[The Builder<br/>Implementation Engineer<br/>KPI: Execution Correctness]
    Signal[The Signal<br/>Market Strategist<br/>KPI: Speed & Hype]
    Skeptic[The Skeptic<br/>Operational Auditor<br/>KPI: Risk Prevention]
    WatchfulEye[The Watchful Eye<br/>Reliability Operator<br/>KPI: System Health]
    
    Human -->|"Priority Messages"| MainChannel
    MainChannel -->|"All Messages"| Moderator
    BreakoutChannel -->|"Technical Threads"| Moderator
    Moderator -->|"Routes & Controls"| MainChannel
    Moderator -->|"Creates & Manages"| BreakoutChannel
    
    Governor -->|"Bid to Interrupt"| HiddenChannel
    Builder -->|"Bid to Interrupt"| HiddenChannel
    Signal -->|"Bid to Interrupt"| HiddenChannel
    Skeptic -->|"Bid to Interrupt"| HiddenChannel
    WatchfulEye -->|"Bid to Interrupt"| HiddenChannel
    
    HiddenChannel -->|"Priority Bids"| Moderator
    Moderator -->|"Grants Floor"| Governor
    Moderator -->|"Grants Floor"| Builder
    Moderator -->|"Grants Floor"| Signal
    Moderator -->|"Grants Floor"| Skeptic
    Moderator -->|"Grants Floor"| WatchfulEye
    
    Governor -.->|"Teammate Dossier"| Builder
    Governor -.->|"Teammate Dossier"| Signal
    Governor -.->|"Teammate Dossier"| Skeptic
    Governor -.->|"Teammate Dossier"| WatchfulEye
    
    Builder -.->|"Teammate Dossier"| Governor
    Builder -.->|"Teammate Dossier"| Signal
    Builder -.->|"Teammate Dossier"| Skeptic
    Builder -.->|"Teammate Dossier"| WatchfulEye
    
    Signal -.->|"Teammate Dossier"| Governor
    Signal -.->|"Teammate Dossier"| Builder
    Signal -.->|"Teammate Dossier"| Skeptic
    Signal -.->|"Teammate Dossier"| WatchfulEye
    
    Skeptic -.->|"Teammate Dossier"| Governor
    Skeptic -.->|"Teammate Dossier"| Builder
    Skeptic -.->|"Teammate Dossier"| Signal
    Skeptic -.->|"Teammate Dossier"| WatchfulEye
    
    WatchfulEye -.->|"Teammate Dossier"| Governor
    WatchfulEye -.->|"Teammate Dossier"| Builder
    WatchfulEye -.->|"Teammate Dossier"| Signal
    WatchfulEye -.->|"Teammate Dossier"| Skeptic
    
    style Human fill:#ff6b6b
    style Moderator fill:#4ecdc4
    style MainChannel fill:#95e1d3
    style BreakoutChannel fill:#ffeaa7
    style HiddenChannel fill:#dfe6e9
    style Governor fill:#f38181
    style Builder fill:#aa96da
    style Signal fill:#fcbad3
    style Skeptic fill:#ffd93d
    style WatchfulEye fill:#6bcf7f
```

---

## Interrupt Protocol (Dynamic Group Intelligence)

```mermaid
sequenceDiagram
    participant Builder as The Builder
    participant Skeptic as The Skeptic
    participant Moderator as The Moderator
    participant HiddenChannel as Hidden Channel
    participant MainChannel as Main Channel
    
    Note over Builder: Speaking about new feature
    Builder->>MainChannel: "I'll implement cloud-native solution..."
    
    Note over Skeptic: Detects high-risk context
    Skeptic->>Skeptic: Calculate Urgency Score
    Note over Skeptic: Context: Cloud-native<br/>Risk Level: HIGH<br/>Urgency: 0.95
    
    Skeptic->>Skeptic: Calculate Bid Score
    Note over Skeptic: Bid = f(Urgency, Context,<br/>Chaos Level, Floor Openness)
    
    Skeptic->>HiddenChannel: Bid to Interrupt (Score: 0.95)
    HiddenChannel->>Moderator: Priority Bid Received
    
    Moderator->>Moderator: Evaluate Current State
    Note over Moderator: Chaos Level: 0.7<br/>Floor Openness: 0.6<br/>Bid Threshold: Dynamic
    
    alt Bid > Dynamic Threshold
        Moderator->>Builder: Pause Current Statement
        Moderator->>Skeptic: Grant Floor (Critical Objection)
        Skeptic->>MainChannel: "Critical risk: Data sovereignty..."
        Note over Skeptic: Interrupted with high-priority concern
    else Bid < Threshold
        Moderator->>HiddenChannel: Queue Bid (Wait for Turn)
        Note over Moderator: Bid queued for later
    end
```

---

## Dynamic Threshold Calculation

```mermaid
flowchart TD
    Message[Message/Context Arrives] --> VibeAnalysis[Vibe Analysis Layer]
    
    VibeAnalysis --> SentimentCheck{Analyze Sentiment<br/>& Urgency}
    SentimentCheck -->|Frustrated/Urgent| HighChaos[Chaos Level: 0.8-1.0]
    SentimentCheck -->|Neutral/Calm| MediumChaos[Chaos Level: 0.4-0.7]
    SentimentCheck -->|Thinking Out Loud| LowChaos[Chaos Level: 0.0-0.3]
    
    HighChaos --> FloorOpenness1[Floor Openness: 0.3-0.5<br/>Lower Threshold]
    MediumChaos --> FloorOpenness2[Floor Openness: 0.5-0.7<br/>Medium Threshold]
    LowChaos --> FloorOpenness3[Floor Openness: 0.7-0.9<br/>Higher Threshold]
    
    FloorOpenness1 --> AgentBid1[Agent Calculates Bid]
    FloorOpenness2 --> AgentBid2[Agent Calculates Bid]
    FloorOpenness3 --> AgentBid3[Agent Calculates Bid]
    
    AgentBid1 --> BidFormula[Bid = Urgency × Context Relevance<br/>× Role Priority × Chaos Multiplier]
    AgentBid2 --> BidFormula
    AgentBid3 --> BidFormula
    
    BidFormula --> Compare{Bid > Floor Openness?}
    Compare -->|Yes| GrantFloor[Moderator Grants Floor]
    Compare -->|No| QueueBid[Queue Bid for Later]
    
    style HighChaos fill:#ff6b6b
    style MediumChaos fill:#ffd93d
    style LowChaos fill:#6bcf7f
    style GrantFloor fill:#2ecc71
```

---

## Tension Matrix (Conflicting KPIs & Debate Mode)

```mermaid
graph TB
    subgraph KPIs[Conflicting Performance Indicators]
        SignalKPI[The Signal<br/>KPI: Maximize Speed & Market Hype<br/>Goal: Fast Launch, High Visibility]
        SkepticKPI[The Skeptic<br/>KPI: Prevent Failures & Risk<br/>Goal: Thorough Review, Safety First]
        BuilderKPI[The Builder<br/>KPI: Execution Correctness<br/>Goal: Reliable Implementation]
        GovernorKPI[The Governor<br/>KPI: System Leverage & Durability<br/>Goal: Long-term Stability]
    end
    
    Task[Task Arrives] --> SignalResponse[Signal: "Launch in 2 weeks!"]
    Task --> SkepticResponse[Skeptic: "Need 6 weeks for security audit"]
    
    SignalResponse --> Debate[Debate Mode Activated]
    SkepticResponse --> Debate
    
    Debate --> Tension[Tension: Speed vs Safety]
    Tension --> ModeratorSynthesis[Moderator: Synthesize Consensus]
    
    ModeratorSynthesis --> Consensus[Consensus: "4 weeks with<br/>phased security gates"]
    
    Note1[Agents maintain conflicting goals<br/>to create productive friction]
    
    KPIs -.-> Note1
    Consensus -.-> Note1
    
    style SignalKPI fill:#fcbad3
    style SkepticKPI fill:#ffd93d
    style BuilderKPI fill:#aa96da
    style GovernorKPI fill:#f38181
    style Debate fill:#ff6b6b
    style Consensus fill:#2ecc71
```

---

## Breakout Rooms (Sub-Thread Architecture)

```mermaid
sequenceDiagram
    participant Human as The Human
    participant MainChannel as Main Channel
    participant Moderator as The Moderator
    participant Breakout as Breakout Room
    participant Gov as The Governor
    participant Builder as The Builder
    
    Human->>MainChannel: "Design new API integration"
    MainChannel->>Moderator: Task Received
    
    Moderator->>Moderator: Vibe Analysis: Technical Deep-Dive Needed
    
    Moderator->>MainChannel: "Governor and Builder discussing architecture..."
    Note over MainChannel: High-level progress only
    
    Moderator->>Breakout: Create Breakout Thread
    Note over Breakout: Technical Discussion Space
    
    Moderator->>Gov: Activate in Breakout
    Gov->>Breakout: "API schema should use GraphQL..."
    
    Moderator->>Builder: Activate in Breakout
    Builder->>Breakout: "GraphQL adds complexity, REST is simpler..."
    Note over Builder: Aware of Governor's input
    
    Gov->>Breakout: "But GraphQL provides better flexibility..."
    Builder->>Breakout: "Agreed, with caching layer..."
    
    Note over Breakout: Technical details resolved
    
    Breakout->>Moderator: Discussion Complete
    Moderator->>Moderator: Synthesize Breakout Results
    Moderator->>MainChannel: "Architecture decided: GraphQL with caching"
    MainChannel->>Human: Final Decision (Clean Summary)
    
    Note over Human: Sees high-level outcome<br/>not technical debate
```

---

## Vibe Analysis (Sentiment & Urgency Layer)

```mermaid
flowchart TD
    Message[Human Message Arrives] --> VibeAnalysis[Vibe Analysis Engine]
    
    VibeAnalysis --> SentimentAnalysis[Sentiment Detection]
    VibeAnalysis --> UrgencyAnalysis[Urgency Detection]
    VibeAnalysis --> ContextAnalysis[Context Analysis]
    
    SentimentAnalysis --> SentimentType{Sentiment Type}
    SentimentType -->|Frustrated| FrustratedVibe[Vibe: Frustrated<br/>Action: Reassurance First]
    SentimentType -->|Excited| ExcitedVibe[Vibe: Excited<br/>Action: Enthusiastic Response]
    SentimentType -->|Neutral| NeutralVibe[Vibe: Neutral<br/>Action: Standard Flow]
    SentimentType -->|Concerned| ConcernedVibe[Vibe: Concerned<br/>Action: Address Concerns]
    
    UrgencyAnalysis --> UrgencyLevel{Urgency Level}
    UrgencyLevel -->|High| HighUrgency[Urgency: High<br/>Lower Interrupt Threshold]
    UrgencyLevel -->|Medium| MediumUrgency[Urgency: Medium<br/>Standard Threshold]
    UrgencyLevel -->|Low| LowUrgency[Urgency: Low<br/>Higher Threshold]
    
    FrustratedVibe --> RouteDecision[Routing Decision]
    ExcitedVibe --> RouteDecision
    NeutralVibe --> RouteDecision
    ConcernedVibe --> RouteDecision
    
    HighUrgency --> RouteDecision
    MediumUrgency --> RouteDecision
    LowUrgency --> RouteDecision
    
    ContextAnalysis --> RouteDecision
    
    RouteDecision --> AgentSelection{Select Agent}
    AgentSelection -->|Frustrated + Strategic| GovernorFirst[Governor: Reassurance]
    AgentSelection -->|Excited + Market| SignalFirst[Signal: Amplify Enthusiasm]
    AgentSelection -->|Concerned + Technical| BuilderFirst[Builder: Address Issue]
    AgentSelection -->|High Urgency + Risk| SkepticFirst[Skeptic: Risk Assessment]
    
    GovernorFirst --> PersonalityLayer[Apply Personality Layer]
    SignalFirst --> PersonalityLayer
    BuilderFirst --> PersonalityLayer
    SkepticFirst --> PersonalityLayer
    
    PersonalityLayer --> Response[Humanized Response]
    
    Note1[Personality Examples:<br/>Builder: Brief & Pragmatic<br/>Signal: Enthusiastic & Visionary<br/>Skeptic: Cautious & Analytical]
    
    PersonalityLayer -.-> Note1
    
    style FrustratedVibe fill:#ff6b6b
    style ExcitedVibe fill:#6bcf7f
    style HighUrgency fill:#ff6b6b
    style LowUrgency fill:#95a5a6
    style Response fill:#2ecc71
```

---

## Teammate Dossier (Relationship Awareness)

```mermaid
graph LR
    subgraph BuilderDossier[Builder's Internal Dossier]
        Builder[The Builder]
        BuilderNote1["Skeptic: Always concerned<br/>about data sovereignty"]
        BuilderNote2["Governor: Prefers<br/>long-term solutions"]
        BuilderNote3["Signal: Pushes for<br/>speed over perfection"]
    end
    
    Builder -->|"Proposing Cloud Solution"| Anticipation[Anticipation Logic]
    Anticipation -->|"Knows Skeptic's concerns"| ProactiveResponse[Proactive Response]
    
    ProactiveResponse -->|"Addresses data sovereignty<br/>in first message"| MainChannel[Main Channel]
    
    Note1[Builder anticipates Skeptic's objection<br/>and addresses it proactively]
    
    BuilderDossier -.-> Note1
    ProactiveResponse -.-> Note1
    
    style Builder fill:#aa96da
    style BuilderNote1 fill:#ffd93d
    style BuilderNote2 fill:#f38181
    style BuilderNote3 fill:#fcbad3
    style ProactiveResponse fill:#2ecc71
```

---

## Moderator's Debate Encouragement (Active Challenge Promotion)

```mermaid
sequenceDiagram
    participant Builder as The Builder
    participant Moderator as The Moderator
    participant Skeptic as The Skeptic
    participant MainChannel as Main Channel
    
    Builder->>MainChannel: "Quick hack: Use direct DB access for speed"
    
    Note over Moderator: Detects Potential Standards Violation
    Moderator->>Moderator: Analyze Against TheOneEye Standards
    Note over Moderator: Direct DB access violates<br/>reliability standards
    
    Moderator->>Moderator: Lower Skeptic's Interrupt Threshold
    Note over Moderator: Risk Context Detected<br/>Threshold: 0.3 (Low)<br/>Normal: 0.7
    
    Moderator->>Skeptic: Actively Prompt Challenge
    Note over Moderator: "Skeptic, does this approach<br/>meet our reliability standards?"
    
    Skeptic->>Skeptic: Calculate Bid (Now Lower Threshold)
    Note over Skeptic: Bid: 0.95 > Threshold: 0.3
    
    Skeptic->>MainChannel: "This violates TheOneEye reliability standards.<br/>Direct DB access creates single point of failure."
    
    Moderator->>Moderator: Encourage Counter-Response
    Note over Moderator: Debate Mode Active
    
    Builder->>MainChannel: "But we need speed for this feature..."
    
    Skeptic->>MainChannel: "Speed without reliability defeats our purpose.<br/>Use connection pooling with circuit breaker."
    
    Moderator->>Moderator: Synthesize Consensus
    Moderator->>MainChannel: "Consensus: Connection pooling with<br/>circuit breaker maintains speed + reliability"
    
    Note over Moderator: Moderator actively ensures<br/>standards are challenged, not just allowed
```

---

## Active Challenge Mechanism

```mermaid
flowchart TD
    Proposal[Agent Makes Proposal] --> ModeratorCheck[Moderator: Check Against Standards]
    
    ModeratorCheck --> StandardsViolation{Standards<br/>Violation Detected?}
    
    StandardsViolation -->|Yes| LowerThreshold[Lower Challenge Threshold]
    StandardsViolation -->|No| CheckAgreement{All Agents<br/>Agreeing?}
    
    LowerThreshold --> IdentifyChallenger[Identify Appropriate Challenger]
    IdentifyChallenger --> ActivePrompt[Actively Prompt Challenge]
    ActivePrompt -->|"Skeptic, does this meet<br/>reliability standards?"| ChallengeIssued[Challenge Issued]
    
    CheckAgreement -->|Yes - Suspicious| EncourageDissent[Encourage Dissent]
    CheckAgreement -->|No - Healthy Debate| MonitorDebate[Monitor Debate]
    
    EncourageDissent -->|"Governor, any architectural concerns?"| LowerThreshold
    EncourageDissent -->|"Skeptic, any risk concerns?"| LowerThreshold
    EncourageDissent -->|"Watchful Eye, operational impact?"| LowerThreshold
    
    ChallengeIssued --> DebateMode[Debate Mode Active]
    MonitorDebate --> DebateMode
    
    DebateMode --> CollectViews[Collect Conflicting Views]
    CollectViews --> Synthesize[Moderator: Synthesize Consensus]
    Synthesize --> FinalDecision[Final Decision with Standards Enforced]
    
    Note1[Key Principle: Agreement is suspicious.<br/>Healthy teams challenge each other.]
    
    StandardsViolation -.-> Note1
    CheckAgreement -.-> Note1
    
    style StandardsViolation fill:#ff6b6b
    style LowerThreshold fill:#f39c12
    style ActivePrompt fill:#9b59b6
    style EncourageDissent fill:#e74c3c
    style DebateMode fill:#e74c3c
    style FinalDecision fill:#2ecc71
```

---

## Standards Enforcement & Threshold Manipulation

```mermaid
graph TB
    subgraph Standards[TheOneEye Standards]
        Reliability[Reliability Standards<br/>No Single Points of Failure]
        Security[Security Standards<br/>Data Sovereignty Required]
        Scalability[Scalability Standards<br/>Must Handle Growth]
        Maintainability[Maintainability Standards<br/>Code Must Be Auditable]
    end
    
    Proposal[Agent Proposal] --> CheckStandards[Moderator Checks Standards]
    
    CheckStandards --> ViolationType{Type of Violation?}
    
    ViolationType -->|Reliability Risk| SkepticThreshold[Skeptic Threshold: 0.3<br/>Normal: 0.7]
    ViolationType -->|Security Risk| SkepticThreshold2[Skeptic Threshold: 0.2<br/>Normal: 0.7]
    ViolationType -->|Architecture Risk| GovernorThreshold[Governor Threshold: 0.4<br/>Normal: 0.7]
    ViolationType -->|Operational Risk| WatchfulEyeThreshold[Watchful Eye Threshold: 0.3<br/>Normal: 0.7]
    
    SkepticThreshold --> ActiveChallenge1[Actively Prompt Skeptic]
    SkepticThreshold2 --> ActiveChallenge1
    GovernorThreshold --> ActiveChallenge2[Actively Prompt Governor]
    WatchfulEyeThreshold --> ActiveChallenge3[Actively Prompt Watchful Eye]
    
    ActiveChallenge1 --> ChallengeIssued[Challenge Must Be Issued]
    ActiveChallenge2 --> ChallengeIssued
    ActiveChallenge3 --> ChallengeIssued
    
    ChallengeIssued --> StandardsEnforced[Standards Enforced Through Debate]
    
    Note1[Moderator doesn't just allow challenges<br/>- Moderator actively ensures they happen]
    
    Standards -.-> Note1
    ChallengeIssued -.-> Note1
    
    style ViolationType fill:#ff6b6b
    style SkepticThreshold fill:#ffd93d
    style GovernorThreshold fill:#f38181
    style WatchfulEyeThreshold fill:#6bcf7f
    style ChallengeIssued fill:#e74c3c
    style StandardsEnforced fill:#2ecc71
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

## Moderator Decision Flow (Enhanced with Vibe & Interrupts)

```mermaid
flowchart TD
    Start([Message Received]) --> CheckInterrupts{Any Interrupt<br/>Bids Pending?}
    
    CheckInterrupts -->|Yes| EvaluateBids[Evaluate Interrupt Bids]
    CheckInterrupts -->|No| IsHuman{Is Human<br/>Message?}
    
    EvaluateBids --> BidThreshold{Bid > Dynamic<br/>Threshold?}
    BidThreshold -->|Yes| GrantInterrupt[Grant Floor to Bidder]
    BidThreshold -->|No| QueueBid[Queue Bid]
    QueueBid --> IsHuman
    GrantInterrupt --> End([End])
    
    IsHuman -->|Yes| VibeAnalysis[Vibe Analysis Layer]
    IsHuman -->|No| ClassifyIntent[Classify Intent]
    
    VibeAnalysis --> SentimentCheck{Sentiment &<br/>Urgency?}
    SentimentCheck -->|Frustrated| FrustratedRoute[Route to Governor<br/>for Reassurance]
    SentimentCheck -->|Excited| ExcitedRoute[Route to Signal<br/>for Amplification]
    SentimentCheck -->|Concerned| ConcernedRoute[Route to Builder/Skeptic<br/>for Resolution]
    SentimentCheck -->|Neutral| HumanPriority[Standard Priority Processing]
    
    FrustratedRoute --> PauseCheck
    ExcitedRoute --> PauseCheck
    ConcernedRoute --> PauseCheck
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
    ValueCheck -->|Yes| CheckBreakout{Needs Technical<br/>Deep-Dive?}
    
    CheckBreakout -->|Yes| CreateBreakout[Create Breakout Room]
    CheckBreakout -->|No| CheckMultiple{Multiple Domains<br/>Required?}
    
    CreateBreakout --> BreakoutActivate[Activate in Breakout]
    BreakoutActivate --> MonitorBreakout[Monitor Breakout Progress]
    MonitorBreakout --> SynthesizeBreakout[Synthesize Results]
    SynthesizeBreakout --> MainChannel[Report to Main Channel]
    MainChannel --> End
    
    CheckMultiple -->|Yes| MultiActivate[Activate Multiple Members<br/>Enable Debate Mode]
    CheckMultiple -->|No| SingleActivate[Activate Single Member]
    
    MultiActivate --> TensionCheck{Conflicting KPIs<br/>Detected?}
    TensionCheck -->|Yes| DebateMode[Enable Debate Mode]
    TensionCheck -->|No| Activate
    DebateMode --> CollectDebate[Collect Conflicting Views]
    CollectDebate --> SynthesizeConsensus[Synthesize Consensus]
    SynthesizeConsensus --> Activate
    
    SingleActivate --> Activate
    NoResponse --> End
    Activate --> End
    
    style HumanPriority fill:#ff6b6b
    style VibeAnalysis fill:#9b59b6
    style NoResponse fill:#95a5a6
    style Activate fill:#2ecc71
    style DebateMode fill:#e74c3c
    style CreateBreakout fill:#f39c12
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

## Task Collaboration Flow (With Debate & Tension)

```mermaid
sequenceDiagram
    participant Human as The Human
    participant MainChannel as Main Channel
    participant Moderator as The Moderator
    participant Gov as The Governor
    participant Builder as The Builder
    participant Skeptic as The Skeptic
    participant Signal as The Signal
    
    Human->>MainChannel: Task Request
    MainChannel->>Moderator: Receive Task
    
    Moderator->>Moderator: Vibe Analysis + Context Analysis
    Moderator->>Moderator: Determine Collaboration Sequence
    
    Moderator->>Gov: Activate First (Architecture)
    Gov->>MainChannel: Architecture Design
    Note over Gov: Aware of all team members<br/>Teammate Dossier active
    
    MainChannel->>Moderator: Governor Response
    
    Moderator->>Signal: Activate Second (Market Perspective)
    Signal->>MainChannel: "We can launch in 2 weeks!"
    Note over Signal: KPI: Speed & Hype
    
    MainChannel->>Skeptic: Skeptic Detects Tension
    Skeptic->>Skeptic: Calculate Interrupt Bid
    Note over Skeptic: High Risk Context<br/>Bid Score: 0.92
    
    Skeptic->>Moderator: Bid to Interrupt (Hidden Channel)
    Moderator->>Signal: Pause
    Moderator->>Skeptic: Grant Floor
    Skeptic->>MainChannel: "Need 6 weeks for security audit!"
    Note over Skeptic: KPI: Risk Prevention<br/>Conflicting with Signal
    
    MainChannel->>Moderator: Tension Detected
    
    Note over Moderator: Debate Mode Activated
    
    Signal->>MainChannel: "But market window closes in 3 weeks!"
    Skeptic->>MainChannel: "Security breach costs more than delay!"
    
    Moderator->>Builder: Activate (Implementation Reality Check)
    Builder->>MainChannel: "Can do phased rollout: 4 weeks"
    Note over Builder: Addresses both concerns<br/>Uses Teammate Dossier knowledge
    
    MainChannel->>Moderator: All Perspectives Collected
    
    Moderator->>Moderator: Synthesize Consensus (Not Just Merge)
    Note over Moderator: Creates solution that<br/>addresses conflicting KPIs
    
    Moderator->>MainChannel: "Consensus: 4-week phased launch<br/>with security gates at weeks 2 & 3"
    MainChannel->>Human: Deliver Synthesized Consensus
    
    Note over Gov,Signal: Debate creates better solutions<br/>through productive friction
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

1. **Dual Channel Architecture**: 
   - **Main Channel**: High-level progress visible to Human
   - **Breakout Rooms**: Technical deep-dives hidden from Human until synthesis
2. **Moderator Authority**: The Moderator has exclusive control over who speaks and when, but supports dynamic interrupts
3. **Full Team Awareness**: Every team member maintains awareness of all other members' roles, expertise, and current involvement
4. **Teammate Dossiers**: Each member maintains relationship awareness (who agrees/disagrees with what, common concerns)
5. **Human Priority**: Human messages interrupt normal flow with immediate priority processing
6. **Context-Dependent Routing**: Moderator determines response sequence based on message context, domain, and vibe
7. **Collaborative Tasks**: System supports both single-member and multi-member task collaboration with debate mode

### Humanization Features

#### 1. Interrupt Protocol (Dynamic Group Intelligence)
- **Hidden Channel**: Agents can bid to interrupt via hidden channel
- **Dynamic Thresholds**: 
  - **Chaos Level (0.0-1.0)**: Urgency/complexity of current topic
  - **Floor Openness (0.0-1.0)**: How much silence is preferred
  - **Bid Calculation**: `Bid = Urgency × Context Relevance × Role Priority × Chaos Multiplier`
- **Priority Scoring**: Agents calculate their own urgency to interrupt based on context
- **Threshold Adjustment**: Lower thresholds when Human is frustrated/urgent, higher when thinking out loud

#### 2. Tension Matrix (Conflicting KPIs)
- **Agent KPIs**:
  - **The Signal**: Maximize speed & market hype
  - **The Skeptic**: Prevent failures & risk
  - **The Builder**: Execution correctness
  - **The Governor**: System leverage & durability
- **Debate Mode**: When conflicting KPIs detected, enable debate rather than smooth handoff
- **Consensus Synthesis**: Moderator synthesizes conflicting views into consensus, not just merging responses

#### 3. Breakout Rooms (Sub-Thread Architecture)
- **Automatic Creation**: Moderator creates breakout rooms for technical deep-dives
- **Context Isolation**: Technical discussions happen in breakout, main channel shows high-level progress
- **Synthesis & Reporting**: Breakout results synthesized and reported to main channel
- **Human Experience**: Human sees clean summaries, not technical debates

#### 4. Vibe Analysis (Sentiment & Urgency Layer)
- **Sentiment Detection**: Analyze Human's emotional state (frustrated, excited, concerned, neutral)
- **Urgency Detection**: Determine urgency level (high, medium, low)
- **Context Analysis**: Combine sentiment + urgency + context for routing decisions
- **Personality Layer**: Each agent has professional persona (Builder: brief & pragmatic, Signal: enthusiastic & visionary)
- **Adaptive Routing**: Frustrated Human → Governor for reassurance, Excited Human → Signal for amplification

#### 5. Active Challenge Encouragement (Social Humanization)
- **Standards Enforcement**: Moderator checks all proposals against TheOneEye standards (reliability, security, scalability, maintainability)
- **Threshold Manipulation**: When standards violations detected, lower challenge thresholds (e.g., 0.3 instead of 0.7) to make challenges easier
- **Proactive Prompting**: Moderator actively asks challengers "Does this meet our standards?" rather than just allowing challenges
- **Agreement Detection**: If all agents agree, Moderator treats this as suspicious and prompts dissenting views
- **Risk-Based Thresholds**: Lower thresholds for high-risk contexts (security: 0.2, reliability: 0.3, architecture: 0.4)
- **Challenge Requirement**: Standards violations must trigger challenges - Moderator ensures this happens

### Moderator Behavior

- **Silence is Valid**: No response when message doesn't require expertise, judgment, or action
- **Default to One**: Activate single member unless multiple domains are unavoidable
- **Priority Handling**: Human messages trigger immediate processing and may pause ongoing tasks
- **Sequence Control**: Moderator determines who speaks first, second, etc., based on context
- **Interrupt Management**: Evaluate interrupt bids against dynamic thresholds
- **Vibe-Aware Routing**: Consider sentiment and urgency in routing decisions
- **Breakout Management**: Create and manage breakout rooms for technical discussions
- **Debate Orchestration**: Enable debate mode when conflicting KPIs detected, synthesize consensus
- **Active Challenge Encouragement**: 
  - **Agreement is Suspicious**: If all agents agree, actively prompt dissenting views
  - **Standards Enforcement**: When proposals violate TheOneEye standards, lower challenge thresholds and actively prompt appropriate challengers
  - **Threshold Manipulation**: Dynamically lower interrupt thresholds (e.g., 0.3 instead of 0.7) when standards violations or risks are detected
  - **Proactive Prompting**: Don't just allow challenges - actively ask "Does this meet our standards?" to ensure challenges happen
  - **Healthy Skepticism**: Encourage agents to challenge each other, especially when quick fixes or shortcuts are proposed

### Team Member Behavior

- **Awareness**: Each member knows all other members and their expertise
- **Teammate Dossiers**: Maintain relationship awareness (e.g., "Skeptic always concerned about data sovereignty")
- **Proactive Anticipation**: Use dossier knowledge to address concerns proactively
- **Interrupt Bidding**: Calculate urgency and bid to interrupt when high-priority concerns detected
- **Orchestration Respect**: Members primarily speak when activated, but can bid to interrupt
- **Collaboration**: Members can reference and build upon each other's contributions
- **Context Preservation**: Members maintain awareness of full conversation context
- **KPI-Driven Responses**: Responses reflect each member's conflicting performance indicators
- **Personality Expression**: Responses reflect professional persona (brief vs. enthusiastic, etc.)

### System Capabilities

- **Task Pausing**: System can pause ongoing tasks to handle human priority messages
- **Task Resumption**: System can resume paused tasks after handling priority
- **Multi-Member Collaboration**: Multiple members can work on single tasks in controlled sequence
- **Debate Mode**: System enables productive friction through conflicting KPIs
- **Consensus Synthesis**: Moderator synthesizes conflicting views into coherent consensus
- **Breakout Room Management**: Create, monitor, and synthesize breakout room discussions
- **Dynamic Threshold Calculation**: Calculate chaos level and floor openness based on context
- **Interrupt Bid Evaluation**: Evaluate and grant/queue interrupt bids dynamically
- **Vibe Analysis**: Analyze sentiment, urgency, and context for intelligent routing
- **Response Synthesis**: Moderator can synthesize multiple member responses into coherent output
- **Active Challenge System**: Moderator actively encourages challenges by lowering thresholds and prompting challengers
- **Standards Enforcement**: System checks proposals against TheOneEye standards and ensures violations trigger challenges
- **Agreement Detection**: System detects when all agents agree and prompts dissenting views
- **Threshold Manipulation**: System dynamically adjusts interrupt thresholds based on risk level and standards violations

## Development Notes

This README defines the **end-state vision** for TheOneEye Team system with **Dynamic Group Intelligence**. All diagrams represent the ideal operational flow that AI agent developers must implement. The system should:

- Enable seamless collaboration between specialized AI agents with **human-like behavior**
- Maintain clear authority and control through the Moderator while supporting **dynamic interrupts**
- Respect human priority while supporting autonomous team operation
- Foster informed collaboration through full team awareness and **teammate dossiers**
- Support complex multi-member task execution with **productive friction** (debate mode)
- Create **breakout rooms** for technical deep-dives while keeping main channel clean
- Analyze **vibe** (sentiment & urgency) for intelligent, context-aware routing
- Enable agents to **bid to interrupt** when high-priority concerns are detected
- Synthesize **consensus** from conflicting viewpoints rather than just merging responses

### Key Humanization Principles

1. **Dynamic Group Intelligence**: Move away from "Machine-in-a-Sequence" to "Dynamic Group Intelligence"
2. **Productive Friction**: Conflicting KPIs create debate and better solutions
3. **Proactive Interruption**: Agents can raise hands when they see critical issues
4. **Context Saturation Prevention**: Breakout rooms keep main channel focused
5. **Theory of Mind**: Vibe analysis enables responses to intent and emotion, not just text
6. **Relationship Awareness**: Teammate dossiers enable proactive anticipation
7. **Active Challenge Encouragement**: **Moderator doesn't just allow challenges - Moderator actively ensures they happen**
   - Agreement is suspicious - healthy teams challenge each other
   - Standards violations must trigger challenges
   - Moderator lowers thresholds and prompts challengers proactively
   - Example: Builder suggests quick hack → Moderator lowers Skeptic's threshold to 0.3 and actively asks "Does this meet our reliability standards?"

### Social Humanization Benchmark

**A truly human-like team doesn't just agree with proposals. The Moderator must:**
- Detect when proposals violate TheOneEye standards
- Actively lower challenge thresholds for appropriate challengers
- Proactively prompt challenges with questions like "Does this meet our standards?"
- Treat unanimous agreement as suspicious and prompt dissenting views
- Ensure that quick fixes and shortcuts are always challenged

**Example Flow:**
1. Builder: "Quick hack: Direct DB access for speed"
2. Moderator: Detects reliability standards violation → Lowers Skeptic threshold to 0.3 → Actively prompts "Skeptic, does this meet our reliability standards?"
3. Skeptic: "This violates TheOneEye reliability standards. Direct DB access creates single point of failure."
4. Debate ensues → Consensus reached with standards enforced

**This is the target architecture. Build to match these specifications.**

