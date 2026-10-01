# Architecture Decision Record (ADR)

## 1. Title
Adoption of React Native, Node.js (NestJS), PostgreSQL, and Python (FastAPI) for FitFlow Redesign.

## 2. Status
Accepted

## 3. Context
FitFlow requires a redesign to support a growing user base, complex personalized workout generation via AI, social features, and a seamless cross-platform mobile experience. The previous monolithic or outdated architecture could not scale efficiently or support real-time interactions effectively.

## 4. Decision
- **Frontend:** Use React Native for mobile cross-platform development.
- **Backend:** Use Node.js with the NestJS framework for the primary API.
- **AI Service:** Create a separate microservice using Python and FastAPI for AI and ML workloads.
- **Database:** Use PostgreSQL as the primary relational database.
- **Caching:** Use Redis for session management and caching frequent queries.
- **Authentication:** Utilize Firebase Authentication.

## 5. Consequences
**Positive:**
- Unified mobile codebase reduces development and maintenance overhead.
- NestJS provides a highly scalable and structured backend environment.
- Separating the AI service allows for independent scaling and usage of Python's rich AI ecosystem.
- PostgreSQL ensures data integrity and complex querying capabilities.

**Negative:**
- Requires managing multiple services (Backend + AI Service), increasing deployment complexity.
- Team must be proficient in both TypeScript (NestJS/React Native) and Python.
