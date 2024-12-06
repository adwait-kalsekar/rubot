# RUBot: AI-Enabled University Information and Academic Companion

## Table of Contents
- [Overview](#overview)
- [Description](#description)
- [Motivation](#motivation)
- [System Architecture](#system-architecture)
  - [Microservices Overview](#microservices-overview)
  - [Technology Stack](#technology-stack)
- [Frontend (Next.js + TypeScript)](#frontend-nextjs--typescript)
- [Authentication Service (ExpressJS + MongoDB)](#authentication-service-expressjs--mongodb)
- [Chat Service (ExpressJS + PostgreSQL)](#chat-service-expressjs--postgresql)
- [GenAI Service (Python)](#genai-service-python)
- [Vector Database (MongoDB Atlas)](#vector-database-mongodb-atlas)
- [LLM & Agentic Workflow](#llm--agentic-workflow)
- [RAG (Retrieval-Augmented Generation) Integration](#rag-retrieval-augmented-generation-integration)
- [Deployment & Infrastructure](#deployment--infrastructure)
- [Security & Authentication](#security--authentication)
- [Future Improvements](#future-improvements)
- [Repository Links](#repository-links)
- [Deployed Link](#deployed-link)

---

## Overview
This project is a comprehensive solution designed to streamline the academic experience for university students. It leverages modern web development, microservices, advanced database strategies, vector embeddings, and Large Language Model (LLM) based AI agents. The platform centralizes university information, offers personalized course planning, fetches deadlines from Canvas, and integrates course registration details—all through an intuitive chatbot interface.

---

## Description
This solution was developed as a final project submission for the Advanced Database Course in the Master’s of Information Technology and Analytics program at Rutgers Business School. It demonstrates:
- Modern **database techniques** (MongoDB, PostgreSQL, Vector Databases)
- **Cloud-native** microservices architecture for modularity and scalability
- Integration of **LLM-based AI agents** capable of retrieving academic data, performing vector searches, and interacting with external APIs (e.g., Canvas)
- A single user interface that consolidates diverse functionalities: university info lookup, course planning, assignment tracking, and registration details

---

## Motivation
The development of this platform was inspired by the challenges faced by prospective and current students:
1. **Scattered Information Access:** Before starting graduate studies, researching programs and course details required navigating multiple websites and documents. This project consolidates that data into one unified interface.
2. **Academic Resource Management:** Once enrolled, keeping track of assignments and deadlines across multiple courses and Canvas pages was cumbersome. By integrating AI agents and course data, the system provides quick, conversational access to all academic details, reducing overhead and improving student productivity.

---

## System Architecture
The architecture is built on a microservices paradigm, with each service dedicated to a specific domain responsibility. The frontend and each backend service operate independently, communicating via RESTful APIs. This approach ensures loose coupling, scalability, and easier deployment/maintenance.

### Microservices Overview
- **Frontend (Next.js + TypeScript):** UI Layer and API Gateway
- **Auth Service (ExpressJS + MongoDB):** User management, authentication, and profile handling
- **Chat Service (ExpressJS + PostgreSQL):** Conversation management, message handling, integration with GenAI
- **GenAI Service (Python):** LLM-based agentic AI workflow, RAG models, function calling to external APIs

### Technology Stack
- **Languages:** TypeScript, JavaScript, Python
- **Frameworks:** Next.js (frontend), ExpressJS (backend), LLM tooling (Python)
- **Databases:** MongoDB (Auth), PostgreSQL (Chat), MongoDB Atlas vector store (embeddings)
- **Integrations:** Canvas API, PDF document embeddings, course information retrieval

---

## Frontend (Next.js + TypeScript)
- **Responsibilities:**  
  - Render a responsive, React-based UI  
  - Serve as an API gateway, routing client requests to appropriate backend services  
  - Handle client-side logic, state management, and authenticated sessions  
- **Features:**  
  - Single-page interactive experience  
  - Secure token handling (via JWT) for authenticated routes  
  - Smooth user journey from login to chat interface

**Repository:** [Frontend Application](https://github.com/adwait-kalsekar/rubot-frontend)

---

## Authentication Service (ExpressJS + MongoDB)
- **Responsibilities:**
  - User registration, login, and secure JWT-based authentication
  - Profile management: storing and updating user information in MongoDB
- **Technical Details:**
  - ExpressJS for routing and middleware support
  - MongoDB for document-based data persistence
  - JWT issuance and verification for secure, stateless authentication

**Repository:** [Auth Service](https://github.com/adwait-kalsekar/rubot-auth-backend)

---

## Chat Service (ExpressJS + PostgreSQL)
- **Responsibilities:**
  - Manage user conversations and messages persistently
  - Store and retrieve conversation history, queries, and AI responses
  - Interact with the GenAI service to obtain contextually relevant responses
- **Technical Details:**
  - ExpressJS for REST endpoints  
  - PostgreSQL for structured, relational data storage (optimized for querying message histories)
  - Integrates with GenAI to fetch AI responses dynamically

**Repository:** [Chat Service](https://github.com/adwait-kalsekar/rubot-chat-backend)

---

## GenAI Service (Python)
- **Responsibilities:**
  - LLM-based reasoning using an agentic workflow
  - Implement Retrieval-Augmented Generation (RAG) to incorporate domain-specific data
  - Function calling to external APIs (e.g., Canvas) for live data retrieval
- **Notes:**
  - This service is internal and not directly exposed to end-users
  - Accessible only through the Chat service for security and orchestration

**Note:** The GenAI service code is proprietary and stored in a private repository. It is not publicly accessible.

---

## Vector Database (MongoDB Atlas)
- **Role:**
  - Store vector embeddings of course syllabi, PDFs, and other academic resources
  - Support vector searches to quickly locate the most relevant data points for user queries
- **Benefits:**
  - Rapid similarity search on embeddings
  - Enhanced accuracy and relevance in LLM responses
  - Streamlined retrieval of context for RAG

---

## LLM & Agentic Workflow
- **LLM Choice:**
  - Employs a large language model capable of chain-of-thought reasoning
  - Utilizes system and developer prompts for contextual steering
- **Agentic Workflow:**
  - The LLM can “call” functions or services (e.g., Canvas API) dynamically
  - Multistep reasoning: determines what data is needed, fetches it, and provides a consolidated response

---

## RAG (Retrieval-Augmented Generation) Integration
- **Process:**
  - On user query, the Chat service requests the GenAI service to find relevant embeddings from the vector DB
  - RAG retrieves top matches, feeding them into the LLM prompt to ground responses in factual data
  - Ensures the chatbot provides accurate, context-specific answers rather than hallucinations

---

## Deployment & Infrastructure
- **Backend Services (Auth, Chat, GenAI):** Deployed on **Railway**, a managed cloud platform that simplifies continuous deployment and scaling.
- **Frontend (Next.js):** Deployed on **Vercel**, providing instant global edge network distribution and effortless CI/CD.
- **Static/Media Content:** User profile pictures are stored on **Cloudinary**, a managed S3-like storage solution, ensuring reliable, fast, and scalable media delivery.

**Infrastructure Highlights:**
- Containerized services for consistent environments
- Environment variables stored and managed securely
- Horizontal scaling supported by Railway and Vercel's automatic scaling features

---

## Security & Authentication
- **JWT-based Access Control:**
  - Only authenticated users can access the chat interface and personal data
  - The GenAI service is isolated behind the Chat service, preventing unauthorized direct access
- **Least Privilege:**
  - Each microservice has scoped permissions to its database and limited external APIs
- **Secure Communications:**
  - HTTPS endpoints and TLS for secure data transmission

---

## Future Improvements
- **Scaling the Vector Store:**
  - Experiment with alternative vector databases or embedding models
- **Enhanced UI/UX:**
  - Add personalization features and improved conversation handling
- **More Integrations:**
  - Extend functionality to include scheduling, note-taking, or real-time campus alerts

---

## Repository Links
- **Frontend:** [https://github.com/your-org/frontend-repo](https://github.com/adwait-kalsekar/rubot-frontend)
- **Auth Service:** [https://github.com/your-org/auth-service-repo](https://github.com/adwait-kalsekar/rubot-auth-backend)
- **Chat Service:** [https://github.com/your-org/chat-service-repo](https://github.com/adwait-kalsekar/rubot-chat-backend)

---

## Deployed Link
- **Production Deployment:** [RUBot](https://rubot.vercel.app/)
