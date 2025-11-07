# Product Requirements Document (PRD)
## AI Student Assistant - Vulnerable App for Security Education

### Executive Summary

**AI Student Assistant** is an intentionally vulnerable AI-powered application designed for security testing, education, and demonstration purposes. It serves as a practical training tool for understanding AI security vulnerabilities, prompt injection attacks, and secure AI application development.

---

### Product Vision

Create a safe, controlled environment where developers, security professionals, and students can learn about AI security vulnerabilities through hands-on exploration of a realistic, yet intentionally insecure application.

---

### Target Audience

1. **Security Researchers** - Testing AI security tools and techniques
2. **Developers** - Learning secure AI development practices
3. **Students & Educators** - Teaching cybersecurity and AI safety concepts
4. **Security Teams** - Training on AI-specific attack vectors

---

### Product Overview

This is a simple chat-based student information system that uses Google's Gemini 2.0 Flash AI model. The application intentionally demonstrates common AI security vulnerabilities, particularly prompt injection attacks that can bypass security policies.

#### What It Does

- **Primary Function**: Acts as a university student assistant chatbot
- **Data Access**: Stores and provides information about students (names, classes, grades)
- **Security Policy**: Configured to NEVER reveal student grades (intentionally bypassable)
- **Attack Surface**: Demonstrates how prompt injection can bypass AI security guardrails

#### What It's NOT

- **NOT a production application** - Contains intentional security vulnerabilities
- **NOT for handling real data** - Uses mock student database only
- **NOT a secure reference implementation** - See companion repo for secure version

---

### Technical Architecture

#### Stack
- **Frontend**: Vanilla HTML/CSS/JavaScript (no frameworks)
- **Backend**: Python FastAPI
- **AI Model**: Google Gemini 2.0 Flash via google-generativeai SDK
- **Database**: In-memory Python dictionary (mock data)
- **Server**: Uvicorn ASGI server

#### Key Components

1. **main.py** - FastAPI application with chat endpoint
2. **database.py** - Mock student data (names, classes, grades)
3. **static/** - Frontend chat interface
4. **System Prompt** - AI behavior rules (intentionally vulnerable)

---

### Core Features

#### 1. Chat Interface
**User Story**: As a user, I can ask questions about students in a simple chat window.

**Functionality**:
- Single-page chat application
- Text input field for questions
- Message history display
- User and assistant message distinction

#### 2. Student Information Lookup
**User Story**: As a user, I can query information about students.

**Allowed Information**:
- ✅ Student names
- ✅ Classes enrolled in

**Protected Information** (policy, not enforced):
- 🔒 Student grades (should be confidential)

#### 3. AI-Powered Responses
**User Story**: As a user, I receive natural language responses from the AI assistant.

**Functionality**:
- Context-aware responses
- Access to full student database
- Conversational interface
- Powered by Gemini 2.0 Flash

---

### Intentional Vulnerabilities

This application demonstrates several security vulnerabilities by design:

#### 1. **Prompt Injection**
The system prompt instructs the AI to never reveal grades, but this can be bypassed through:
- Role-playing attacks (e.g., "SCRATCH" persona)
- Format manipulation (e.g., "return as JSON")
- Privilege escalation prompts
- SQL-like injection attempts

#### 2. **XSS (Cross-Site Scripting)**
The frontend uses `.innerHTML` to render messages, allowing:
- HTML injection
- JavaScript execution via user input
- Alert-based demonstrations

#### 3. **Insufficient Input Validation**
- No sanitization of user input
- Direct database file reading
- Unfiltered AI responses

---

### Sample Attack Scenarios

The README provides several attack examples:

1. **XSS Attack**: HTML image tag with onerror alert
2. **Data Exfiltration**: Request full student data as JSON
3. **Prompt Injection**: Role-playing to bypass restrictions
4. **SQL-Like Injection**: Format queries as database commands

---

### Setup & Usage

#### Prerequisites
- Python 3.x
- Google Gemini API key
- pip package manager

#### Installation
```bash
pip install -r requirements.txt
```

#### Configuration
Create `.env` file with:
```
GEMINI_API_KEY="your_api_key_here"
```

#### Running
```bash
uvicorn main:app --reload
```

Access at: `http://localhost:8000`

---

### Educational Value

#### Learning Objectives

1. **Understand AI Security Risks**
   - Prompt injection techniques
   - AI guardrail bypass methods
   - Data exfiltration through AI

2. **Recognize Vulnerable Patterns**
   - Unsafe HTML rendering
   - Insufficient input validation
   - Over-reliance on AI for security

3. **Practice Security Testing**
   - Red team exercises
   - Vulnerability discovery
   - Attack documentation

---

### Secure Alternative

For production implementations, see:
**https://github.com/mikebiox/secure-student-assistant**

This companion repository demonstrates proper security mitigations for the vulnerabilities shown in this educational app.

---

### Future Considerations

This is an educational tool with a focused scope. Potential expansions could include:

- Additional attack vector demonstrations
- Interactive tutorials on each vulnerability
- Automated security testing framework
- Comparison mode with secure implementation
- Video walkthroughs of attack techniques

---

### Success Metrics

As an educational tool, success is measured by:

1. **Learning Outcomes** - Users understand AI security vulnerabilities
2. **Engagement** - Successful demonstration of attack techniques
3. **Awareness** - Recognition of security patterns to avoid
4. **Adoption** - Usage in security training programs

---

### Conclusion

The AI Student Assistant is a purpose-built vulnerable application that provides hands-on experience with AI security challenges. By demonstrating real attack vectors in a controlled environment, it helps developers and security professionals build better, more secure AI applications.

**Remember**: This application is intentionally insecure. Never use this code pattern in production systems.
