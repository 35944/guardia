# Product Purpose Analysis Prompt

> **Purpose**: Analyze a codebase to create a Product Purpose document that defines what the product does, who it's for, and why it exists.
> **Output**: `product-purpose.md`

---

## Instructions for AI Assistant

Analyze this codebase to create a Product Purpose document.

## Analysis Steps

### 1. Identify the Core Problem

- Read README.md, landing page copy, or product description
- Search for comments mentioning "problem", "solve", "pain", "challenge"
- Look at the main entry points - what do they do?

### 2. Map the Capabilities

- List all API endpoints or main functions
- Group them by feature/capability
- Identify which are core vs supporting

### 3. Find the Target Users

- Search for user-related types/models (User, Account, Profile)
- Look at authentication/authorization to understand user types
- Check any analytics or tracking for user segments

### 4. Surface Disconnects (IMPORTANT - these are weaknesses)

- Features that exist in code but aren't documented
- Documentation that promises features not in code
- Dead code or unused endpoints
- Inconsistent naming between docs and code

## Output Format

Create a `product-purpose.md` following the template with:

- **Mission statement** (1 line)
- **What it does** (2-3 sentences)
- **Core capabilities** (3-5 items)
- **The problem it solves**
- **Target users**
- **Differentiators**
- **Desired outcome**

Flag any disconnects found as **"Areas to Align"** at the bottom.
