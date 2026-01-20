I'll thoroughly analyze the backend to understand its architecture and then provide you with a comprehensive draw.io documentation strategy. Let me start exploring the codebase systematically.

[12 tools called]

Let me continue exploring the core components, Django apps, and actual implementation files:

[12 tools called]

Let me explore a few more critical components:

[3 tools called]

Now I have a comprehensive understanding of the backend architecture. Let me provide you with a detailed **draw.io documentation strategy** that will allow anyone to rebuild this entire system from your diagrams.

---

# 📐 Draw.io Documentation Strategy for TheOneEye Backend

## 📁 File Structure & Naming Convention

Create the following draw.io files, organized by concern:

```
TheOneEye-Diagrams/
├── 01-System-Context.drawio          # High-level system overview
├── 02-Architecture-Layers.drawio     # Django project structure & layers
├── 03-Workflow-Engine.drawio         # Core workflow orchestration
├── 04-Node-System.drawio             # Node hierarchy & lifecycle
├── 05-Execution-System.drawio        # Flow execution (Production/Development/API)
├── 06-Storage-System.drawio          # Redis queues & cache
├── 07-Form-System.drawio             # Form dependency & validation
├── 08-API-Endpoints.drawio           # REST API & WebSocket endpoints
├── 09-Database-Schema.drawio         # Django models & relationships
├── 10-Browser-Session.drawio         # Browser automation subsystem
├── 11-Node-Categories.drawio         # Available node types catalog
└── 12-Data-Flow-Examples.drawio      # End-to-end workflow examples
```

---

## 📄 File-by-File Content Specification

### **01-System-Context.drawio**
**Purpose:** C4 Context diagram - shows the system from a 30,000ft view

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Context` | External actors (Developer, Frontend, Redis, Celery) and their relationships |
| `Container` | API Service container showing major components |
| `Technology-Stack` | Python, Django, DRF, Celery, Redis, Channels, Playwright |

**Key Elements:**
- Developer ↔ REST API / WebSocket
- API Service ↔ Redis (queues, cache)
- API Service ↔ Celery (async tasks)
- Frontend (React) ↔ Backend API

---

### **02-Architecture-Layers.drawio**
**Purpose:** Django project structure and package organization

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Project-Structure` | Directory tree: `backend/`, `apps/`, `core/` |
| `Django-Apps` | All Django apps with responsibilities |
| `Core-Packages` | `core/Node/`, `core/Workflow/`, `core/views/` breakdown |
| `Dependency-Graph` | How apps/modules depend on each other |

**Key Diagrams:**
```
backend/
├── apps/
│   ├── authentication/     → Google OAuth, auth services
│   ├── browsersession/     → Browser automation via WebSocket
│   ├── workflow/           → Main workflow CRUD & execution
│   ├── nodes/              → Node discovery & metadata API
│   ├── contact/            → Contact form/demo requests
│   └── common/             → Shared exceptions, responses
├── core/
│   ├── Node/               → Node system (BaseNode, Forms)
│   ├── Workflow/           → FlowEngine, FlowGraph, Execution
│   └── views/              → Node registry & scanning services
└── theoneeye/              → Django settings, URLs, Celery config
```

---

### **03-Workflow-Engine.drawio**
**Purpose:** The core orchestration system

**Pages:**
| Page Name | Content |
|-----------|---------|
| `FlowEngine-Class` | FlowEngine class with methods and properties |
| `FlowGraph-Structure` | FlowGraph, FlowNode, node_map structure |
| `FlowBuilder` | JSON → FlowGraph transformation |
| `FlowAnalyzer` | Graph traversal operations |
| `Workflow-Loading` | Sequence: JSON → Build → PostProcess → Create Loops |
| `PostProcessors` | QueueMapper, NodeValidator pipeline |

**Key Class Diagram (FlowEngine):**
```
FlowEngine
├── workflow_id: str
├── data_store: DataStore
├── flow_runners: List[FlowRunner]
├── flow_graph: FlowGraph
├── flow_analyzer: FlowAnalyzer
├── flow_builder: FlowBuilder
├── events: WorkflowEventEmitter
├── state_tracker: ExecutionStateTracker
│
├── load_workflow(workflow_json)
├── run_production()
├── run_development_node(node_id, input_data)
├── run_api(input_data, timeout, request_context)
├── create_loop(producer_flow_node)
└── force_shutdown()
```

---

