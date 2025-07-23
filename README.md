# MSSQL On-Premises MCP Server

<div align="center">
  <img src="./src/img/logo.png" alt="MSSQL On-Premises MCP Server Logo" width="400"/>
</div>

## What is this? 🤔

This is a **Model Context Protocol (MCP) server** specifically designed for **on-premises SQL Server databases**. It enables AI assistants like GitHub Copilot and Claude to interact directly with your local SQL Server instances using traditional SQL Server authentication.

**Key Difference**: This version has been adapted from the original Azure SQL samples to work with on-premises SQL Server installations, removing Azure Active Directory dependencies and cloud-specific authentication requirements.

### Quick Example
```text
You: "Show me all customers from New York"
GitHub Copilot: *connects to your local SQL Server and returns the results*
```

## How Does It Work? 🛠️

This server leverages the Model Context Protocol (MCP), a versatile framework that acts as a universal translator between AI models and databases. It supports multiple AI assistants including GitHub Copilot and Claude Desktop.

### What Can It Do? 📊

- Connect to **on-premises SQL Server** instances using SQL Server authentication
- Run queries using **natural language** - no SQL knowledge required
- Create, read, update, and delete data securely
- Manage database schema (tables, indexes)
- **Secure connection handling** with certificate trust options
- Real-time data interaction with local databases

## Quick Start 🚀

### Prerequisites
- **Node.js 16+** installed on your system
- **SQL Server instance** (local, on-premises, or Docker)
- **SQL Server Authentication enabled** on your SQL Server instance
- **Claude Desktop** or **GitHub Copilot**

### Installation

1. **Clone the Repository**
   ```bash
   git clone https://github.com/dnldelarosa/mssql-mcp-onpremises.git
   cd mssql-mcp-onpremises
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Build the Project**
   ```bash
   npm run build
   ```

4. **Configure Environment**
   Create a `.env` file in the root of the project and add the following variables:
   ```env
    SERVER_NAME="localhost"
    DATABASE_NAME="your-database-name"
    DB_USER="your-sql-username"
    DB_PASSWORD="your-sql-password"
    READONLY="false"
    TRUST_SERVER_CERTIFICATE="true"
   ```
   *Alternatively, you can rename the `.env.example` file to `.env` and edit the values.*


## Configuration Setup

### Option 1: GitHub Copilot Setup

1. **Install GitHub Copilot Extension**
   - Open VS Code
   - Go to Extensions (Ctrl+Shift+X)
   - Search for "GitHub Copilot" and install the official extension.

2. **Create MCP Configuration File**
   - Create a `.vscode/mcp.json` file in your workspace
   - Add the following configuration:

   ```json
   {
     "servers": {
       "mssql-onpremises": {
          "type": "stdio",
          "command": "node",
          "args": ["C:/path/to/your/project/dist/index.js"],
        }
      }
   }
   ```
   ***Note**: Ensure the path to `dist/index.js` is correct.*

3. **Alternative: User Settings Configuration**
   - Open VS Code Settings (Ctrl+,)
   - Search for "mcp"
   - Click "Edit in settings.json"
   - Add the following configuration:

  ```json
   {
    "mcp": {
        "servers": {
            "mssql-onpremises": {
                "command": "node",
                "args": ["C:/path/to/your/project/dist/index.js"],
            }
        }
    }
  }
  ```
   ***Note**: For the latest information on how to configure the MCP server with GitHub Copilot, please refer to the official documentation.*

4. **Restart VS Code**
   - Close and reopen VS Code for the changes to take effect

5. **Verify MCP Server**
   - Open Command Palette (Ctrl+Shift+P)
   - Run "MCP: List Servers" to verify your server is configured
   - You should see "mssql-onpremises" in the list of available servers

### Option 2: Claude Desktop Setup

1. **Open Claude Desktop Settings**
   - Navigate to File → Settings → Developer → Edit Config
   - Open the `claude_desktop_config` file

2. **Add MCP Server Configuration**
   Replace the content with the configuration below, updating the path to the project's `dist/index.js` file:

   ```json
   {
     "mcpServers": {
       "mssql-onpremises": {
         "command": "node",
         "args": ["C:/path/to/your/project/dist/index.js"],
       }
     }
   }
   ```

3. **Restart Claude Desktop**
   - Close and reopen Claude Desktop for the changes to take effect

### Configuration Parameters

- **SERVER_NAME**: Your SQL Server instance (e.g., `localhost`, `192.168.1.100`, or `MYSERVER\SQLEXPRESS`)
- **DATABASE_NAME**: Your database name
- **DB_USER**: SQL Server username for authentication
- **DB_PASSWORD**: SQL Server password for authentication
- **READONLY**: Set to `"true"` to restrict to read-only operations, `"false"` for full access
- **TRUST_SERVER_CERTIFICATE**: Set to `"true"` to trust self-signed certificates (recommended for local development)
- **CONNECTION_TIMEOUT**: (Optional) Connection timeout in seconds. Defaults to `30` if not set
- **Path**: Update the path in `args` to point to your actual project location

## Sample Configurations

You can find sample configuration files in the `src/samples/` folder:
- `claude_desktop_config.json` - For Claude Desktop
- `vscode_agent_config.json` - For GitHub Copilot

## Usage Examples

Once configured, you can interact with your database using natural language:

- "Show me all users from New York"
- "Create a new table called products with columns for id, name, and price"
- "Update all pending orders to completed status"
- "List all tables in the database"

## Security Notes

- The server requires a WHERE clause for read operations to prevent accidental full table scans
- Update operations require explicit WHERE clauses for security
- Set `READONLY: "true"` in production environments if you only need read access

## 🛠️ Troubleshooting

### Common Issues

**Connection Failed**
- Ensure SQL Server Authentication is enabled
- Verify firewall settings allow connections on SQL Server port (default 1433)
- Check if `TRUST_SERVER_CERTIFICATE` is set to `"true"` for self-signed certificates

**"Login failed for user" Error**
- Verify username and password are correct
- Ensure the SQL Server user has appropriate database permissions
- Check if the user account is not locked or disabled

**MCP Server Not Listed**
- Restart your AI assistant (Claude Desktop / GitHub Copilot)
- Verify the path to `dist/index.js` is correct
- Check the MCP configuration syntax for any JSON errors

**Build Errors**
- Ensure Node.js 16+ is installed
- Delete `node_modules` and run `npm install` again
- Check for TypeScript compilation errors

### Getting Help

- Check the [Issues](https://github.com/dnldelarosa/mssql-mcp-onpremises/issues) page
- Review the [ATTRIBUTION.md](ATTRIBUTION.md) for technical details
- See original Microsoft samples for additional context

You should now have successfully configured the MCP server for on-premises SQL Server with your preferred AI assistant. This setup allows you to seamlessly interact with your local SQL Server through natural language queries!

## 📄 License

MIT License - See [LICENSE](LICENSE) file for details

## 🙏 Acknowledgments

Based on the original work from [Microsoft SQL-AI-samples](https://github.com/Azure-Samples/SQL-AI-samples), modified to support on-premises SQL Server installations.

See [ATTRIBUTION.md](ATTRIBUTION.md) for detailed information about the original work and modifications made for on-premises support.
