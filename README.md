# AgenticOps: LLM-Driven DevOps Automation Engine


### Khurram Nazir (München,Germany)
#### Khurram.Deutsch@yahoo.com
##### Initiated: xx.05.2024
##### Presented PoC: 12.10.2025
##### Revised PoC: 16.06.2026
------------------------------
# AgenticOps: LLM-Driven DevOps Automation Engine
A modern, and secured Transformation of classic DevOps Tool (i.e. Ansible/Bash/Terraform and etc.) into AgenticOps. The PoC Project a way from DevOps to AgenticOps (limited to Ansible only).
Its LLM-Driven DevOps Automation Engine, Agentic Proof of Concept (PoC) designed to bridge the gap between human infrastructure requests and autonomous system administration. This multi-agent framework orchestrates natural language processing and standard IT automation tools to securely ingest, parse, validate, generate, and execute system configurations.

---

## Core Capabilities
* **Intelligent Ingestion:** Structural extraction of data models from unstructured case files (e.g., ticket PDFs).
* **Dynamic Code Generation:** On-the-fly generation of syntactically validated infrastructure playbooks.
* **Self-Healing Mechanics:** Autonomous LLM-driven syntax verification and code error correction loops.
* **Decoupled Execution Node:** Standard automation runners providing execution status and real-time outputs.
* **Production-Grade Observability:** Fully structured asynchronous event logger for compliance auditing.

---

## Framework Architecture & Implementation

The repository implements a modern decoupled software architecture consisting of factory abstractions, declarative schemas, and isolated processing nodes.

<img width="538" height="441" alt="image" src="https://github.com/user-attachments/assets/f86a02f1-bd3d-47c4-82f2-21ff3bf8e5ef" />

### 1. Extensible Model Providers (`LLMFactory`)
Implements an absolute factory behavioral pattern to isolate client code from shifting underlying multi-model APIs (Google Gemini and Anthropic Claude). All configurations default to deterministic behavior (`temperature=0`) to ensure reliable infrastructure workflows.

### 2. Strong Declarative Typing (`CaseSchema` & `DevOpsTaskSchemas`)
Ensures strict system reliability by compiling application-wide types under Pydantic models. Custom validators verify system operations against target regex patterns (e.g., matching strict naming rules for incident identifiers) to eliminate runtime drift.

### 3. Agentic Code Processing Core (`CodeGeneratorAgent`)
Transforms standard operational commands into idempotent deployment playbooks. Rather than relying blindly on LLM outputs, the core routes scripts through an automated runtime validation and code verification process.

### 4. Controlled Action Runner (`AnsibleExecutor`)
Translates multi-agent commands into safe infrastructure mutations via isolated wrappers. It structures task payloads, dynamically creates system inventories, handles private key environments securely, and collects standard return arrays.

---

## 🛠 Prerequisites & Installation

### Core Software Stack
* Python 3.10+
* OpenSSH Server & System Administrator rights on host environments
* Ansible Core Engine
* Ticket as PDF (sample attached)
  <img width="836" height="306" alt="image" src="https://github.com/user-attachments/assets/d6e66273-3dd9-4afb-985a-8f0fbda59699" />


### Setup Instructions
Clone the workspace and populate required package versions within your virtual environment:

```bash
git clone https://github.com
cd agenticOps

# Install operational framework dependencies
pip install langchain==0.1.13 langchain-google-genai==3.0.0 langchain-anthropic==1.0.0
pip install pdfplumber==0.11.7 pydantic==2.12.3 structlog==25.4.0 ansible-runner
```

---

## 💻 Sample Project Execution Flow

An execution lifecycle passing a real-world infrastructure request token is tracked below via the console renderer:

```text
======================================================================
DEVOPS AGENTIC-AI COMPLETE WORKFLOW TEST
======================================================================

STEP 1: PDF EXTRACTION
----------------------------------------------------------------------
2026-06-30T08:11:26Z [info] PDF_extractor_initialized       llm_provider=ChatGoogleGenerativeAI max_retries=3
2026-06-30T08:11:31Z [info] RAW_text_parsed_successfully    case_id=TEF_21102025 task_count=1
2026-06-30T08:11:31Z [info] case_validation_passed          case_id=TEF_21102025

EXTRACTION RESULTS
CASE ID: TEF_21102025
DESCRIPTION: Urgent request to create a Linux user on an AWS sandbox Linux machine.
PRIORITY: CRITICAL
ENVIRONMENT: aws
TOTAL TASKS: 1

Task 1:
Action: create_user
Resource: user - kn5155638
Tool: ANSIBLE
Targets: 13.62.52.201

STEP 2: CODE GENERATION
----------------------------------------------------------------------
2026-06-30T08:12:07Z [info] ansible_yaml_corrected_by_llm    corrected_length=984 original_length=976
2026-06-30T08:12:07Z [info] ansible_playbook_generated       lines=31 task_id=1 validation_status=valid

CODE GENERATION RESULTS
✔ Generated 1 code file(s)
TASK 1: playbook_task_1_create_user.yml | Tool: ANSIBLE | Validation: VALID

STEP 3: SAVING RESULTS
----------------------------------------------------------------------
✔ Case-details saved as JSON to: TEF_21102025_extracted.json
✔ Saved yml file to: playbook_task_1_create_user.yml

STEP 4: EXECUTING GENERATED CODE (ANSIBLE)
----------------------------------------------------------------------
Permissions for /content/aws_ubuntu_pem.pem set to 400.
Executing Ansible playbook for Task 1 ...
...
✔ Task 1 executed via Ansible: successful
======================================================================
```

---

## 📈 System Architectural Improvements (Roadmap)

To elevate this PoC into a production enterprise application, the following system refinements should be prioritized:

* **Production-Grade Package Control:** Transition away from loose, unprotected pip installation loops. Implement standard dependency locking engines like `Poetry` or `Pipenv` to separate strict operational parameters from baseline host system packages.
* **Isolated Processing Architecture:** Replace hot script execution hosts with stateless container workers. Moving tasks into ephemeral Docker runtime pools isolates execution side-effects and safeguards private identity keys against prompt-injection security exploits.
* **Declarative Workflow Graph Routing:** Migrate linear retry loops into dedicated structural state flowcharts using platforms like `LangGraph`. Building explicit workflow graphs enables safe parallel execution forks, state recovery check-pointing, and strict human-in-the-loop manual validation approvals before altering remote targets.
