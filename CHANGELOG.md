# Changelog

## [1.0.0] - 2025-01-22

### 🎯 On-Premises SQL Server Support

This version has been specifically adapted from the original Microsoft Azure SQL samples to work with **on-premises SQL Server installations**.

### ✅ Added Features

- **Traditional SQL Server Authentication**: Support for username/password authentication
- **Self-signed Certificate Support**: `TRUST_SERVER_CERTIFICATE` option for local development
- **Local Instance Connection**: Optimized for localhost and on-premises network deployments
- **Environment Configuration**: Added `.env.example` with clear on-premises examples

### 🚫 Removed Dependencies

- **@azure/identity**: Removed Azure Active Directory authentication requirements
- **Azure AD Token Management**: Eliminated cloud-specific authentication code
- **Interactive Browser Credential**: Removed browser-based Azure authentication
- **Cloud-specific Connection Handling**: Simplified for on-premises use

### 🔧 Configuration Changes

- **Updated Sample Configs**: Both Claude Desktop and VS Code Agent examples now use local configurations
- **Environment Variables**: Added `DB_USER`, `DB_PASSWORD`, and `TRUST_SERVER_CERTIFICATE`
- **Connection Logic**: Simplified to use direct SQL Server authentication

### 📝 Documentation Updates

- **README**: Complete rewrite focusing on on-premises deployment
- **Installation Guide**: Updated with local SQL Server requirements
- **Configuration Examples**: All examples now use localhost configurations
- **Usage Instructions**: Updated for on-premises scenarios

### 🛠️ Technical Changes

- **Authentication Method**: Changed from Azure AD to SQL Server Authentication
- **Connection Configuration**: Simplified config creation without token management
- **Security**: Maintained all existing security validations and parameterized queries
- **Build Process**: Cleaned up to remove Azure-specific dependencies

### 🎁 Package Changes

- **Name**: Updated to `mssql-mcp-server-onpremises` to reflect the on-premises focus
- **Dependencies**: Removed `@azure/identity`, kept essential MCP and SQL dependencies
- **Keywords**: Added relevant keywords for discoverability

### 🔄 Migration from Original

This version enables developers to use the MCP server with:
- Local SQL Server Developer Edition
- SQL Server Express instances
- On-premises SQL Server deployments
- SQL Server running in Docker containers

Without requiring:
- Azure subscriptions
- Azure AD authentication
- Cloud connectivity
- Browser-based authentication flows

### 📋 Breaking Changes

- **Authentication**: No longer supports Azure AD authentication
- **Configuration**: Requires SQL Server username/password instead of Azure credentials
- **Dependencies**: Must install without `@azure/identity` package
