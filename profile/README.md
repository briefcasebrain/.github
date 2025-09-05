# Briefcasebrain Partner API Catalog
**Comprehensive API Reference & Integration Guide**

*Version 1.0 | Last Updated: September 2025*

---

## Table of Contents

1. [Overview](#overview)
2. [Quick Start](#quick-start)
3. [SDKs & Client Libraries](#sdks--client-libraries)
4. [Core AI Services](#core-ai-services)
5. [Data Management & Processing](#data-management--processing)
6. [Analytics & Monitoring](#analytics--monitoring)
7. [Authentication & Authorization](#authentication--authorization)
8. [Unified Retrieval Framework](#unified-retrieval-framework)
9. [Administrative Services](#administrative-services)
10. [Content & Document Management](#content--document-management)
11. [Billing & Payments](#billing--payments)
12. [Utility & System Services](#utility--system-services)
13. [Integration Guidelines](#integration-guidelines)
14. [Support & Resources](#support--resources)

---

## Overview

Welcome to the Briefcasebrain API ecosystem—a comprehensive suite of AI-powered legal intelligence, document processing, and analytics capabilities designed for seamless integration into partner applications.

This catalog provides complete documentation for all available APIs, including authentication methods, request/response schemas, and practical integration examples.

### Architecture Overview

Our platform consists of multiple specialized services built with different technologies:
- **Next.js Route Handlers**: Modern web API endpoints with full HTTP verb support
- **FastAPI Services**: High-performance Python APIs with automatic validation
- **Flask Applications**: Flexible Python services for specialized processing

---

## Quick Start

### Prerequisites
- **Authentication**: API keys, JWT bearer tokens, or session cookies
- **Response Format**: All APIs return JSON responses
- **Rate Limits**: Contact your account manager for specific quotas

### Framework Behavior (for developers)
- **Next.js Route Handlers**: `app/api/**/route.ts` with verbs GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS
- **Dynamic route segments**: `[id]`, `[slug]`, catch-all `[...slug]`
- **FastAPI models**: `response_model` provides automatic schema documentation and validation
- **Flask views**: Return dicts (auto-JSON) or explicit `jsonify(...)` responses
- **Streaming**: Server-Sent Events (`text/event-stream`) with `event:`/`data:` line format (UTF-8)

---

## SDKs & Client Libraries

### Python SDK
**Package**: `briefcasebrain-sdk`  
**PyPI**: https://pypi.org/project/briefcasebrain-sdk/

```python
pip install briefcasebrain-sdk
```

**Basic Usage**:
```python
from briefcasebrain import BriefcasebrainClient

client = BriefcasebrainClient(api_key="your-api-key")
result = client.aiafs.score_text("Your text content here")
print(f"AI Authorship Score: {result.aiafs_score}")
```

### JavaScript/Node.js SDK
**Package**: `briefcasebrain-sdk`  
**NPM**: https://www.npmjs.com/package/briefcasebrain-sdk

```bash
npm install briefcasebrain-sdk
```

**Basic Usage**:
```javascript
import { BriefcasebrainClient } from 'briefcasebrain-sdk';

const client = new BriefcasebrainClient({ apiKey: 'your-api-key' });
const result = await client.aiafs.scoreText('Your text content here');
console.log(`AI Authorship Score: ${result.aiafsScore}`);
```

### SDK Features
- **Automatic Authentication**: Built-in API key and token management
- **Type Safety**: Full TypeScript definitions and Python type hints
- **Error Handling**: Comprehensive error handling with retry logic
- **Streaming Support**: Native support for real-time data streams
- **Batch Processing**: Efficient handling of bulk operations

---

## Core AI Services

### 1. AI Authorship Forensic Score (AIAFS)
**Purpose**: Analyze text to determine likelihood of AI authorship with forensic-level accuracy

#### Endpoints

| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/score` | POST | Analyze raw text for AI authorship | Content authenticity verification |
| `/api/score-file` | POST | Analyze uploaded text files (txt/pdf) | Bulk document verification |
| `/api/health` | GET | Service health check | Monitoring integration |

**Request Example**:
```json
{
  "text": "Your text content here",
  "use_spacy": false
}
```

**Response Format**:
```json
{
  "AIAFS": 85.7,
  "probability": 0.857,
  "multiDimensionalAnalysis": {
    "lexical": 0.82,
    "entropy": 0.91,
    "syntax": 0.78,
    "structure": 0.89,
    "ai_markers": 0.94
  },
  "modelAgreement": 0.92,
  "confidence": "high"
}
```

---

### 2. Legal Query Enhancement & Processing
**Purpose**: Transform and enhance legal queries using AI, manage legal research workflows

#### Query Enhancement
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/enhance-query` | POST | Improve query using AI | Better search results |
| `/api/enhanced-legal-query` | POST | Generate refined legal queries | Legal research optimization |
| `/api/analyze-keywords` | POST | Extract key legal concepts | Topic identification |

#### Document Generation & Analysis
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/generate-document-ai` | POST | AI-powered legal document creation | Contract drafting, legal briefs |
| `/api/summary` | POST | Summarize legal documents | Quick document review |
| `/api/contracts` | GET, POST | Manage contract records | Contract lifecycle management |
| `/api/contracts/[id]` | GET, PUT, DELETE | Individual contract operations | Document governance |

#### Search & Retrieval
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/search` | POST | Search across legal documents | Legal research |
| `/api/query` | POST | Execute complex legal queries | Advanced research workflows |

---

### 3. Legal Nexus Pipeline
**Purpose**: Verify legal answers against source documents, prevent hallucinations

| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/verify` | POST | Sentence-level verification against sources | Quality assurance for AI-generated content |

**Request Format**:
```json
{
  "answer": "Legal statement to verify",
  "retrieved_contexts": ["source1", "source2"]
}
```

**Response Format**:
```json
[
  {
    "sentence": "Legal statement portion",
    "fact_supported": true,
    "fact_confidence": 0.94,
    "citation_verified": true,
    "hallucinated": false,
    "reason": "Supported by context 1"
  }
]
```

---

### 4. AI Extractor Framework
**Purpose**: Advanced AI extraction and analysis service with comprehensive processing capabilities

#### Basic API Endpoints
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/health` | GET | Health & service signature | Service monitoring |
| `/process` | POST | Process JSON input with type/provider options | General AI processing |
| `/providers` | GET | List available LLM providers | Provider management |
| `/config` | GET, POST | Read/update engine configuration | System configuration |

#### Enhanced API Endpoints
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/auth/login` | POST | Demo login for JWT token | Authentication |
| `/api/health` | GET | Component health with metrics | Enhanced monitoring |
| `/api/metrics` | GET | Detailed runtime metrics | Performance analysis |
| `/api/process` | POST | Enhanced processing with caching | Production processing |
| `/api/process/stream` | POST | Server-Sent Events processing stream | Real-time processing |
| `/api/upload` | POST | File upload and processing | Document processing |
| `/api/batch/create` | POST | Create batch processing job | Bulk operations |
| `/api/batch/[id]/status` | GET | Batch job status and progress | Job monitoring |
| `/api/batch/[id]/results` | GET | Batch job results | Result retrieval |
| `/api/analyze/clustering` | POST | Cluster documents/conversations | Content analysis |
| `/api/analyze/embeddings` | POST | Generate text embeddings | Semantic analysis |
| `/api/analyze/privacy` | POST | Analyze for PII/privacy concerns | Compliance checking |
| `/api/sessions` | GET | List active sessions | Session management |
| `/api/sessions/[id]` | GET, DELETE | Session details and deletion | Session control |
| `/api/providers/test` | POST | Test provider with validation prompt | Provider testing |
| `/api/cache/stats` | GET | Cache performance statistics | Cache monitoring |
| `/api/cache/clear` | POST | Clear processing cache | Cache management |
| `/api/ws/updates` | WebSocket | Real-time updates (Socket.IO in production) | Live updates |

---

## Data Management & Processing

### 1. Expense Processing
**Purpose**: Automated expense report generation from receipts

| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/process-expense` | POST | Extract expense data from receipts | Automated expense reporting |

**Accepts**: PDF, PNG, JPG receipt uploads  
**Returns**: Structured expense data (date, vendor, amount, description)

---

### 2. LakeFS Proxy
**Purpose**: Authentication and lightweight admin layer for LakeFS data management

#### Authentication
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/auth/login` | POST | Authenticate user, set HTTP-only cookie | User authentication |
| `/api/auth/logout` | POST | Clear authentication cookie | Session termination |
| `/api/auth/me` | GET | Current session profile | User context |

#### User Management
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/admin/users` | GET, POST | List or create users | User administration |
| `/api/admin/users/[username]` | PUT | Update user details | User management |
| `/api/admin/users/[username]/access-keys` | GET, POST | Manage user access keys | Access control |

#### Audit & Monitoring
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/admin/audit-logs` | GET | Recent admin events with pagination | Audit trail |

---

## Analytics & Monitoring

### Analytics Suite
**Purpose**: Comprehensive usage tracking and business insights

#### Core Analytics
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/analytics` | GET | General analytics with CSV/JSON export | Usage reporting |
| `/api/analytics/summary` | GET | High-level metrics summary | Dashboard widgets |
| `/api/analytics/user` | GET | User-specific analytics | Customer insights |
| `/api/analytics/query` | GET | Query performance analytics | Search optimization |

#### Administrative Analytics
| Endpoint | Method | Description | Auth Required |
|----------|--------|-------------|---------------|
| `/api/admin/analytics-dashboard` | GET | Comprehensive admin metrics | Admin |
| `/api/admin/db-metrics` | GET | Database performance metrics | Admin |

---

## Authentication & Authorization

### Session Management
| Endpoint | Method | Description | Required For |
|----------|--------|-------------|-------------|
| `/api/auth/login` | POST | Authenticate user | All protected endpoints |
| `/api/auth/logout` | POST | End session | Security compliance |
| `/api/auth/me` | GET | Current user profile | User context |

### Authentication Methods
- **JWT Tokens**: For programmatic API access
- **Session Cookies**: For web application integration
- **API Keys**: For service-to-service communication

---

## Unified Retrieval Framework

### UIR Framework (Public)
**Purpose**: Advanced search across multiple data sources with hybrid strategies

#### Search Operations
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/v1/search` | POST | Multi-provider keyword search | Comprehensive search |
| `/v1/vector-search` | POST | Semantic similarity search | Concept-based retrieval |
| `/v1/hybrid-search` | POST | Combined search strategies | Best-of-both approaches |
| `/v1/rag/retrieve` | POST | RAG-optimized chunk retrieval | AI answer generation |
| `/v1/analyze-query` | POST | Query analysis (spell, entities, intent) | Query optimization |
| `/v1/batch-search` | POST | Batch multiple search operations | Bulk search operations |

#### Data Management
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/v1/index/documents` | POST | Index or upsert documents | Content management |
| `/health` | GET | Service health check | Monitoring |

---

## Administrative Services

### AI Agent Framework
**Purpose**: Automated workflow and task management

| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/agents` | GET, POST | List or create AI agent jobs | Workflow automation |
| `/api/agents/[agentId]` | GET, DELETE | Manage specific agent jobs | Job monitoring |
| `/api/agents/llm` | POST | Direct LLM interaction | Custom AI processing |

**Agent Creation Example**:
```json
{
  "templateId": "legal-research",
  "name": "Contract Review Agent",
  "description": "Reviews contract for key terms",
  "type": "analysis"
}
```

---

## Content & Document Management

### Document & Blog Management
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/blog/posts` | GET, POST | Manage blog content | Content marketing |
| `/api/blog/generate` | POST | AI-generated blog drafts | Content creation |
| `/api/content/share` | POST, GET | Create shareable document links | Document sharing |

### Conversation Analysis (BriefXAI)
**Purpose**: Analyze and cluster conversations at scale

| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/conversations` | POST | Ingest conversation data | Data pipeline |
| `/api/analysis/start` | POST | Begin analysis session | Batch processing |
| `/api/analysis/results` | GET | Retrieve insights and clusters | Analytics retrieval |
| `/api/monitoring/health` | GET | Service health check | Monitoring |

#### Real-time Communication
| Protocol | Endpoint | Description | Use Case |
|----------|----------|-------------|----------|
| WebSocket | `/ws/analysis` | Real-time analysis updates | Live monitoring |
| WebSocket | `/ws/progress` | Progress notifications | Status tracking |

---

## Billing & Payments

### Payment Processing
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/billing/create-checkout` | POST | Create payment session | Subscription initiation |
| `/api/billing/usage` | GET | Current usage statistics | Usage monitoring |
| `/api/billing/track-usage` | POST | Log usage events | Metered billing |
| `/api/billing/webhook` | POST | Payment processor webhooks | Payment automation |

---

## Utility & System Services

### Health & System Monitoring
| Endpoint | Method | Description | Monitoring Tool |
|----------|--------|-------------|----------------|
| `/api/health` | GET | Basic health check | Uptime monitoring |
| `/api/monitoring` | GET | Detailed system metrics | Performance tracking |
| `/api/system` | GET | System configuration info | Environment monitoring |

### Development & Testing
| Endpoint | Method | Description | Use Case |
|----------|--------|-------------|----------|
| `/api/debug` | GET, POST | Debug information and helpers | Development support |
| `/api/test` | GET, POST | Test endpoints for validation | Integration testing |
| `/api/examples` | GET | API usage examples | Documentation |

---

## Integration Guidelines

### Best Practices
1. **Authentication**: Secure API keys and tokens; prefer short-lived tokens for enhanced security
2. **Rate Limiting**: Implement exponential backoff with jitter for 429/5xx responses
3. **Error Handling**: Parse error JSON responses and surface actionable messages to users
4. **Pagination**: Use tokens/offsets for large result sets to optimize performance
5. **Caching**: Cache idempotent GET responses where permissible to reduce API calls
6. **Monitoring**: Implement comprehensive logging and monitoring for production deployments

### Standard Error Response Format
```json
{
  "error": "Descriptive error message",
  "status": 400,
  "timestamp": "2025-09-05T12:00:00Z",
  "details": {
    "field": "validation_error_details"
  }
}
```

### HTTP Status Codes
| Code | Status | Description |
|------|--------|-------------|
| 200 | OK | Successful request |
| 201 | Created | Resource created successfully |
| 400 | Bad Request | Invalid request parameters |
| 401 | Unauthorized | Authentication required |
| 403 | Forbidden | Insufficient permissions |
| 404 | Not Found | Resource not found |
| 413 | Payload Too Large | Request size exceeded limits |
| 429 | Too Many Requests | Rate limit exceeded |
| 500 | Internal Server Error | Server error |

---

## Support & Resources

### Rate Limits & Quotas
Contact your account manager for:
- Custom rate limits and quotas
- Bulk processing options
- Enterprise SLAs and support
- Volume-based pricing tiers

### Changelog
- **v1.0** (September 2025): Initial comprehensive partner API catalog release

---

## Integration Examples

### Example 1: AI Authorship Detection
```bash
curl -X POST [AIAFS_ENDPOINT]/api/score \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -d '{
    "text": "Analyze this text for AI authorship patterns",
    "use_spacy": true
  }'
```

### Example 2: Legal Query Enhancement
```bash
curl -X POST [LEGAL_ENDPOINT]/api/enhance-query \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "query": "breach of contract damages calculation"
  }'
```

### Example 3: Batch Document Processing
```bash
curl -X POST [EXTRACTOR_ENDPOINT]/api/batch/create \
  -H "Authorization: Bearer YOUR_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "documents": ["doc1.pdf", "doc2.pdf"],
    "processing_type": "legal_analysis"
  }'
```

### Example 4: Real-time Processing Stream
```javascript
const eventSource = new EventSource(
  '[EXTRACTOR_ENDPOINT]/api/process/stream',
  {
    headers: {
      'Authorization': 'Bearer YOUR_TOKEN'
    }
  }
);

eventSource.onmessage = function(event) {
  const progress = JSON.parse(event.data);
  console.log('Processing progress:', progress.percentage);
};
```

---

## Technical References

### Framework Documentation
- **Next.js Route Handlers**: App Router methodology and HTTP verb mapping
- **FastAPI**: Automatic schema generation and Pydantic model validation
- **Flask**: JSON response handling and decorator patterns
- **WebSocket/SSE**: Real-time communication protocols and event formatting

### Security Considerations
- **API Key Management**: Rotation policies and secure storage
- **JWT Token Handling**: Expiration and refresh token strategies
- **CORS Configuration**: Cross-origin request policies
- **Rate Limiting**: Implementation strategies and monitoring

---

*This document is maintained by the Briefcasebrain Partner Success Team. For updates or corrections, please contact aansh@briefcasebrain.com*

---

**© 2025 Briefcasebrain. All rights reserved.**
