# Notes on Day-2
## Topics
- Role of Tools: Extending Agent capabilities
- Tool Design Best Practices (Granilarity and documentation)
- N x M integration problem
- MCP architecture
- MCP Primitives: Tools, Reousrce, Prompts
- Security Risks: Shadowing & Dynamics injection

## Live-Session 
- Deterministic Frameworks - gaurntee is needed
- Use schema approach for Agent-2-Agent calls
- Instruct Agents to handle Error cases. 
- Documentation is key
- Singleton Agent vs Internet of Agents for Enterprise? Think...
- Super-Intelligence is a possiblity

## CodeLabs
- 


## Assignment
Complete Unit 2 - “Agent Tools & Interoperability with Model Context Protocol (MCP)”:
- [x] Listen to the summary podcast episode for this unit, created by NotebookLM.
- [x] To complement the podcast, read the “Agent Tools & Interoperability with Model Context Protocol (MCP)” whitepaper.
- [x] Complete these codelabs on Kaggle:
    - [x] Explore new ways to add tools to extend what your agents can do.
    - [x] Explore best practices for tools, including using MCP and long-running operations.
    - [x] Want to have an interactive conversation? Try adding the whitepapers to NotebookLM.

### Summary Podcast Episode
- Link to podcast episode: https://www.youtube.com/watch?v=Cr4NA6rxHAM

- Agent Tools & Interoperability with MCP 
    - Models from thinking to doing
    - Tools 
        - Agents senses
        - `n` models x `m` agents =  exp (`n` x `m`) combinations
        - Solution: 
            - MCP - Model Context Protocal 
            - Open standard, streamlines all these
    
        - Tool = function or program - LLM application uses - model can't do natively 
            - 2 types
                - Know something
                - Do something
            - 3 categories of tools
                - 1. function tools 
                    - Developers write 
                    - detailed docstrings
                    - contract, inputs, outputs between functions
                - 2. built-in tools 
                    - provided by service provider
                    - Ex: Gemini with google search 
                - 3. agent tools 
                    - Invoke another agent 
                    - Primary agent is in-charge
                    - Agent tool class or SDK usage
            - Grouping tools 
                - sending emails 
                - connecting to other softwares
                - HITL tool
            
    - Best Practices 
        - 1. Non-negotiable 
            - documenation is prime 
            - doc info. fed to model context
            - Name and description 
        - 2. Describe the Action 
            - task to accomplish 
            - create a bug ; not how to perform soemthing
            - LLM reason - tool Act
            - Publish tasks - Not APIs
            - Keep task focused not the underlying task 
        - 3. Data 
            - Design for conscise output 
            - context window will blow; LLM might degrade
            - Don't return RAW data 
            - Google's ADK - Keep context clean
        - 4. Error Handling
            - Schema validation 
            - Error during execution - should be descriptive and constructive. 
            - Ex: API rate limite exceeded; please call after 10min or increase time limits if access is present 

    - Client x Server interaction 
        - 3 working together 
            - MCP Host
            - MCP client 
            - MCP Server
        - COmmunication layer 
            - Standard JSON 
        - Transport layer 
            - Local, Child - DDO Input./Output
            - Real-world distributed - Streamable HTTP

    - Tools are core value propogation for MCP 
        - Standardized Schemas defs. - Contract
        - Results come back in 2 forms 
            - Structured - JSON
            - Unstructured - raw text, audio file, etc.,
        - Signal when tool execution fails 
            - Standard MCP protocol errors
            - Errors during tools execution 
                - Call completes - but, results is error
            
    - Strategic Wins due to MCP 
        - Accelerating dev. 
        - Re-using work 
        - Lowering barrier to entry 
        - Public MCP registries 

    - Major Non-Security problem
        - Connection to Many tools 
        - Standardization - firehouse of tools - problems of blow
        - Solution: 
            - Filter before you Load
            - Tool retreival RAG 
            - Sematic search on Tool database 
            - Reduce context blow 

    - Security Problems 
        - Risk-1: 
            - Critical 
            - Confused deputy 
            - MCP Sever with high level access - User asks MCP (confused deputy)
            - Doesn't check access of the User
            - Solution: 
                - don't expose MCP servers openly 
                - external APIs 
                    - check access
                    - limits etc., 
- Conclusion:
    - Standard models are powerful brains ; but need tools to ACT
    - MCP is standard language - connect brains to hands/eyes (a.k.a tools)
        - Getting most value - disciplined; focus on tasks not apis
        - Robust security aroudn the protocol 
    - Control, Autherization, and Accountability in Agentic world. 


### Whitepaper - Agent Tools & Interoperability with MCP 
- Link to whitepaper: https://www.kaggle.com/whitepaper-agent-tools-and-interoperability-with-mcp