### **04-Node-System.drawio**
**Purpose:** Node type hierarchy, lifecycle, and registration

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Node-Hierarchy` | Class inheritance: BaseNode → ProducerNode, BlockingNode, NonBlockingNode, ConditionalNode |
| `Node-Lifecycle` | State machine: init → setup → run → execute → cleanup |
| `BaseNode-Methods` | All methods: `init()`, `run()`, `execute()`, `populate_form_values()`, etc. |
| `NodeRegistry` | Auto-discovery mechanism from `Node.Nodes` package |
| `NodeConfig-Data` | NodeConfig, NodeOutput, NodeOutputMetaData dataclasses |
| `Jinja-Templates` | Template detection and runtime rendering flow |

**Key Diagrams:**
```
                    BaseNode (ABC)
                         │
         ┌───────────────┼───────────────┐
         │               │               │
    ProducerNode    BlockingNode   NonBlockingNode
         │               │
         │         ConditionalNode
         │
    (QueueReader,   (HttpRequest,   (QueueWriter,
     Webhook)        Transform)      FileWriter)
```

---

### **05-Execution-System.drawio**
**Purpose:** How workflows execute in different modes

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Production-Mode` | FlowRunner loop: Producer → BlockingNodes → NonBlockingNode |
| `Development-Mode` | Direct node execution with cache |
| `API-Mode` | APIFlowRunner: single request-response |
| `FlowRunner-Class` | FlowRunner methods and state machine |
| `PoolExecutor` | ASYNC, THREAD, PROCESS pool selection |
| `Branch-Selection` | ConditionalNode yes/no routing logic |
| `Event-System` | WorkflowEventEmitter, ExecutionStateTracker |

**Production Mode Flow:**
```
FlowEngine
    │
    ├── Creates FlowRunner per ProducerNode
    │
    └── FlowRunner.start()
            │
            ├── _init_nodes() - recursive init
            │
            └── Loop:
                 ├── Execute Producer
                 ├── _process_next_nodes()
                 │       ├── Execute BlockingNode
                 │       ├── If ConditionalNode → follow branch
                 │       └── If NonBlockingNode → continue
                 └── Return to Producer
```

---

### **06-Storage-System.drawio**
**Purpose:** Redis-based storage architecture

**Pages:**
| Page Name | Content |
|-----------|---------|
| `DataStore-Facade` | DataStore as facade to QueueStore, CacheStore |
| `QueueStore` | Redis Lists: LPUSH/BRPOP operations |
| `CacheStore` | Redis Strings: SET/GET/TTL operations |
| `RedisConnection` | Connection lifecycle management |
| `Cross-Loop-Comm` | QueueWriter → Redis → QueueReader flow |
| `Dev-Mode-Cache` | How cache stores node outputs for development |

---

### **07-Form-System.drawio**
**Purpose:** Django form with dependencies and Jinja templates

**Pages:**
| Page Name | Content |
|-----------|---------|
| `BaseForm-Class` | Methods: `update_fields()`, `validate_form()`, `get_form_schema()` |
| `DependencyMetaclass` | How `_field_dependencies` is built |
| `Cascading-Updates` | Parent field change → loader call → child update |
| `Jinja-Rendering` | Template detection → render → validate |
| `FormSchemaBuilder` | JSON schema generation for frontend |
| `Validation-Flow` | Two-phase: pre-execution (template check) → post-render (full) |

---

### **08-API-Endpoints.drawio**
**Purpose:** Complete REST API and WebSocket documentation

**Pages:**
| Page Name | Content |
|-----------|---------|
| `URL-Structure` | All URL patterns with HTTP methods |
| `Workflow-Endpoints` | CRUD, start/stop execution, canvas_data |
| `Node-Endpoints` | Add, update, input/output, position |
| `Execution-Endpoints` | execute_and_save_node, execute (API mode) |
| `WebSocket-Protocol` | Connection flow, event types, message formats |
| `Celery-Integration` | Task endpoints, status checking |

**Key Endpoints Table:**
```
┌────────────────────────────────────────┬────────┬──────────────────────────┐
│ Endpoint                               │ Method │ Purpose                  │
├────────────────────────────────────────┼────────┼──────────────────────────┤
│ /api/workflow/                         │ GET    │ List workflows           │
│ /api/workflow/{id}/                    │ GET    │ Get workflow details     │
│ /api/workflow/{id}/start_execution/    │ GET    │ Start production mode    │
│ /api/workflow/{id}/stop_execution/     │ GET    │ Stop workflow            │
│ /api/workflow/{id}/execute/            │ POST   │ Execute API workflow     │
│ /api/workflow/{id}/execute_and_save_node/│ POST │ Execute single node      │
│ /api/workflow/{id}/canvas_data/        │ GET    │ Get canvas with nodes    │
│ /api/workflow/{id}/nodes/add/          │ POST   │ Add node to workflow     │
│ /ws/workflow/{id}/                     │ WS     │ Real-time execution      │
└────────────────────────────────────────┴────────┴──────────────────────────┘
```

---

### **09-Database-Schema.drawio**
**Purpose:** Django models and their relationships

