SmartMed Review 3.0: Comprehensive Technical Specification
Executive Summary
This document serves as the authoritative technical specification for SmartMed Review 3.0, an advanced AI Regulatory Toolkit & Agentic Skill Execution System. Designed as a modern, client-side Single Page Application (SPA), SmartMed Review 3.0 leverages the power of Google's Gemini Large Language Models (LLMs) to automate, enhance, and streamline the medical and pharmaceutical regulatory review process.
By combining a robust React 19 frontend, Vite for lightning-fast build tooling, Tailwind CSS for dynamic theming, and a suite of document processing libraries (pdfjs-dist, jspdf, html2canvas), the system provides a comprehensive environment for regulatory professionals. Users can ingest complex medical documents, execute agentic AI skills to analyze compliance, edit and refine AI-generated toolkits, and monitor the entire process via a live interactive dashboard.
This specification details the system architecture, component design, state management paradigms, AI integration strategies, security considerations, and future scalability pathways. It is intended for software engineers, AI specialists, product managers, and regulatory compliance officers involved in the ongoing development and deployment of the SmartMed Review platform.
1. Introduction
1.1 Purpose of the System
The primary purpose of SmartMed Review 3.0 is to reduce the cognitive load and time required for regulatory affairs professionals to review medical documentation (e.g., clinical trial protocols, FDA/EMA submission dossiers, labeling documents, and post-market surveillance reports). The system acts as an "Agentic Co-pilot," capable of autonomously executing predefined regulatory "skills" (e.g., checking for adverse event reporting compliance, verifying statistical methodology descriptions, or ensuring proper informed consent formatting) using state-of-the-art generative AI.
1.2 Scope
The scope of this specification covers the frontend architecture, the integration layer with the Google GenAI SDK, local document processing capabilities, the global state management system, and the UI/UX implementation details. It does not cover backend database architectures, as the current iteration is designed to run primarily in the client browser, communicating directly with the Gemini API to ensure maximum data privacy and minimal infrastructure overhead.
1.3 Target Audience
Frontend Engineers: To understand the React component hierarchy, Tailwind theming system, and state management.
AI Engineers: To understand how prompts are constructed, how context windows are managed, and how the gemini.ts service layer operates.
UX/UI Designers: To understand the grid layout, Pantone-inspired color theming, and interactive feedback loops.
QA & Security Teams: To understand data handling, API key management, and browser-based processing constraints.
1.4 Glossary of Terms
Agentic Skill: A predefined, AI-driven workflow that autonomously analyzes a document for a specific regulatory requirement.
Ingestion Zone: The UI component responsible for accepting, parsing, and chunking user-uploaded documents (PDFs, DOCX, TXT).
Pantone Theme: A dynamic CSS variable system allowing the UI to switch between classic design color palettes (e.g., Classic Blue, Living Coral).
Toolkit: A generated set of guidelines, checklists, or summaries produced by the AI based on the ingested documents.
LLM: Large Language Model (specifically referring to Google Gemini 3.1 Pro/Flash in this context).
2. System Architecture
2.1 High-Level Architecture
SmartMed Review 3.0 employs a Client-Heavy, Serverless-API Architecture. The application is delivered as static assets (HTML, CSS, JS) to the user's browser. All business logic, document parsing, and UI rendering occur on the client side.
The only external network communication is directed to the Google Gemini API via the @google/genai SDK. This architectural decision ensures that sensitive medical documents are not stored on an intermediary proprietary server, significantly reducing HIPAA/GDPR compliance overhead. Documents are parsed in-memory, sent to the Gemini API via secure HTTPS, and the results are rendered back to the user.
2.2 Technology Stack
The application is built on a modern, high-performance web stack:
Core Framework: React 19.0.0 (using Functional Components and Hooks).
Build Tool: Vite 6.2.0 (configured for rapid HMR and optimized production bundling).
Language: TypeScript 5.8 (Strict mode enabled for maximum type safety).
Styling: Tailwind CSS 4.1 (with @tailwindcss/typography for rich text rendering).
Animation: Framer Motion 12.38 (for fluid transitions and micro-interactions).
Icons: Lucide React 0.546 (for consistent, scalable vector iconography).
AI Integration: @google/genai 1.29.0 (Official Google SDK for Gemini models).
Document Processing:
pdfjs-dist 5.5 (for client-side PDF text extraction).
jspdf 4.2 & html2canvas 1.4 (for exporting reports and toolkits to PDF).
Markdown & Visualization: react-markdown 10.1, remark-gfm, and mermaid 11.13 (for rendering AI outputs and generating dynamic flowcharts).
2.3 Directory Structure Analysis
The repository follows a feature-based and modular directory structure:
/src/components/: Contains all modular UI components. Separating concerns into specific functional blocks (e.g., IngestionZone, SkillEngine).
/src/context/: Contains AppContext.tsx, the centralized state management hub using React Context API.
/src/lib/: Contains utility functions (utils.ts) and third-party service wrappers (gemini.ts).
/src/App.tsx: The root layout component orchestrating the grid system.
/src/index.css: The global stylesheet defining Tailwind directives and the custom Pantone CSS variables.
3. Core Components & UI/UX Design
The User Interface is designed as a high-density, professional dashboard. It utilizes a responsive CSS Grid layout that adapts from single-column mobile views to a complex multi-column desktop layout.
3.1 Main Layout (App.tsx)
The MainLayout component acts as the structural skeleton. It implements a sticky header with a backdrop blur (bg-card/80 backdrop-blur-md) for a modern glassmorphism effect.
The main content area is constrained to a max-w-7xl container and divided into distinct rows:
Top Row: Interactive Dashboard (spanning 2 columns) and Settings Panel (spanning 1 column).
Middle Row: Ingestion Zone & Live Log (stacked in 1 column) and Toolkit Editor (spanning 2 columns).
Bottom Row: Skill Engine and Wow Features (split evenly).
Footer: Follow-up Questions component.
This layout prioritizes the user's workflow: Configure (Settings) -> Upload (Ingestion) -> Analyze (Dashboard/Live Log) -> Review/Edit (Toolkit Editor) -> Execute Advanced Tasks (Skill Engine).
3.2 Interactive Dashboard (InteractiveDashboard.tsx)
The Dashboard is the primary telemetry center. It visualizes the current state of the regulatory review process.
Metrics Displayed: Number of documents ingested, total token count, active regulatory frameworks (e.g., FDA 21 CFR Part 11, EU MDR), and overall compliance score.
Technical Implementation: Likely utilizes Framer Motion to animate progress bars and numerical counters. It subscribes to the AppContext to receive real-time updates as the gemini.ts service processes data.
3.3 Settings Panel (SettingsPanel.tsx)
This component allows the user to configure the application's behavior and aesthetic.
Theming: Allows toggling between light/dark modes and selecting from the 10 predefined Pantone themes (e.g., Classic Blue, Living Coral).
AI Configuration: Provides inputs for adjusting the Gemini model parameters (Temperature, Top-K, Top-P) and selecting the specific model version (e.g., gemini-3.1-pro-preview for deep reasoning vs. gemini-3.1-flash-preview for speed).
State Interaction: Dispatches actions to the AppContext which immediately reflect across the application via CSS variable updates.
3.4 Ingestion Zone (IngestionZone.tsx)
The critical entry point for data.
Drag-and-Drop Interface: Implements standard HTML5 drag-and-drop APIs.
Processing Pipeline: When a PDF is dropped, it utilizes pdfjs-dist via a Web Worker to extract text asynchronously, preventing UI thread blocking.
Chunking: Extracted text is likely chunked into manageable segments to respect the LLM's context window limits, with overlap to maintain semantic continuity.
3.5 Toolkit Editor (ToolkitEditor.tsx)
A rich text or markdown editing environment where the AI's output is presented for human review.
Markdown Rendering: Uses react-markdown with remark-gfm to render tables, lists, and bold text generated by Gemini.
Human-in-the-Loop (HITL): Users can manually edit the AI-generated text, add annotations, or highlight false positives.
Export: Integrates with jspdf and html2canvas to allow the user to download the finalized toolkit as a formatted PDF report.
3.6 Skill Engine (SkillEngine.tsx)
The core "Agentic" feature of the application.
Skill Library: Presents a list of predefined regulatory skills (e.g., "Check for HIPAA Identifiers", "Validate Clinical Endpoints").
Execution: When a skill is triggered, it constructs a specific prompt combining the skill's system instructions with the ingested document context, and calls the gemini.ts service.
Parallel Processing: Capable of firing multiple skills concurrently using Promise.all, leveraging the asynchronous nature of the Gemini API.
3.7 Live Log (LiveLog.tsx)
A real-time terminal-like interface displaying the system's internal state.
Transparency: Shows API request statuses, token usage, parsing errors, and skill execution progress.
Auto-scrolling: Automatically scrolls to the latest log entry, providing immediate feedback to the user during long-running AI operations.
3.8 Wow Features (WowFeatures.tsx)
A dedicated space for advanced, visually impressive capabilities.
Mermaid Diagrams: Can take AI-generated Mermaid.js syntax (e.g., a flowchart of a clinical trial design) and render it into an interactive SVG using the mermaid library.
Data Visualization: May include complex data representations or highly stylized summary cards highlighting critical regulatory risks.
3.9 Follow Up Questions (FollowUpQuestions.tsx)
A conversational interface allowing the user to chat with the document context.
Contextual Chat: Uses the previously ingested documents and the generated toolkit as the conversation history.
Dynamic Suggestions: The AI proactively suggests 3-4 follow-up questions based on the current state of the review, guiding the user toward deeper insights.
4. State Management & Data Flow
4.1 AppContext (AppContext.tsx)
Given the complexity of the application, a robust state management solution is required. The application uses React's native Context API (createContext, useReducer, or complex useState hooks) to avoid prop-drilling.
Expected State Interface:
code
TypeScript
interface AppState {
  theme: 'light' | 'dark';
  pantoneStyle: string; // e.g., 'classic-blue', 'living-coral'
  documents: ProcessedDocument[];
  extractedText: string;
  activeSkills: string[];
  toolkitContent: string;
  logs: LogEntry[];
  isProcessing: boolean;
  geminiConfig: {
    temperature: number;
    model: string;
  };
}
4.2 Theming & Styling Engine
The theming engine is a hybrid of Tailwind's dark mode and custom CSS variables.
Implementation: As seen in App.tsx, a useEffect hook listens to theme and pantoneStyle changes in the context. It directly manipulates the classList of the document.documentElement (the <html> tag).
CSS Variables: index.css defines root variables (--color-primary, etc.). When a class like .theme-living-coral is applied to the root, it overrides --color-primary with #FF6F61. Tailwind is configured to use these CSS variables, allowing instant, application-wide color shifts without re-rendering the entire React tree.
4.3 Data Flow Diagram (Textual)
Input: User drops a PDF into IngestionZone.
Process (Local): pdfjs-dist extracts text -> Text is dispatched to AppContext.
Action: User clicks "Run Compliance Check" in SkillEngine.
Process (Network): SkillEngine reads text from AppContext, constructs a prompt, and calls gemini.ts.
Feedback: gemini.ts dispatches "processing" events to AppContext, updating the LiveLog and InteractiveDashboard.
Response: Gemini returns Markdown text.
Update: The response is dispatched to AppContext -> updates toolkitContent.
Render: ToolkitEditor re-renders to display the new Markdown.
5. AI & Agentic Integration
5.1 Google GenAI Integration (gemini.ts)
The gemini.ts file acts as the abstraction layer between the React frontend and the @google/genai SDK.
Key Responsibilities:
Initialization: Instantiates the GoogleGenAI client using the API key injected via Vite's environment variables (process.env.GEMINI_API_KEY).
Method Wrapping: Exposes clean asynchronous functions (e.g., analyzeDocument(text, instructions), chatWithContext(history, message)) that hide the complexity of the SDK from the UI components.
Error Handling: Catches API errors (e.g., quota limits, network failures) and formats them into user-friendly log messages dispatched to the LiveLog.
5.2 Prompt Engineering & Context Window Management
Medical regulatory documents are notoriously long (often 100+ pages).
Context Window Optimization: The system must leverage the massive context window of Gemini 3.1 Pro (up to 2 million tokens). However, to reduce latency and cost, the gemini.ts service likely implements intelligent truncation or summarization techniques if the document exceeds optimal lengths.
System Instructions: The AI is guided by strict system instructions to adopt the persona of a "Senior Regulatory Affairs Auditor." It is instructed to output findings in structured formats (JSON or Markdown tables) to ensure the ToolkitEditor can render them predictably.
Structured Output: For specific skills, the system utilizes Gemini's responseSchema feature to guarantee the output conforms to a strict JSON structure, which can then be parsed and visualized in the InteractiveDashboard.
5.3 Agentic Skill Execution
The "Agentic" nature implies the system can make decisions or execute multi-step reasoning.
Chain of Thought: Complex skills may utilize a multi-turn prompt strategy. For example, Skill A extracts all statistical claims. Skill B then takes the output of Skill A and cross-references it with FDA guidelines.
Tool Calling: Future iterations of the gemini.ts service could implement Gemini's Function Calling capabilities, allowing the LLM to request specific sections of a document or trigger external API lookups (e.g., querying a live FDA database) during its reasoning process.
6. Document Processing & Export
6.1 PDF Parsing (pdfjs-dist)
Handling PDFs entirely in the browser is computationally expensive.
Web Workers: To maintain a smooth 60fps UI, pdfjs-dist is configured to run its parsing logic inside a Web Worker.
Text Extraction: The library reads the PDF binary, extracts text layers, and reconstructs the reading order. It must handle complex medical document layouts, including multi-column text, tables, and footnotes.
6.2 Export Generation (jspdf, html2canvas)
Once the AI has generated a toolkit and the user has refined it, the result must be exportable.
HTML to Canvas: html2canvas takes a snapshot of the rendered ToolkitEditor DOM element, capturing the exact visual styling (including Tailwind typography and Mermaid diagrams).
Canvas to PDF: jspdf takes the generated canvas image and embeds it into a downloadable PDF document. This ensures the exported report looks exactly like what the user sees on screen, preserving formatting and branding.
7. Security & Compliance
7.1 API Key Management
Environment Variables: The GEMINI_API_KEY is loaded via Vite's loadEnv and injected into the build via the define configuration in vite.config.ts.
Browser Exposure: Because this is a client-side SPA, the API key is ultimately exposed to the browser's memory and network requests. In a true production environment intended for public use, this architecture would require a backend proxy server to hide the API key. However, for a specialized, internal, or AI Studio-hosted applet, this approach is acceptable provided the user supplies their own key or the environment secures it.
7.2 Data Privacy (Client-Side Processing)
Zero-Retention Architecture: By processing PDFs locally using pdfjs-dist and sending text directly to the Gemini API, the application avoids storing sensitive medical data on a proprietary database.
Ephemeral State: Once the browser tab is closed, all ingested documents, AI outputs, and logs are destroyed. This ephemeral nature is a strong security feature for handling confidential regulatory submissions.
7.3 Regulatory Compliance (Medical Context)
While the software itself is not a medical device, it handles data related to medical regulations.
Audit Trails: The LiveLog component serves as a rudimentary audit trail, recording exactly which skills were executed and when.
Disclaimer: The UI must prominently feature a disclaimer that the AI-generated toolkits are for informational purposes and must be reviewed by a certified human regulatory professional before official submission.
8. Performance & Scalability
8.1 React Optimization
Memoization: Given the large amount of text data flowing through the AppContext, components like ToolkitEditor and LiveLog must utilize React.memo, useMemo, and useCallback to prevent unnecessary re-renders when unrelated state (like the Pantone theme) changes.
Virtualization: If the LiveLog or ToolkitEditor grows to thousands of lines, implementing list virtualization (e.g., react-window) will be necessary to maintain DOM performance.
8.2 Asynchronous Processing
Non-Blocking UI: All heavy operations (PDF parsing, Gemini API calls, PDF export generation) are strictly asynchronous. The UI utilizes loading spinners, skeleton screens, and Framer Motion transitions to keep the user engaged while waiting for promises to resolve.
9. Deployment & DevOps
9.1 Build Process (Vite)
Bundling: Vite uses Rollup under the hood for production builds. It automatically chunks dependencies (e.g., separating pdfjs-dist and framer-motion into their own vendor chunks) to optimize initial load times.
TypeScript Compilation: The tsconfig.json is configured for modern ES2022 targets, ensuring the output JavaScript is highly optimized for modern browsers.
9.2 Environment Configuration
Hosting: The application is designed to be hosted on any static file server or serverless container platform (e.g., Google Cloud Run, Vercel, Netlify). The provided APP_URL environment variable ensures OAuth callbacks or self-referential links resolve correctly regardless of the hosting environment.
10. Comprehensive Follow-Up Questions
To ensure the continued evolution, security, and robustness of SmartMed Review 3.0, the following 20 technical and strategic questions must be addressed by the engineering and product teams:
Architecture & State Management
State Scalability: As the number of Agentic Skills grows, will the single AppContext become a performance bottleneck due to frequent re-renders, and should we consider atomic state management like Zustand or Jotai?
Web Worker Integration: Have we fully isolated the pdfjs-dist parsing logic into a dedicated Web Worker, and how are we handling memory limits if a user uploads a 500+ page PDF dossier?
Persistence: Currently, state is ephemeral. Should we implement IndexedDB to allow users to save their workspace locally and resume reviews across browser sessions without compromising the "zero-retention" security posture?
Error Boundaries: Are React Error Boundaries properly implemented around critical components like the ToolkitEditor and SkillEngine to prevent a single parsing failure from crashing the entire SPA?
AI & Prompt Engineering
Context Window Saturation: When a document exceeds the Gemini model's maximum context window, what specific chunking, overlapping, or map-reduce summarization strategy is implemented in gemini.ts?
Structured Outputs: Are we utilizing Gemini's responseSchema to guarantee JSON outputs for the InteractiveDashboard metrics, or are we relying on fragile regex parsing of Markdown text?
Skill Chaining: Does the SkillEngine support sequential skill chaining (where the output of Skill A automatically becomes the input for Skill B), and how is the dependency graph managed?
Hallucination Mitigation: What specific prompt engineering techniques (e.g., "Cite your sources from the provided text", Chain-of-Thought) are enforced in the system instructions to prevent the AI from hallucinating regulatory clauses?
Model Fallbacks: If gemini-3.1-pro-preview experiences a rate limit or timeout, is there an automatic fallback mechanism to route the request to gemini-3.1-flash-preview?
Security & Compliance
API Key Exposure: Acknowledging this is a client-side SPA, what is the long-term strategy for securing the GEMINI_API_KEY? Will we migrate to a Backend-for-Frontend (BFF) pattern using Express (which is already in the package.json dependencies)?
Data Sanitization: Before sending document text to the Gemini API, is there a local regex-based sanitization step to strip out obvious Patient Health Information (PHI) to ensure HIPAA compliance?
Content Security Policy (CSP): What CSP headers are required to allow connections to the Google GenAI endpoints while blocking unauthorized third-party scripts?
Audit Logging: The LiveLog is ephemeral. Should we implement a feature to cryptographically sign and export the log file as proof of the AI's reasoning process for regulatory compliance audits?
UI/UX & Visualization
Mermaid.js Security: Rendering AI-generated Mermaid syntax can occasionally introduce XSS vulnerabilities if not properly sanitized. How is the input to the mermaid library sanitized in the WowFeatures component?
Responsive Degradation: How does the complex 3-column grid layout in App.tsx degrade on mobile devices, and are the drag-and-drop features of the IngestionZone replaced with standard file pickers for touch interfaces?
Accessibility (a11y): Are the dynamic Pantone theme color combinations tested for WCAG AA contrast compliance, particularly for users with visual impairments reviewing dense text?
Export Fidelity: html2canvas can sometimes struggle with complex CSS Grid layouts or external fonts. Have we validated that the exported PDFs perfectly match the DOM rendering across different browsers?
DevOps & Future Roadmap
Express Server Utilization: The package.json includes express and @types/express, but the architecture is described as client-side. Is there an intended migration to a full-stack Vite+Express setup for handling backend tasks?
Testing Strategy: What is the automated testing strategy for the Agentic Skills? How do we deterministically test LLM outputs in our CI/CD pipeline (e.g., using LLM-as-a-judge frameworks)?
Multi-Modal Expansion: Gemini 3.1 supports multimodal inputs. What is the roadmap for allowing the IngestionZone to accept images of medical devices or audio recordings of clinical consultations for regulatory review?