#### Introduction: Models, Tools and Agents 
- Advanced Models 
    - Many things like: law exams, writing code, creating images/videos, solving math problems 
    - Generate new content based on data it was prev. trained on.
    - Can't access any new data about the world except - fed into context
    - Can't interact with external systems 
    - Can't take actions to influence env. 
    - Modern foundational models
        - Capacity to call external functions or tools
        - Tools act as "eyes" and "hands" - to perceive and act on the world 

    - AI Agent use: 
        - Foundational model's reasoning capability
        - to interact with users and achieve specific goals

    - Challenges - Connecting external tools to foundational models 
        - Basic tech. issues 
        - Important security risks
- MCP: 
    - Introduced in 2024
    - Way to streamline the process of intergrating tools and models 
    - Address tech. and security challenges

- To Learn: 
    - Nature of tools used by found. models
    - What they are? How to use them? 
    - Best practice and guidelines for designing effective tools - use them effectively 
    - Look into MCP
        - basic components 
        - some of the challenges
        - risks it entails 
    - Risks posed by MCP - enterprise env. and connected to high-value external systems

#### Tools and tool calling 
- What do we mean by a tool? 
    - Tool
        - function or program an LLM-based application can use 
        - to aaccomplish a task outsid ethe model's capability
    - Model - generates content to respond to the user's question 
    - Tool - let the application interact with other systems  

    - 2 Types of Tools 
        - To Know - allow model to know something - Ex: access data 
        - To Do -  allow model to do something - Ex: call external API 
    
- Types of tools 
    - Tool: liek a function in a non-AI program 
    - Declares a contract between the model and the tool 
    - At min, includes:  
        - clear name
        - parameters
        - a natural language description
            - to explain it's purpose
            - how to use it 
    - 3 Types of tools 
        - 1. Function Tools
            - developer to define external fucntions for model to call 
            - basic details:
                - how the model should use the tool 
                - provided as part of request context 
            - In python frameworks like Google ADK, 
                - definition passed to model is extracted from python docstrings 
        - 2. Built-in Tools 
            - Ability to leverage built in tools  - tool def. is in model implicitly or behind the scene of the model service
            - Gemini API 
                - Google Search 
                - Code execution 
                - URL Context
                - Computer Use
        - 3. Agent Tools 
            - Agent invoked as a tool 
            - Prevents a full handoff of the user conversation 
            - Primary Agent controls the Sub-agent input and output as needed 
            - In ADK,
                - AgentTool class
                - A2A protocol  - remote agents as tools 
    
- Taxonomy of Agent Tools 
    - Categorizing by agent tools's primary function 
        - Information Retrieval 
        - Action/Execution 
        - System/API Integration 
        - Human-in-the-Loop

- Best Practices 
    - Documentation is important
    - Tool documentation (name, description, and attributes)
        - use a clear name - clearly descriptive, human readable, specific to the model 
        - describe all input and output parameters
        - Simplify parameter list
        - Clarify tool description - avoid shorthand or technical jargon; focus on clear explanation using simple terminology 
        - Add targeted examples 
        - Provide default values 
 
- Describe Actions, not implementations
    - Describe Actions -> not specific tools 
    - Try eliminate possiblity of conflict between instructions on how to use tool 
    - Describe what, now how
    - Don't duplicate instructions 
    - don't dictate workflows
    - Do explain tool interactions

- Publish Tasks, Not API Calls
    - tools - encapsulate tasks the agent needs to perform, not any external API
    - tool developers - define tools that clearly capture specific actions the agent might take on behalf of the user
    - tools - expected to be used dynamically - by an agent that decides a runtime 

- Make tools as granular as possible 
    - Functions concise - limited to single function
    - Design for concise output 
        - Dont' return large responese 
        - Use external system s
    
- Use validation effectively 
    - Use optional schema validation for input and outputs
    - Run-time check on tool operation 

- Provide descriptive error messages 
    - Overlooked opportunity for refining and documenting tool capabilities


#### Understanding the MCP 
- The "N x M" Integartion problem and need for standardization 
    - tools are essential link between an AI Agent or an LLM and external world 
    - `Anthropic` introduced MCP in 2024, open standard
    - Replace the fragmented landscape of custom integration 
        - unified, plug and play protocol
        - serve as a universal interface between AI apps and vast world of external tools and data. 
    - By Standardizing the communication layer, 
        - MCP aims to decouple the AI Agent from specific implementation details of the tools it uses
        - modular, scalable and efficient ecosystem 

