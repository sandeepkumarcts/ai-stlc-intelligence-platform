AI-Powered STLC Intelligence Platform
C4 Context Diagram

1. System Overview
   The AI-Powered STLC Intelligence Platform is an AI-driven test engineering system that transforms natural language software requirementsinto structured, validated, and traceable test assets.

	It supports QA teams by automating:
		Requirement understanding
		Test case generation
		Traceability mapping (RTM)
		Test coverage analysis

The system is designed as a local-first AI platform using open-source LLMs.

2. System Context Diagram
	                    

                         +----------------------+
                         |    QA Engineer       |
                         | (Primary User)       |
                         +----------+-----------+
                                    |
                                    v
+------------------------------------------------------------------+
|        AI-Powered STLC Intelligence Platform                     |
|                                                                  |
|  - Requirement processing                                        |
|  - Multi-agent test generation (LangGraph)                      |
|  - Traceability matrix generation                                |
|  - Coverage analysis                                             |
|  - Test validation & structuring                                 |
+----------------------------+-------------------------------------+
                             |
          +------------------+------------------+
          |                                     |
          v                                     v

+------------------------+           +----------------------------+
|  Jira (Optional)       |           |  Ollama LLM Runtime        |
|  Requirements Source   |           |  (Llama3 / Mistral)        |
+------------------------+           +----------------------------+			

3. External Actors
 3.1 QA Engineer (Primary Actor)
	 - Provides software requirements
     - Reviews generated test cases
     - Validates traceability and coverage output
				
 3.2 Jira (Optional External System)
     Source of user stories and acceptance criteria
     Not part of MVP scope
     Future integration target

3.3 Ollama LLM Runtime (External Dependency)
	- Local inference engine for AI models
	- Provides reasoning and generation capabilities
	- Used for:
		requirement analysis
		test case generation
		test review assistance
		
4. System Responsibilities

	The platform is responsible for:

	- Converting natural language requirements into structured test cases
		Generating multiple test types:
			functional
			negative
			boundary
			integration
	- Maintaining requirement-to-test traceability
	- Evaluating test coverage completeness
	- Ensuring structured and validated outputs		

5. System Boundary Definition
	- Inside the System
	- FastAPI backend
	- LangGraph orchestration engine
	- Requirement processing module
	- Test generation agents
	- Validation layer (Pydantic)
	- Test repository (DB layer)
	

   Outside the System
	- QA Engineer (user)
	- Jira (future external input system)
	- Ollama LLM runtime (external AI dependency)

6. Key Interaction Flow

	QA Engineer
		↓
	Submit Requirement
		↓
	AI Platform (FastAPI)
		↓
	LangGraph Orchestrator
		↓
	Ollama LLM
		↓
	Validated Test Cases
		↓
	Traceability + Coverage Output


7. Assumptions
	- Requirements are provided in natural language
	- LLM outputs may be non-deterministic
	- Local models are sufficient for MVP workloads
	- External integrations (Jira) are optional and future scope

8. Constraints
	- No paid APIs (OpenAI/Claude excluded)
	- Local execution environment only
	- MVP scope only (no enterprise integrations)
	- Limited compute resources assumed (CPU/GPU optional)

	