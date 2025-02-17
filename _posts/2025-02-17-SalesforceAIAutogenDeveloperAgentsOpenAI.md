---
layout: post
title:  AI Salesforce Developer Agents using Microsoft Autogen and OpenAI 
---
![_config.yml]({{ site.baseurl }}/images/aiagent/0.png)

In today's fast-paced development environment, automating repetitive tasks can significantly boost productivity. To address this, I developed the **SFDC Brewery Salesforce Developer Agent**, an AI-powered assistant capable of performing tasks akin to a mid-level Salesforce developer. This agent interprets tasks described in Jira or natural language and generates the corresponding Salesforce code. You can access the project repository [here](https://github.com/sfdcbrewery/Salesforce-AI-Developer-Agent/).

The Future of Enterprise Applications: AI Agents
------------------------------------------------

AI-powered agents are set to revolutionize enterprise applications by automating complex workflows, reducing manual effort, and improving efficiency. With advancements in AI, these intelligent agents can now understand natural language, learn from interactions, and perform tasks that previously required human intervention. Enterprises adopting AI-driven agents can expect:

*   **Increased Productivity**: AI agents streamline processes, allowing teams to focus on strategic work rather than repetitive tasks.
    
*   **Enhanced Decision-Making**: With real-time data processing and intelligent recommendations, AI agents assist in making informed decisions faster.
    
*   **Scalability**: AI agents handle growing workloads without requiring proportional increases in human resources.
    
![_config.yml]({{ site.baseurl }}/images/aiagent/1.png)

Boosting Salesforce Team Productivity
-------------------------------------

For Salesforce teams, AI-powered agents provide tangible benefits, including:

*   **Automating Development Tasks**: AI agents generate and execute Salesforce code, reducing the time required for manual coding.
    
*   **Integrating with Business Tools**: By pulling data from Jira and other sources, AI agents bridge the gap between task management and development execution.
    
*   **Reducing Errors**: Intelligent agents ensure adherence to best practices, minimizing bugs and rework.
    
*   **Accelerating Deployment**: Automated code execution and testing streamline the release cycle, enhancing agility and responsiveness.
    

Key Features
------------

*   **Natural Language Processing**: Understands and processes tasks described in plain English.
    
*   **Jira Integration**: Parses Jira tasks to extract actionable items.
    
*   **Code Generation**: Produces Salesforce code tailored to the specified requirements.
    
*   **Code Execution**: Executes the generated code within a secure environment.
    
*   **User-Friendly Interface**: Offers an interactive web UI for seamless user interaction.
    

Frameworks and Architecture
---------------------------
![_config.yml]({{ site.baseurl }}/images/aiagent/2.png)


The agent leverages several frameworks and technologies to deliver its functionalities:

### 1\. Streamlit for UI

