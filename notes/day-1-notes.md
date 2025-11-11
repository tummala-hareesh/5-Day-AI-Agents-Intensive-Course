# Notes on Day-1
## Topics
- Introduction to AI Agents
- Taxonomy of Agent Capabilities 
- Need for Agent Ops for reliability and governance
- Importance of agent interoperability & security (through identity and constrained policies)

## CodeLabs
- Build 1st AI Agent
    - Use ADK
    - Use google search for live results 
- Build 1st multi-agent system
    - Create team of specialized agents
    - Explore different architecture patterns

## Assignment
Complete the Unit 1 – “Introduction to Agents”:
- [x] Listen to the summary podcast episode for this unit, created by NotebookLM.
- [x] To complement the podcast, read the “Introduction to Agents” whitepaper
- [] Complete these codelabs on Kaggle:
    - [] Build your first agent using Gemini and ADK.
    - [] Build your first multi-agent systems using ADK.
    - [] Make sure you phone verify your Kaggle account before starting, it's necessary for the codelabs.
    - [] We also have a troubleshooting guide for the codelabs. Be sure to check there for solutions to common problems.
    - [] Want to have an interactive conversation? Try adding the whitepapers to NotebookLM.

### Summary Podcast Episode
- Link to podcast episode: https://www.youtube.com/watch?v=zTxvGzpfF-g

- Autonomous AI Agents
    - Plan, Act, Solve complex problems 
    - Over multiple steps
    - Without holding their hands
    - Autonomy: Execute actions in real work to go. 

- Agent Anatomy 
    - 3 core parts
    - **model**, the brain 
        - model = LLM 
        - the core langugage model, the reasoning engine
        - key responsibilties: 
            - managing context 
            - i.e., decides the input matters for the next though process
        - model thinks, but needs tools to perform actions
        - crucial responsibility:
            - model reasons about which tool is needed for current step of the plan

    - **tools**, the hands
        - connections of outside world or internal systems 
        - Ex: APIs, code functions, ways to access DBs, vector scores
    - **orchestration layer**, the conductor pulling all together
        - calls the tool decided by the model
        - manages: 
            - operational loop
            - keep track of memory or state
            - executing the reasoning strategy, like chain of thought or react, common for agents
    - Each step of the loop: Think, Act, Observe cycle.
    
- Complexity of Agents 
    - **Level 0:**
        - `Baseline`
        - LLM on it's own
        - No tools
        - Knows on what it's trained on. 
        - Can tell about history Maybe, explain a concept.
        - Can't tell about score of last night game!
    - **Level 1:**
        - `The connected problem solver`
        - Tools come in. 
        - connect reasoning engine to tools. 
        - those hands can:
            - search API, DBs, 
            - Answer score questions
        - conects to the world.
    - **Level 2:**
        - `The startegic problem solver`
        - Moving beyond simple tasks, hanlde more complex multi-arch tasks. 
        - Key skill: **context engineering**
            - Agent gets smart after crafting the input for every step
        - Example: find coffee shops with rating >4.0 halfway between two address
            - 1st maps tool to calculate the actual halfway co-oridinates
            - then, takes those results (coordinates or address halfway), uses it to craft a specific query to get coffee shops with rating >4.0 in that neighbourhood nearby. 
        - Actively managing it's own content to give more relevant results and avoid noise. 
    - **Level 3:**
        - `Collaborative multi-agent system`
        - Team of specialists
        - Agents treat other agents as tools
        - Example: A project manager agents delegates tasks to other specialized agents, maybe, market research agent or data analyst agent. 
        - What's the difference? Agent API call vs complex function call
            - The difference is the autonomy of the agent being called. 
            - Agent-to-Agent goal deligation 
    - **Level 4:**
        - `The Self-Evolving System`
        - Frontier now. 
        - System can identify gaps in it's capabilities
            - it knows what it doesn't know or what it can't do
            - fixes it

- Putting Agents in Production? 
    - Model selection 
        - look beyond benchmark scores
        - model routing 
    - Function calling 
        - Tells what tool does and what it needs
        - Structured communication
    - Orchestration layer
        - setting operating rules 
        - like prompting rules 
        - Memory usage: short and long term memory
    - Testing and Debugging 
        - Evaluate quality 
        - Use a "Judge" - Use more powerful Agent to judge
        - If fails, observability is important
            - pinpoint where things were wrong 
    - Security and Scaling 
        - More utility = more risk 
        - Simple rules enforced by calls 
            - AI based gaurdlines 
            - Agent own identify 
            - Own, secure, verifiable identity
        - Single point of control is needed for L-3/L-4
    - How do they learn and improve? 
        - Logs, traces, updated policies
        - improve context engineering
        - future is simulated enviroment. 

- Building Successful Agents 
    - Not just a powerful model thing
    - Agent is combination of:
        - Model for reasoning 
        - Tools for action 
        - Orchestration layer managing the loop
    - Success of Agent 
        - Engineering rigour around it
        - The architecture 
        - The governance 
        - Security 
        - Testing
        - Observability 
        - PROD ready !!!!


### Introduction to Agents - Whitepaper
- Link to whitepaper: https://www.kaggle.com/whitepaper-introduction-to-agents
- `Agents are natural evolution of LLM, made useful in software`. 
- For years, focus was on **models** that excel at passive, discrete tasks:
    - anwering a question
    - translating text
    - generating an image from prompt
    - this paradigm needs constant human direction at every step 
- Moving towards "Autonomous problem solving and task execution"
- New Frontier - "AI Agents"
- What is an AI Agent? 
    - Not a simple static model in AI workflow
    - it's a complete application , making plans and taking actions to achieve goals.
    - Combines LLMs ability to reason with practical ability to act, allowing it to handle complex tasks. 
    - Critically, Agents can work on their own. 
    - 

         



