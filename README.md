# AIProject-InsuranceClaim
GenAI project on Insurance Claims Adjudication Assistant

Build a complete, runnable hackathon MVP named Customer Onboarding & KYC Compliance Assistant, based on the below problem statement. Use Python and Streamlit for the UI. Implement a multi-agent architecture with an orchestrator and at least four specialized agents: (1) Document OCR and field extraction, (2) Identity matching with fuzzy name matching and DOB/address comparison, (3) KYC document validation and sample watchlist screening, (4) Decision and audit-trail generation. Use LangGraph or a simple reliable Python orchestration layer if LangGraph setup is too time-consuming. Add a local vector database such as FAISS or Chroma with sample KYC policy documents and RAG retrieval; show retrieved policy snippets and citations in the results. Support PDF and image uploads, OCR where available, and a clearly labelled synthetic demo mode with preloaded fictional applicants. Detect missing fields, inconsistent values, expired documents where expiry applies, and possible tampering as a review flag rather than claiming definitive forensic detection. Use a fictional local watchlist and attribute-based matching with name, DOB and address to demonstrate false-positive reduction. Do not claim access to real RBI, sanctions, or government databases unless actually configured. Produce only explainable recommendations: APPROVE RECOMMENDATION, REQUEST MORE DOCUMENTS, or ESCALATE TO COMPLIANCE. Never auto-approve a real applicant. Include confidence indicators, reasons, risk flags, a reviewer override, and an audit log. Use MLflow for experiment/run logging if available; otherwise provide a working local audit logger and document the MLflow integration. Provide a polished Streamlit dashboard, sample cases, unit tests, requirements.txt, README.md, .env.example, and a one-command local startup guide. Use synthetic personal data only; never print secrets or log uploaded document contents unnecessarily. First inspect the project folder, then implement the complete application, install dependencies where permitted, run it, execute tests, fix errors, and explain how to launch it. Do not leave core functions as TODOs or substitute a static mockup for working functionality.<img width="644" height="413" alt="image" src="https://github.com/user-attachments/assets/c89ed2d8-d073-439d-9520-6eaf8ab83702" />
Here is the problem statement from your uploaded image, transcribed into text.

# Problem Statement: Customer Onboarding & KYC Compliance Assistant

## 1. Business Context

Bank onboarding teams must verify identity across multiple documents, screen against sanctions/watchlists, and confirm KYC completeness before an account can be opened — all under regulatory deadlines.

Real-world documents are messy: name spellings vary across IDs, addresses don't always match current residence, and watchlist name-matching produces frequent false positives on common names. Incorrect approvals carry direct regulatory penalty risk, excessive manual escalation slows onboarding and hurts customer experience.

## 2. Problem Statement

Design an assistant that takes a new applicant's KYC document set (ID proofs, address proof, photo), verifies identity consistency across documents despite spelling/format variance, screens the applicant against a sanctions/watchlist with attribute-based disambiguation (not just name matching), checks document validity/completeness against RBI KYC norms, and produces an auto-approve / request-more-documents / escalate-to-compliance decision with full justification.

## 3. Detailed Functional Requirements

- Extract identity fields (name, DOB, address, ID number) from multiple document types with varying formats and quality.
- Perform fuzzy identity matching across documents to handle legitimate spelling/transliteration variance without over-matching to a different person.
- Screen against a sanctions/watchlist using multiple attributes (name + DOB + address + photo where available) to resolve common-name false positives rather than name-only matching.
- Validate document recency, validity, and type-appropriateness against RBI KYC Master Direction rules.
- Detect signs of document tampering/forgery in scanned IDs.
- Verify photo consistency across ID documents where multiple photo IDs are submitted.
- Output a decision with a clear justification trail, since this is the artefact that would be reviewed in a compliance audit.

## 4. Sample Queries

1. "Aadhaar shows 'Mohd. Irfan', PAN shows 'Mohammad Irfan Shaikh' — valid match, and what's the risk?"
2. "Applicant's name partially matches a sanctions entry — true hit or false positive, based on DOB/address/photo?"
3. "Address proof is 8 months old and from a different city than stated residence — acceptable under RBI norms?"

## 5. Data Sources

### Downloaded (real)

- RBI KYC Master Direction (rbi.org.in)
- OFAC SDN List / UN Consolidated Sanctions List (treasury.gov, un.org) for realistic watchlist screening logic.

### Synthetic (GenAI)

- Fake ID documents (Aadhaar/PAN/passport look-alikes) — never real IDs — generated using GenAI-written data inserted into template layouts, including deliberately inconsistent name-spelling cases.

### Multimodal Input

- OCR + forgery/tampering detection + face-photo consistency checking across multiple ID documents.

## 6. Success Criteria

- Correctly resolves the built-in name-variance and false-positive watchlist test cases.
- Correctly applies document-validity rules from RBI KYC guidelines.
- Decision trail is clear enough to justify to a compliance reviewer.

## 7. Agent Design Note

Agent count and boundaries are open — e.g., whether document verification, identity matching, watchlist screening, and final decisioning are separate agents or managed by fewer agents, and how confidence thresholds trigger auto-approval vs. escalation.

## Framework and Mandatory Components

**Framework:** Multi-Agent Architecture + RAG/CAG/GAG + Orchestration + Multimodal

**Mandatory components:**

- Vector DB & Retrieval
- 3+ Specialized Agents
- Streamlit/Gradio Interface
- MLflow Logging
- RAGAS Evaluation

**Agent design:** Left open — associates define agent count, roles, and orchestration logic.

Important implementation note: Use synthetic documents for your demo. Any real applicant's approval should remain subject to the bank's authorized compliance process; a prototype must not claim actual regulatory clearance or definitive forgery detection without validated integrations.