[Streamlit](https://streamlit.io/) is utilized to create a responsive and interactive web interface. It allows users to input task descriptions and view generated code and execution results in real-time.

Placeholder for Streamlit UI setup code

### 2\. Simple-Salesforce for Salesforce Integration

The agent uses the [simple-salesforce](https://github.com/simple-salesforce/simple-salesforce) library to interact with the Salesforce API. This enables seamless authentication and execution of Salesforce operations.

Placeholder for Simple-Salesforce integration code

### 3\. Microsoft Autogen for AI Capabilities

To interpret natural language tasks and generate appropriate code, the agent employs [Microsoft Autogen](https://github.com/microsoft/autogen). This framework facilitates the creation of conversational AI agents capable of complex reasoning and code generation.

Placeholder for Microsoft Autogen assistant agent initialization code

### 4\. Local Command Line Code Execution

For executing the generated code, the agent incorporates a local command-line code executor. This ensures that the code runs in a controlled environment, and results are captured and displayed to the user.

Placeholder for Local Command Line Code Executor setup code

### 5\. Group Chat Manager for Agent Coordination

The agent system includes a group chat manager to coordinate interactions between the assistant agent and the executor agent. This setup ensures a seamless flow from task interpretation to code execution.

Placeholder for Group Chat and Manager initialization code

Full Code of the Agent 
------------------------
```
# app.py

import re
import streamlit as st
from simple_salesforce import Salesforce
from autogen import AssistantAgent, ConversableAgent, GroupChat, GroupChatManager
from autogen.coding import LocalCommandLineCodeExecutor

# Load credentials from Streamlit secrets
sf_creds = st.secrets["salesforce"]
azure_config = st.secrets["azure"]

# Initialize Salesforce connection
sf = Salesforce(
    username=sf_creds["username"],
    password=sf_creds["password"],
    security_token=sf_creds["security_token"],
    domain=sf_creds["domain"]
)

# Initialize Assistant Agent
assistant = AssistantAgent(
    name="assistant",
    system_message="""You are a Salesforce CPQ expert. Generate Python code using simple_salesforce library.
    Ensure the code is executable and handles Salesforce API responses properly.""",
    llm_config={
        "config_list": [{
            "model": "productgpt-4",
            "api_type": "azure",
            "api_key": azure_config["api_key"],
            "base_url": azure_config["base_url"],
            "api_version": azure_config["api_version"]
        }]
    },
    human_input_mode="NEVER"
)

# Initialize Code Executor
code_executor = LocalCommandLineCodeExecutor(timeout=30)
executor_agent = ConversableAgent(
    name="executor",
    system_message="Execute Python code and return results.",
    code_execution_config={"executor": code_executor},
    human_input_mode="NEVER"
)

# Initialize Group Chat and Manager
group_chat = GroupChat(
    agents=[assistant, executor_agent],
    messages=[],
    max_round=6,
    speaker_selection_method="round_robin"
)

manager = GroupChatManager(
    groupchat=group_chat,
    llm_config=assistant.llm_config
)

# Function to extract Python code from assistant's response
def extract_python_code(response):
    """Extract Python code from a response string."""
    patterns = [
        r'```python\n(.*?)\n```',  # Standard markdown
        r'```\n(.*?)\n```',        # Code block without language
        r'%%\n(.*?)\n%%',          # Alternative block format
        r'"""(.*?)"""',            # Triple-quoted string
        r"'''(.*?)'''"             # Triple-single-quoted string
    ]
    
    for pattern in patterns:
        match = re.search(pattern, response, re.DOTALL)
        if match:
            code = match.group(1).strip()
            if code.startswith('python'):
                code = code[6:].lstrip()
            return code
    return None

# Streamlit UI setup
st.set_page_config(page_title="SFDC Brewery Salesforce Developer Agent", page_icon=":robot_face:", layout="wide")
st.title("SFDC Brewery Salesforce Developer Agent 🤖")
st.markdown("Welcome! Describe your JIRA task below, and I'll generate and execute the corresponding Salesforce code for you.")

# Initialize session state for chat history
if "messages" not in st.session_state:
    st.session_state.messages = []

# Display chat history
for message in st.session_state.messages:
    with st.chat_message(message["role"]):
        st.markdown(message["content"])

# Chat input
if prompt := st.chat_input("Describe your Salesforce task:"):
    # Add user message to chat history
    st.session_state.messages.append({"role": "user", "content": prompt})
    with st.chat_message("user"):
        st.markdown(prompt)

    # Generate assistant response
    with st.chat_message("assistant"):
        with st.spinner("Thinking..."):
            try:
                # Initiate chat with the manager
                chat_result = assistant.initiate_chat(
                    recipient=manager,
                    message=prompt
                )

                # Collect all assistant responses
                assistant_responses = [msg for msg in chat_result.chat_history if msg['name'] == 'assistant']
                
                # Try all responses until we find valid code
                python_code = None
                for response in reversed(assistant_responses):
                    python_code = extract_python_code(response['content'])
                    if python_code:
                        break

                if python_code:
                    st.code(python_code, language="python")
                    
                    # Execute the code
                    execution_result = executor_agent.initiate_chat(
                        recipient=manager,
                        message=python_code
                    )
                    
                    # Collect execution output
                    execution_output = ""
                    for msg in execution_result.chat_history:
                        if msg['name'] == 'executor':
                            execution_output += msg['content'] + "\n"
                    
                    # Display results
                    st.subheader("Execution Result:")
                    if execution_output.strip():
                        st.text(execution_output)
                    else:
                        st.warning("No output was returned from the code execution.")
                else:
                    st.error("No valid Python code generated")
                    st.text("Assistant responses for debugging:")
                    st.json([r['content'] for r in assistant_responses])
                
            except Exception as e:
                st.error(f"Error: {str(e)}")

```

Demo
------------
![_config.yml]({{ site.baseurl }}/images/aiagent/demo.gif)


How It Works
------------

1.  **User Input**: The user describes a Salesforce task in natural language or references a Jira ticket.
    
2.  **Task Interpretation**: The assistant agent processes the input, generating the necessary Salesforce code.
    
3.  **Code Display**: The generated code is presented to the user for review.
    
4.  **Code Execution**: Upon user approval, the executor agent runs the code and displays the results.
    

![_config.yml]({{ site.baseurl }}/images/aiagent/3.jpg)

This architecture ensures that users can automate Salesforce development tasks efficiently, reducing manual effort and the potential for errors.

For a hands-on experience and to explore the codebase, visit the [GitHub repository](https://github.com/sfdcbrewery/Salesforce-AI-Developer-Agent/).

_Note: Ensure that all credentials and sensitive information are securely managed and not hard-coded in production environments._

Keywords: #SFDCBrewery #OpenAI #Agentforce #Microsoft #Azure #Autogen #SriharideepKolagani #SalesforceDX #SalesforceDevelopment #Salesforce #SFDCBrewery #Brewery #SalesforceOnlineTraining #SalesforceTutorials #SalesforceCertification 
