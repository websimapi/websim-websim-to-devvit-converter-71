# WebSim API & Asset Extraction Guide

This document details the reverse-engineered process used to fetch project metadata, discover assets, and download raw content from WebSim. It serves as a reference for how the "WebSim ➔ Devvit" converter interacts with WebSim's backend.

## Base URL
All API requests are made relative to:
`https://websim.ai/api/v1`

---

## 1. Project Identification

The first step is resolving a user input (URL or ID) into a canonical Project ID.

### Parsing
The converter accepts inputs in these formats:
- **Direct ID**: `12345678901234567890` (20 chars)
- **Project URL**: `https://websim.ai/p/12345678901234567890`
- **Slug URL**: `https://websim.ai/@username/project-slug`
- **Short Slug**: `@username/project-slug`

### Resolution Endpoints
Depending on the input type, different endpoints are used to retrieve the `projectId` and `current_version`.

**By ID:**
```http
GET /projects/{projectId}