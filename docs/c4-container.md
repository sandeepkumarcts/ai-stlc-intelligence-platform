# AI-Powered STLC Intelligence Platform
## C4 Container Diagram

---

# 1. Purpose

This diagram describes the major deployable containers (applications, services, and data stores) that make up the AI-Powered STLC Intelligence Platform and the interactions between them.

The platform automates requirement analysis, test generation, traceability mapping, and coverage assessment using AI-powered workflows.

---

# 2. Container Diagram

```text
┌──────────────────────────────────────────────────────────────┐
│                    QA Engineer / User                        │
└───────────────────────┬──────────────────────────────────────┘
                        │
                        ▼

┌──────────────────────────────────────────────────────────────┐
│                    Streamlit UI (Future)                     │
│--------------------------------------------------------------│
│ Responsibilities                                             │
│ - Requirement submission                                     │
│ - Display generated test cases                               │
│ - View traceability matrix                                   │
│ - View coverage reports                                      │
└───────────────────────┬──────────────────────────────────────┘
                        │ REST API
                        ▼

┌──────────────────────────────────────────────────────────────┐
│                   FastAPI Gateway                            │
│--------------------------------------------------------------│
│ Responsibilities                                             │
│ - API endpoints                                              │
│ - Request validation                                         │
│ - Authentication (future)                                    │
│ - Routing                                                    │
└───────────────────────┬──────────────────────────────────────┘
                        │
                        ▼

┌──────────────────────────────────────────────────────────────┐
│              Test Intelligence Service                       │
│--------------------------------------------------------------│
│ Technology: Python + LangGraph                               │
│                                                              │
│ Responsibilities                                             │
│ - Requirement analysis                                       │
│ - Multi-agent orchestration                                  │
│ - Test generation                                            │
│ - Test review                                                │
│ - Coverage analysis                                          │
└───────────────┬───────────────────────────────┬──────────────┘
                │                               │
                │                               │
                ▼                               ▼

┌──────────────────────────────┐   ┌──────────────────────────┐
│      LLM Gateway Service     │   │ Validation Service       │
│------------------------------│   │--------------------------│
│ Responsibilities             │   │ Responsibilities         │
│ - Model abstraction          │   │ - Schema validation      │
│ - Provider routing           │   │ - Guardrails             │
│ - Retry logic                │   │ - Output verification    │
│ - Fallback strategy          │   │ - Auto-repair workflow   │
└──────────────┬───────────────┘   └──────────────┬───────────┘
               │                                  │
               ▼                                  │

┌──────────────────────────────────────────────────────────────┐
│                 Ollama Runtime (External)                    │
│--------------------------------------------------------------│
│ Models                                                       │
│ - Llama 3                                                    │
│ - Mistral                                                    │
│ - Qwen                                                       │
└──────────────────────────────────────────────────────────────┘
                                                  │
                                                  ▼

┌──────────────────────────────────────────────────────────────┐
│                  Test Repository                             │
│--------------------------------------------------------------│
│ Technology: PostgreSQL / SQLite                              │
│                                                              │
│ Stores                                                       │
│ - Requirements                                               │
│ - Test Cases                                                 │
│ - Traceability Matrix                                        │
│ - Coverage Reports                                           │
└──────────────────────────────────────────────────────────────┘

Future Integrations
───────────────────────────────────────────────────────────────

┌──────────────┐      ┌──────────────┐      ┌──────────────┐
│ Jira         │      │ TestRail     │      │ GitHub CI/CD │
└──────────────┘      └──────────────┘      └──────────────┘
```

---

# 3. Container Responsibilities

## Streamlit UI

Provides the user interface for:
- Requirement submission
- Reviewing generated tests
- Viewing coverage metrics
- Exporting results

## FastAPI Gateway

Acts as the platform entry point.

Responsibilities:
- API exposure
- Request validation
- Service routing
- Future authentication and authorization

## Test Intelligence Service

Core business service.

Contains the LangGraph workflow:

```text
Requirement Agent
        ↓
Test Generation Agent
        ↓
Review Agent
        ↓
Coverage Agent
```

This service owns the STLC intelligence logic.

## LLM Gateway Service

Abstracts AI model providers.

Benefits:
- Provider independence
- Retry handling
- Future support for OpenAI, Claude, Azure OpenAI
- Cost and model management

## Validation Service

Ensures AI-generated outputs meet platform standards.

Responsibilities:
- Pydantic schema validation
- Output quality checks
- Auto-repair prompts
- Guardrail enforcement

## Test Repository

Persistent storage for:
- Requirements
- Generated tests
- RTM mappings
- Coverage reports

---

# 4. External Dependencies

## Ollama Runtime

Provides local AI inference.

Current target models:
- Llama 3
- Mistral
- Qwen

---

# 5. Design Decisions

### Why separate LLM Gateway?

To prevent vendor lock-in and isolate AI provider concerns.

### Why separate Validation Service?

Because LLM outputs are non-deterministic and must be treated as untrusted.

### Why LangGraph?

Provides stateful multi-agent orchestration and workflow management.

### Why FastAPI?

Lightweight, high-performance API framework with strong Python ecosystem support.

---

# 6. Non-Functional Considerations

### Scalability

- FastAPI can scale horizontally
- Test Intelligence Service can be independently scaled

### Maintainability

- Clear separation of concerns
- Replaceable AI providers

### Reliability

- Retry mechanisms
- Validation layer
- Structured output contracts

### Extensibility

Future integrations:
- Jira
- TestRail
- Playwright
- CI/CD pipelines

---

# Architecture Review Verdict

This container design demonstrates:
- Proper separation of concerns
- AI governance thinking
- Enterprise integration readiness
- Vendor abstraction
- Scalable service boundaries

For a portfolio project, this is more than sufficient to support discussions at a Senior QA Architect, Solution Architect, AI Test Architect, or Engineering Manager level.