- Core Architecture Compoenents of MCP 
    - Inspired by `Language Server Protocol (LSP)`
    - Seperate AI app from tool integration - makes it modular, and extensible to tool dev. 
    - Hosts
        - Responsible for creating and managing indiviual MCP clients
        - Responsibilities include: 
            - managing user experience
            - orchestration  the use of tools 
            - enforcing security policies
            - content guardrails
    - Clients
        - software compoenet embedded within the host that maintains the connection with the server 
        - resposible for issuing commands, receiving responses, and managing the lifecycle of the communication session with its server
    - Servers
        - Program that provides set of capabilities the server developer watns to make avaialbel for AI application 
        - Functions as adapter or a proxy for an ternal tool 

```
┌─────────────────────┐
│       HOST           │
│  (Main App UI)       │
│  - Manages tools     │
│  - Enforces safety   │
└─────────┬───────────┘
          │ Uses
          ▼
┌─────────────────────┐
│       CLIENT         │
│  (Messenger)         │
│  - Sends commands    │
│  - Gets results      │
└─────────┬───────────┘
          │ Talks to
          ▼
┌─────────────────────┐
│       SERVER         │
│  (Tool provider)     │
│  - Lists tools       │
│  - Executes tasks    │
│  - Returns results   │
└─────────────────────┘
```

- Communication Layer 
    - built on a standardized tech. foundation for consistency and interoperability 
    - Base protocal: JSON-PRC 2.0 as its base message format; light-weight, text-based, language-agnostic 
    - Message Types:    
        - Requests: An RPC call sent from on party to another that expects a response
        - Results: Mesage containing the successful outcome of request
        - Errors: indicating that a request failed, including code and description
        - Notifications: one-way message that does not require a reponse and can't be replied to.

Transport Mechanism: 
    - Standard protocol for communication between client and server  - transport protocol
    - two transport protocols 
        - local communcaiton - STDIO
        - one for remote communications: Streamable HTTP

Tools
    - The Tool entity in MCP - Standardized way for a server to describe a function it makes available to clients
    - Definictions: 
        - JSON schema 
        - name 
        - title 
        - description 
        - inputSchema
        - outputSchema
        - annotations

Other Capabilities 
- 5 other capabilities that servers and clients can provide 
    - Resources:
        - Server-side capability to provide contextual data 
        - Resources should be validatied and retrieved from a trusted URL 
    - Prompts:
        - server-side capability
        - MCP server - gives client a higher-level description of how to use the tools it provides
    - Sampling: 
        - client-side capability 
        - Request an LLM completion form the client 
        - Content guardrails; offloading LLM calls to client
    - Elicitation 
        - client-side 
        - MCP server to request additional user information form client 
        - Skips LLM and can query host application dynamically for additional data to complete the tool request. 
        - Must not use Elicitation to access Private information
    - Roots: 
        - define the boundaries of where servers can operatte within the filesystem 


#### MCP: For and Against
- Capabilities and Strategic Advantages 
    - Accelerating Development and Fostering a reusable ecosystem  (MCP Registry as source of truth)
    - Dynamically Enhancing Agent Capabilities and Autonomy
        - Dynamic tool discovery 
        - Standardized and structing tool description 
        - Expanding LLM capabilities 
    - Architectural Flexibility and Future-Proofing 
    - Foundations of Governance and Control 

- Critical Risks and Challenges 
    - Need a layer in support (authentication, authorization and user isolation etc., )

- Performance and Scalability Bottlenecks 
    - context windows Bloat 
    - Degraded Reasoning Quality 
    - Stateful Protocol Challenges
    - `RAG based approach for tool discovery itself`

- Enterprise Readiness Gaps
    - Authentication and Authorization 
    - Identity Management Ambiguity
    - Lack of Native Observability 

#### Security in MCP 
- New threat landscape
    - Unauthorized actions and ata exfiltration 
    - Requires a proactive, evolving and multi-layered approach 

## Risks and Mitigation 
- Dynamic capability injection 
- Tool Shadowing 
- Mitigations:
    - Prevent Naming Collioisns 
    - Mutual RLS 
    - Deterministic Policy Enforecement 
    - REquire Human-in-the-Loop (HIL) for high-risk operations
    - Restrict Access to Unauthorized MCP servers


#### Conclusion 
- Foundational Models need tools to observe real data and take actions 
- Good tools require clear docs, simple tasks, concise outputs, and helpful error messages. 
- MCP is a standard that lets' AT system discover and use tools easily
- Solves messy "N x M " integration problem 
- MCP lacks built-in security, identify controls and monitoring 
- MCP requires a governance layer 
- Orgs must use API gateways for policy enforcement, other security related items 
- MCP enables tool interoperability, but enterprises must add the security and control.






            
