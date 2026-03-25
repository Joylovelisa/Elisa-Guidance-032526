
Technical Specification: SmartMed Review 3.0 (Comprehensive AI Regulatory Toolkit & Agentic Skill Execution System)
Document Control
Document Version: 3.0.0
Date: March 25, 2026
Status: Final / Approved
Prepared For: SmartMed Regulatory Affairs & Development Team
System Name: SmartMed Review 3.0 (智慧醫材審查指引與清單生成系統 - 旗艦升級版)
1. Executive Summary
1.1 Product Vision
SmartMed Review 3.0 represents a paradigm shift in regulatory affairs software. Building upon the success of the 2.0 version, this major upgrade transforms the application from a static generation tool into a fully interactive, multimodal, and agentic Single Page Application (SPA). By leveraging Google's advanced Gemini Large Language Models (including gemini-3-flash-preview and gemini-2.5-flash), the system now ingests raw medical device guidance in multiple formats (Text, Markdown, PDF) and orchestrates the creation of a comprehensive, 2000 to 3000-word Medical Device Review Toolkit.
Crucially, version 3.0 introduces an "Agentic Skill Execution Engine." Users can now dynamically define custom review skills via natural language descriptions, instructing the AI to autonomously execute specialized analytical tasks across the ingested documents. This upgrade fundamentally reduces manual review time, eliminates cognitive overload during document triage, and ensures strict alignment with international regulatory standards, all while granting the user unprecedented control over prompts, LLM model selection, and final output modifications.
1.2 Target Audience
Regulatory Affairs (RA) Specialists: Core users who analyze complex regulatory submissions, draft internal guidelines, and prepare submission dossiers.
Medical Device Reviewers (Government/Notified Bodies): Officials requiring rapid, standardized breakdown of dense regulatory text into actionable checklists.
Quality Assurance (QA) Managers: Personnel responsible for verifying that submissions meet all required standards before formal application.
Clinical Evaluation Experts: Specialists who can utilize the custom skill execution feature to run targeted literature or risk analysis against the generated toolkits.
1.3 Key Objectives and Upgrades from 2.0
Multimodal File Ingestion: Seamlessly parse and extract text from pasted content, Markdown files, and complex PDF documents.
Toolkit Generation Baseline: Automatically generate a 2000-3000 word comprehensive Review Toolkit combining both Guidance and Checklists, heavily structured around a default clinical orthopedic template.
Granular LLM Configuration: Empower users to modify system prompts and select specific Gemini models (e.g., gemini-2.5-flash, gemini-3-flash-preview) on a per-feature basis to balance speed, cost, and reasoning capability.
Agentic Skill Execution: Introduce a dynamic workflow where users input a "skill description" (e.g., "Analyze biocompatibility exemptions based on ISO 10993-1") and the AI agent executes this specific skill on the loaded document, modifying or annotating the toolkit accordingly.
Bilingual Support: Full support for generating outputs in English or Traditional Chinese, selectable via UI toggles.
Advanced Export & Editing: Integrated Markdown and Plain Text editors with instant visual rendering, alongside universal export capabilities to TXT, MD, and PDF formats.
Retention of Legacy Features: Complete preservation of the original 2.0 modules (Guidance Generator, Submission Triage, Review Report, Telemetry Terminal) and the core "WOW" features (Mermaid Flowcharts, International Mapping, Risk Prediction, Traceability Heatmaps, Q&A Generation, Tone Analysis).
2. System Architecture
2.1 High-Level Architecture Overview
SmartMed Review 3.0 remains a client-side Single Page Application to ensure maximum data privacy. Sensitive regulatory and product data never leaves the user's browser except when transmitted via secure, encrypted API calls directly to the Google Gemini inference endpoints.
The architecture is modularized into distinct functional layers:
Presentation Layer (UI): Built with modern functional components, managing the complex state of user inputs, file uploads, and active editor panes.
File Processing Engine: A dedicated client-side utility layer utilizing Web Workers to parse PDFs without blocking the main UI thread.
State & Configuration Management: A global context provider tracking the user's selected language, theme, per-feature model selections, and custom prompt templates.
Agentic Orchestration Layer: The core enhancement for 3.0. This layer interprets user-defined "skills," wraps them in operational prompts, and sequences API calls to execute these skills against the current document state.
Export & Rendering Engine: Handles the transformation of raw Markdown into user-friendly HTML views, and subsequently into downloadable PDF blobs using client-side rendering libraries.
2.2 Core Architectural Principles
Stateless Security Model: The application relies on volatile memory. Upon browser refresh, all proprietary submission data is wiped.
Asynchronous Streaming: The system utilizes real-time streaming for long-form generations (such as the 3000-word toolkit) to ensure the user perceives immediate progress, managed through robust abort controller patterns for instant cancellation.
Granular Tooling Control: Instead of a monolithic LLM call, the system breaks down generation into discrete steps (e.g., Parsing, Guidance Generation, Skill Execution), allowing the user to select a lightweight model for formatting and a heavyweight model for deep reasoning.
3. Detailed Feature Specifications
3.1 Multimodal Ingestion Module (Upload & Parse)
To accommodate the diverse formats of regulatory guidelines, the system includes a unified dropzone component.
Supported Input Methods: Direct text paste, Markdown file (.md) upload, and Portable Document Format (.pdf) upload.
PDF Processing: When a PDF is uploaded, the system utilizes a client-side parsing library (such as PDF.js). The text layer is extracted page by page. For complex PDFs (e.g., those containing crucial tables), the system leverages Gemini's native multimodal capabilities, passing the file directly to the API (if supported by the selected model, such as Gemini 3.1 Flash) or passing the extracted text payload.
Text Normalization: Extracted text is sanitized, stripping invisible characters and normalizing line breaks to optimize token usage before being fed into the LLM context window.
3.2 Dynamic Prompt & Model Configuration
Unlike rigid legacy systems, SmartMed Review 3.0 introduces a "Settings & Tuning" panel for every major function.
Per-Feature Model Selection: Users can individually assign an LLM to specific tasks. For instance, the user might select gemini-3-flash-preview for the massive 3000-word Toolkit Generation due to its large context window and superior reasoning, while selecting the faster, more cost-effective gemini-2.5-flash for Submission Triage or real-time Skill Execution.
Prompt Override: Every AI feature exposes its base prompt in a collapsible text area. Users can permanently modify these prompts, inject specific organizational terminologies, or adjust the persona (e.g., instructing the AI to act as an EU Notified Body auditor rather than a TFDA reviewer).
3.3 The Medical Device Review Toolkit Generator
This is the flagship feature of version 3.0. Upon ingesting the raw guidance document, the system generates a highly structured, 2000 to 3000-word comprehensive toolkit.
Language Selection: The user explicitly selects either "English" or "Traditional Chinese" prior to generation. The LLM is instructed to strictly adhere to the chosen language, using localized regulatory terminology (e.g., translating "Certificate of Free Sale" to "出產國許可製售證明" appropriately).
Default Template Integration: The prompt strictly enforces the use of a predefined template. To ensure consistency, the LLM is instructed to map the ingested guidance into the following structural format, expanding upon it intelligently to meet the word count requirement with deep analytical insights.
The Default Baseline Template (Injected into the System Prompt):
第一部分：骨外固定器臨床前審查指引 (Review Guidance)
1. 產品規格要求 (Product Specifications)
申請者應提供詳盡之產品資料，以評估其設計之合理性與安全性：
用途說明：詳列臨床適應症、適用對象及預定用途。
組件清單：應包含所有系統組件（如：骨針、連接桿、接合器、夾具等）。
工程圖面：檢附具備關鍵幾何尺寸、公差之主要組件工程圖。
材質證明：所有與人體接觸或具結構功能之材質，應標明符合之國際材質標準（如 ASTM F136, ISO 5832 等）。
等同性比較：與已上市類似品執行規格、設計及材質之列表比較，並針對差異處進評估。
2. 生物相容性評估 (Biocompatibility)
依據產品與人體接觸之性質與時間，進行風險評估：
豁免機制：若採用常用之醫用金屬（如 Ti6Al4V, 316L 不鏽鋼等）且製程未改變，得檢具材質證明申請豁免試驗。
執行標準：依據 ISO 10993 系列標準。重點評估項目包括細胞毒性、敏感試驗、刺激試驗、系統毒性、基因毒性及植入試驗。
3. 滅菌確效 (Sterilization)
無菌標準：無菌包裝產品之無菌保證水準 (Sterility Assurance Level, SAL) 必須符合 10⁻⁶。
滅菌驗證：須依據對應之 ISO 標準（如 17665-1, 11135 或 11137）提供滅菌計畫書與報告。對於非無菌提供之產品，應提供建議之醫事機構滅菌方法。
4. 機械性質評估 (Mechanical Testing)
機械測試應能模擬臨床最壞情況（Worst-case scenario）：
執行標準：建議參考 ASTM F1541。
評估項目：剛性與屈折測量（評估固定器之結構穩定度）、靜態破壞測試（評估裝置在承受過負荷時之極限強度）、疲勞與鬆脫測試（模擬長期使用下之循環負荷，及接合處是否容易產生鬆動）。
5. 特定風險與額外評估 (Special Risks and Additional Evaluations)
針對具備特殊宣稱或設計之產品，應額外提供資料：
脊椎或動態機能：若具備微動或動態機能，應提供相關動態功能測試報告。
MRI 相容性：若宣稱 MRI 安全（MRI Safe）或 MRI 條件（MRI Conditional），須依國際標準提交相關磁共振環境評估報告。
第二部分：查驗登記審查清單 (Review Checklist)
(System will generate a markdown table mapping the above points into a checklist with columns: 審查項目, 審查重點 / 具備文件, 審查結果, 備註說明, culminating in an approval decision block).
The LLM will ingest the user's specific guidance (whether it be for software as a medical device, cardiovascular stents, or IVDs) and adapt this structural methodology to the new domain, ensuring a comprehensive 3000-word output.
3.4 Agentic Skill Execution Engine
This revolutionary feature transitions the system from a passive generator to an active AI assistant. Drawing inspiration from modern skill-creator frameworks, the user can define custom behaviors on the fly.
Skill Description Input: A dedicated UI panel allows the user to write a natural language skill description. For example: "Skill: Regulatory Gap Analyzer. Description: Read the generated toolkit. Cross-reference it against the latest European Union Medical Device Regulation (EU MDR 2017/745) Annex I General Safety and Performance Requirements. Highlight any areas in the toolkit that fall short of MDR requirements and suggest specific additions."
Execution Workflow:
Intent Capture: The system reads the skill description and the current state of the generated toolkit.
Prompt Assembly: The engine constructs an execution prompt, instructing the selected LLM model to adopt the persona defined in the skill and apply the logical steps to the document.
Autonomous Application: The agent executes the skill. The output is not just a separate chat message; the system allows the agent to propose direct edits to the markdown document, append new sections, or generate a supplementary analytical report alongside the main toolkit.
Review and Commit: The user reviews the agent's work in a split-screen view. They can accept the modifications, refine the skill description, and run it again iteratively until the desired outcome is achieved.
3.5 Unified Editor & Multi-Format Export
Understanding that AI generation is a baseline, not an infallible final product, robust editing capabilities are central to the 3.0 specification.
Dual-Pane Editing: Users can toggle between a "Raw View" (for editing raw Markdown syntax or plain text) and a "Rendered View" (where Markdown, including tables and checklists, is visually rendered as HTML). The editor supports real-time synchronization between the views.
Export Pipeline:
TXT Export: Strips complex formatting, downloading a raw UTF-8 text file for legacy system integration.
MD Export: Downloads the complete Markdown file, preserving all formatting, tables, and Mermaid syntax, ideal for GitHub repositories or Notion imports.
PDF Export: Utilizes a client-side rendering engine to convert the rendered HTML view into a paginated, professionally styled PDF document. It ensures that page breaks avoid splitting table rows and that Mermaid diagrams are converted to static SVG/PNG formats prior to PDF generation to ensure visual fidelity.
4. Preservation & Enhancement of Legacy "WOW" Features
All core features from version 2.0 are retained and heavily integrated into the new Toolkit format.
4.1 WOW 1: AI Auto-Mermaid Flowchart Generator
As part of the Review Toolkit generation, the system automatically parses the regulatory hierarchy and embeds Mermaid.js code blocks. This generates an interactive visual flowchart (e.g., mapping Class I, II, and III review pathways, or mapping the system components like anchoring vs. bridging elements). This visual aid is instantly rendered within the Markdown editor.
4.2 WOW 2: Global Standards Cross-Referencer
Integrated into the skill engine or prompt baseline, this feature scans local regulatory text and automatically maps it to international equivalents. For instance, if the uploaded PDF is a TFDA standard, the system automatically appends a section mapping these requirements to US FDA Product Codes (e.g., KTT, JEC) and EU MDR classifications, ensuring the toolkit is globally relevant.
4.3 WOW 3: Mock Review Risk Predictor
The AI simulates a "Strict Senior Reviewer." It appends a section to the toolkit identifying the "Top 3 Critical Failures" (fatal flaws) most likely to result in a submission rejection for this specific device category. This proactive risk assessment highlights areas where manufacturers frequently provide insufficient data (e.g., inadequate worst-case scenario justification in fatigue testing).
4.4 WOW 4: Regulatory Traceability Heatmap
The toolkit generator outputs a dense Markdown table cross-referencing every checklist item with the exact clause or page number from the uploaded PDF/Guidance. This ensures that every demand made by the reviewer has a traceable, legal foundation.
4.5 WOW 5: Auto-Generated Clarification Q&A
If the agentic skill engine detects ambiguities in the uploaded guidance, or when used during a live submission review, the system drafts 3 to 5 professionally worded clarification questions ready to be sent to the manufacturer or regulatory sponsor.
4.6 WOW 6: Tone & Compliance Analyzer
A final meta-cognitive step where the LLM evaluates its own generated toolkit. It verifies that the document maintains an objective, authoritative regulatory tone, ensuring no subjective biases or non-compliant terminology were introduced during generation.
5. Technology Stack & Component Design
Frontend Framework: React 18 with Vite for high-performance module bundling and concurrent rendering.
Styling: Tailwind CSS for responsive, utility-first design, ensuring seamless transition between Dark and Light viewing modes.
LLM SDK: @google/genai library, directly connecting the client application to Google's infrastructure.
Document Parsing: pdf.js for robust, entirely client-side extraction of text from uploaded PDF files.
Markdown Processing: react-markdown paired with remark-gfm for rendering GitHub Flavored Markdown (tables, task lists) and custom interceptors for rendering Mermaid charts.
Export Utilities: Libraries such as jspdf and html2canvas to manage the conversion of DOM elements into downloadable PDF files without requiring server-side rendering.
6. Telemetry and System Observability
To ensure the user is never left waiting blindly during massive 3000-word generations or complex skill executions, the Telemetry Terminal is expanded.
Real-time Logging: Displays exact milestones: "Parsing PDF...", "Extracting Text...", "Initializing Gemini 3 Flash Preview...", "Generating Section 2: Biocompatibility...", "Executing Skill: Gap Analysis...".
Token Metrics: Exposes prompt token count and generation token count to the user, providing transparency into payload sizes and potential API costs.
Graceful Interruption: The AbortController architecture is maintained. If a skill execution goes off-track or the generated toolkit diverges from the user's intent, clicking "Stop" instantly severs the HTTP stream, halts generation, and preserves the text generated up to that exact millisecond.
7. Security & Compliance Implications
Zero Data Retention: Because the application is a client-side SPA, uploaded PDFs and pasted texts are processed in the browser's volatile memory. When the tab is closed, the data ceases to exist locally.
API Transmission Security: Data sent to the Gemini API is encrypted in transit via standard TLS protocols. Users must be advised on their organization's specific policies regarding sending unredacted, proprietary medical device blueprints to third-party LLM providers.
Cross-Site Scripting (XSS) Mitigation: The Markdown renderer is strictly configured to escape raw HTML tags, neutralizing any malicious script injection vectors that could theoretically be hallucinated by the AI.
8. Performance Optimization Tactics
Generating 3000 words requires sustained network connectivity and UI stability.
Chunked Rendering: The text stream yielded by the Gemini API is debounced slightly before updating the React state. This prevents the browser's rendering engine from being overwhelmed by millisecond-level DOM updates, ensuring smooth scrolling during generation.
Lazy Loading: Heavy dependencies, such as the PDF parsing library and the PDF export engine, are code-split and loaded asynchronously only when the user interacts with those specific features, keeping the initial application load time under one second.
Web Workers for Parsers: Extracting text from a 100-page regulatory PDF is computationally expensive. This process is offloaded to a background Web Worker, ensuring the main thread remains responsive so the user can continue navigating the UI.
9. Future Scalability Road Map
While 3.0 is a massive leap forward, the architecture is designed to accommodate future expansion:
Local LLM Integration: Building abstract interfaces to allow the routing of requests to local, privacy-centric models (like Llama 3 or Gemma) running via WebGPU or local servers for highly classified submissions.
Multi-Agent Workflows: Expanding the Skill Engine into a multi-agent system where a "Generator Agent" writes the toolkit and a separate "Critic Agent" simultaneously reviews it against international standards in a continuous loop before presenting the final draft to the user.
Vector Database (RAG) Hooks: Preparing state management to accept context injected from external enterprise databases, allowing the system to reference historical company submissions automatically.
10. 20 Comprehensive Follow-up Questions for System Enhancement
To ensure SmartMed Review 3.0 meets all operational, security, and user experience requirements, please review and consider the following 20 technical and product-oriented questions prior to the next development phase:
PDF Parsing Fidelity: When handling PDFs that contain complex, multi-column tables or scanned images (rather than native text), should we rely purely on client-side text extraction libraries, or should we pass the raw PDF directly to the Gemini 3.1 multimodal API for superior structural comprehension?
Model Fallback Mechanisms: If a user selects gemini-3.1-pro-preview for a massive document and hits an API rate limit or token threshold, should the system automatically implement a fallback routing to gemini-3-flash-preview, or should it halt and prompt the user?
Skill Execution Memory: When a user executes multiple custom "skills" sequentially on the same document, should the AI possess conversational memory of previous skill outputs within that session, or should each skill execution be treated as an isolated, stateless event?
Template Customization Limits: The system currently injects the orthopedic base template. Should we build a dedicated UI component allowing RA managers to create, save, and manage a library of custom templates (e.g., Software, IVD, Dental) to replace the default orthopedic baseline?
Data Sanitization & PII: Before uploading regulatory texts to the Gemini API, do we need to implement a local, regex-based pre-processing filter to scrub identifiable manufacturer names, proprietary material codes, or patient data (if clinical trials are included)?
Translation Accuracy vs. Speed: For the Traditional Chinese output, should we instruct the LLM to generate directly in Chinese, which might impact reasoning quality, or should we implement a two-pass pipeline where the AI reasons and generates the toolkit in English first, and a secondary agent translates it into localized Traditional Chinese?
Markdown Editor Integration: For the "Raw View" editor, is a standard HTML textarea sufficient, or should we integrate a robust code editor library like Monaco Editor to provide syntax highlighting, line numbers, and search/replace functionality for Markdown?
PDF Export Styling: When exporting the rendered HTML to PDF, do we need to implement custom CSS print media queries to ensure strict adherence to corporate branding guidelines (e.g., specific margins, proprietary fonts, watermark injection)?
Mermaid Diagram Complexity: AI-generated Mermaid code can occasionally contain syntax errors, causing rendering failures. How should the application handle these errors—should it display the raw code, or automatically trigger a hidden LLM retry loop to correct the syntax?
Prompt Version Control: If users are permitted to modify the base prompts for the features, do we need to implement a local version control system (saved in LocalStorage) so they can revert to the factory default prompts if their custom instructions degrade the output quality?
Skill Library Sharing: If a reviewer creates a highly effective "Skill Description" (e.g., a perfect prompt for analyzing MRI compatibility), should there be a mechanism to export and share these skills as JSON configurations with other reviewers on the team?
Token Cost Tracking: Since allowing users to choose models and execute unlimited skills can rapidly consume API quotas, should we implement a client-side token accumulator to display estimated API costs per session to the user?
Checklist State Management: After generating the Markdown checklist, do users need the ability to interact with the checkboxes directly in the UI (checking them off, adding notes) and have those interactive states persist across page reloads, or is static generation sufficient?
Cross-Referencing Accuracy: When the "Global Standards Cross-Referencer" (WOW 2) links a local regulation to an FDA Product Code, should the system be required to provide a confidence score or a direct web link to the FDA database to mitigate the risk of AI hallucination?
Context Window Saturation: If a user uploads a 500-page PDF, it may exceed even Gemini's massive context window. Should we implement a chunking mechanism to summarize the document in parts, or strictly enforce a file size/page limit prior to upload?
Concurrent Generation: During Skill Execution, can the user run two distinct skills simultaneously (e.g., one agent checking Biological Safety, another checking Mechanical Testing), or must the UI enforce a strict, synchronous queue to prevent state conflicts in the editor?
Localization of Regulatory Terms: Traditional Chinese medical device terminology can vary significantly between Taiwan (TFDA) and other regions. Should the language selector include specific regional dialects (e.g., zh-TW for TFDA vs. zh-HK) to ensure precise legal phrasing?
Offline Degradation: If the user loses internet connectivity while modifying the toolkit in the Markdown editor, should the system implement service workers to cache their edits locally, ensuring no manual work is lost during an outage?
Report Pagination Strategy: A 3000-word toolkit will span many pages. In the UI rendered view, should the document be displayed as one continuous infinite scroll, or should we implement artificial pagination (e.g., tabbed navigation per section) to improve readability?
Audit Trail Requirements: For ISO 13485 or FDA 21 CFR Part 11 compliance environments, is there a future requirement to log which LLM model generated which specific paragraph, creating a verifiable audit trail distinguishing human-edited text from AI-generated text in the final downloaded PDF?