**Pages:**
| Page Name | Content |
|-----------|---------|
| `ER-Diagram` | Full entity-relationship diagram |
| `WorkFlow-Model` | Fields, choices (workflow_type, status) |
| `Node-Model` | Fields, JSON fields (form_values, config, input/output) |
| `Connection-Model` | source_node, target_node, source_handle |
| `NodeFile-Model` | File storage for nodes |
| `BrowserSession-Model` | Browser session tracking |

**Key Models:**
```
WorkFlow (1) ──── (*) Node
    │                 │
    │                 └── (*) NodeFile
    │
    └──── (*) Connection
              │
              ├── source_node (FK → Node)
              └── target_node (FK → Node)
```

---

### **10-Browser-Session.drawio**
**Purpose:** Browser automation subsystem

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Architecture` | WebSocket consumer → managers → Playwright |
| `Manager-Classes` | BrowserManager, PageManager, NavigationManager, InteractionManager |
| `Event-Handlers` | MouseHandler, KeyboardHandler |
| `Controllers` | MouseController, KeyboardController |
| `Streaming` | ScreenshotStreamer for live view |
| `Message-Flow` | Client → WebSocket → MessageRouter → Managers |

---

### **11-Node-Categories.drawio**
**Purpose:** Catalog of all available node types

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Category-Overview` | All categories with icons |
| `System-Nodes` | QueueReader, QueueWriter, WebhookProducer |
| `Browser-Nodes` | WebPageLoader, SendConnectionRequest |
| `Data-Nodes` | DataTransformer, StringIterator |
| `Logical-Nodes` | IfCondition |
| `GoogleSheets-Nodes` | GetRow, UpdateRow, GetRecordByQuery |
| `Store-Nodes` | FileWriter |
| `Delay-Nodes` | StaticDelay, DynamicDelay |
| `Counter-Nodes` | CounterNode |
| `WebPageParsers` | LinkedinProfileParser |

**Node Structure Pattern:**
```
Node Category/
├── __init__.py
├── _shared/              # Shared utilities
│   └── services/
├── SpecificNode/
│   ├── __init__.py
│   ├── form.py          # BaseForm subclass
│   ├── node.py          # BlockingNode/ProducerNode/etc.
│   └── icon.png
```

---

### **12-Data-Flow-Examples.drawio**
**Purpose:** Complete end-to-end workflow examples

**Pages:**
| Page Name | Content |
|-----------|---------|
| `Simple-Queue-Flow` | QueueReader → Transform → QueueWriter |
| `Conditional-Flow` | Producer → IfCondition → yes/no branches |
| `API-Workflow` | WebhookProducer → Process → Response |
| `Google-Sheets-Flow` | GetRow → Transform → UpdateRow |
| `Browser-Automation` | WebPageLoader → Click → Extract → Save |
| `Cross-Loop-Comm` | Loop1 (QueueWriter) → Redis → Loop2 (QueueReader) |

---

## 🎨 Visual Standards for Draw.io

### Color Coding (avoid light colors per your preference):
| Component Type | Color |
|----------------|-------|
| **ProducerNode** | `#2E7D32` (Dark Green) |
| **BlockingNode** | `#1565C0` (Dark Blue) |
| **NonBlockingNode** | `#7B1FA2` (Dark Purple) |
| **ConditionalNode** | `#F57C00` (Dark Orange) |
| **Redis/Storage** | `#C62828` (Dark Red) |
| **API/HTTP** | `#00838F` (Dark Cyan) |
| **Database** | `#5D4037` (Dark Brown) |
| **Service Layer** | `#424242` (Dark Gray) |

### Shape Standards:
| Element | Shape |
|---------|-------|
| Classes | Rectangle with compartments |
| Processes/Flows | Rounded rectangle |
| Decisions | Diamond |
| Data stores | Cylinder |
| External systems | Cloud |
| Actors | Stick figure |

### Arrow Styles:
| Relationship | Arrow Style |
|--------------|-------------|
| Data flow | Solid arrow |
| Dependency | Dashed arrow |
| Inheritance | Hollow triangle |
| Implementation | Dashed hollow triangle |
| Association | Plain line |

---

## 📋 Per-Page Checklist

For each page, include:
- [ ] **Title** with page name
- [ ] **Legend** explaining colors/shapes used
- [ ] **Class/Component names** exactly matching code
- [ ] **Method signatures** for key methods
- [ ] **Data flow direction** arrows
- [ ] **Notes** for complex logic
- [ ] **Links** to related pages (draw.io page links)

---

## 🔗 Cross-Referencing Strategy

Use draw.io's **page linking** feature to create navigation:
1. Each diagram should have a "Navigate To" section linking related pages
2. Use consistent numbering (01-, 02-, etc.) for logical ordering
3. Create a master index page in `01-System-Context.drawio`

---

This structure ensures that anyone with these 12 draw.io files can understand and rebuild the entire TheOneEye backend system without needing additional documentation. The key is maintaining exact alignment with code (class names, method names, file paths) so the diagrams serve as an accurate blueprint.