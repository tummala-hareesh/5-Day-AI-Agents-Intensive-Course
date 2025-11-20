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

#### Intruocution: Models, Tools and Agents 

#### Tools and tool calling 

#### Understanding the MCP 

#### MCP: For and Against

#### Security in MCP 

#### Conclusion 


        







            
