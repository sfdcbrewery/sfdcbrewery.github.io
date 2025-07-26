---
layout: post
title:  Beyond Agentforce - Using MCP with Claude Desktop and Github Co-Pilot 
---
![_config.yml]({{ site.baseurl }}/images/claudemcp/0.png)

The Salesforce ecosystem is rapidly evolving with AI integration, but what if you could skip the complexity of AgentForce and connect your favorite AI tools directly to your Salesforce data? This technical walkthrough explores how to create seamless AI-Salesforce integrations using MCP (Model Context Protocol) servers.

The Challenge with Traditional Approaches
------------------------------------------------
* Complex authentication flows (OAuth, security tokens)
* Manual REST API calls and endpoint management
* Time-consuming OpenAPI3 documentation parsing
* Limited real-time data interaction capabilities

These barriers often prevent quick experimentation and rapid prototyping with Salesforce data.

Enter MCP: The "API for AI"
---------------------------
Model Context Protocol (MCP) serves as a standardized interface between AI applications and external tools. Think of it as middleware that translates AI requests into actionable tool commands, eliminating the need for custom API integrations.

Core Stack
------------------------------------------------

* VS Code with Salesforce Extension Pack
* GitHub Copilot ($10/month) with Claude 3.7 Sonnet
* Claude Desktop App for MCP server management(free version no payment required)
* Salesforce MCP Server for direct org connectivity
    
![_config.yml]({{ site.baseurl }}/images/claudemcp/1.png)

Setup
-------------------------------------

* Install the Salesforce MCP Server
```
npm install -g @tsmztech/mcp-server-salesforce
```
* Downaload and Configure Claude Desktop
  Edit claude_desktop_config.json:
```
{
  "mcpServers": {
    "salesforce": {
      "command": "npx",
      "args": ["-y", "@tsmztech/mcp-server-salesforce"],
      "env": {
        "SALESFORCE_CONNECTION_TYPE": "OAuth_2.0_Client_Credentials",
        "SALESFORCE_CLIENT_ID": "your_client_id",
        "SALESFORCE_CLIENT_SECRET": "your_client_secret",
        "SALESFORCE_INSTANCE_URL": "https://your-domain.my.salesforce.com"  // REQUIRED: Must be your exact Salesforce instance URL
      }
    }
  }
}
```
* Enable Agent Mode in GitHub Copilot. The integration automatically detects the MCP server configuration and offers to connect the tools.
![_config.yml]({{ site.baseurl }}/images/claudemcp/2.png)    

Demo
------------

Here is the demo creating a quote:
    
![_config.yml]({{ site.baseurl }}/images/claudemcp/demo.gif)
    
Key Technical Advantages
------------------------
* **Intelligent Tool Selection** - The AI automatically chooses appropriate tools from the 7 available Salesforce MCP server functions without explicit instruction.
* **Dynamic Authentication** - Even without hardcoded credentials, the system can leverage existing SFDX authentication from VS Code, demonstrating flexible auth handling.
* **Context-Aware Analysis** - The AI provides unsolicited but relevant business insights based on data patterns it discovers, going beyond simple data retrieval.

Few potential use cases
------------------------
* **Data Retrieval**: Contact and opportunity listings
* **Business Analysis**: ACV calculations and pipeline insights
* **Strategic Recommendations**: Actionable sales management advice
* **Contextual Intelligence**: Contract renewal identification

Conclusion
------------------------
MCP servers democratize AI-Salesforce integration by removing technical barriers that traditionally required extensive development resources. This approach enables rapid prototyping and immediate value generation from existing Salesforce data, potentially transforming how organizations interact with their CRM systems.

The convergence of conversational AI and enterprise data platforms represents more than a technical achievement it's a fundamental shift toward intuitive, intelligent business tools that augment human decision-making in real-time.

Huge Kudos to tsmztech for putting this together, check out the full MCP [GitHub repository](https://github.com/tsmztech/mcp-server-salesforce).

Keywords: #SFDCBrewery #Claude #Agentforce #MCP #Salesforce #Githubco-pilot #SriharideepKolagani #SalesforceDX #SalesforceDevelopment #Salesforce #SFDCBrewery #Brewery #SalesforceOnlineTraining #SalesforceTutorials #SalesforceCertification 
