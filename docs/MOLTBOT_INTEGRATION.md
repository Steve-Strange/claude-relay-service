# MoltBot Integration Guide for CRS

## Overview
This document describes how Claude Relay Service (CRS) integrates with MoltBot as an API gateway for subscription-based AI accounts.

## Integration Points

### 1. CRS as a Special Provider
MoltBot Backend treats CRS as a provider for OAuth-based accounts (Claude Code Max, Gemini, etc.)

### 2. API Endpoints Used by MoltBot
- `/api/claude/chat` - Claude chat completions
- `/api/gemini/chat` - Gemini chat completions  
- `/api/admin/accounts` - Account pool monitoring
- `/api/admin/concurrency` - Concurrency status

### 3. Configuration in MoltBot Backend

```yaml
providers:
  claude:
    enabled: true
    use-crs: true
    crs-url: ${CRS_URL:http://localhost:3000}
    crs-token: ${CRS_ADMIN_TOKEN}
```

### 4. Account Pool Management
- MoltBot queries CRS account status via admin API
- CRS handles sticky sessions and concurrency
- Automatic failover when accounts are overloaded

### 5. Monitoring Integration
MoltBot's ApiPoolManagement page includes real-time CRS monitoring:
- Account health status
- Concurrency usage
- Overload detection
- Cost tracking

## Setup Instructions

1. Configure CRS admin token in MoltBot
2. Enable CRS provider in application.yml
3. Access CRS admin at http://localhost:3000/admin-next/
4. Add OAuth accounts in CRS admin panel
5. Monitor through MoltBot admin dashboard

## Best Practices
- Keep 20% account redundancy
- Monitor overload patterns
- Rotate accounts regularly
- Use sticky sessions for context preservation
