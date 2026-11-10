
# AI-Enabled Study — Lesson 1.0
**Student:** Ronnie Baker
**Course:** SEIR Foundations
**Lesson:** 1 — EC2, COBOL, SWIFT, APIs, and Databases
**Date:** November 3, 2026

---

## 1. Databases — Relational vs. Non-Relational

Relational databases organize information into structured tables consisting of rows and columns. They use Structured Query Language (SQL) to retrieve, insert, update, and delete information, and they are particularly useful when data has clearly defined relationships and requires strong consistency. Examples include PostgreSQL, MySQL, Microsoft SQL Server, and Oracle Database. Non-relational databases, commonly called NoSQL databases, use alternative structures such as key-value pairs, documents, graphs, and wide-column storage. They are particularly useful when applications need flexible schemas, high-volume data processing, or distributed scalability. In cloud computing, relational databases are commonly provided through managed services such as Amazon RDS and Aurora, while DynamoDB is an example of a managed NoSQL database. PostgreSQL is especially valuable because it is open-source, supports sophisticated SQL queries, transactions, indexing, extensions, and JSON data. Its disadvantages include the need for database administration, careful performance tuning, and more complex horizontal scaling compared with certain purpose-built NoSQL systems. There is no single universally dominant database: PostgreSQL, MySQL, Oracle, SQL Server, and MongoDB are all important, depending on the application. For a financial application such as Balerica Legacy Bank, a relational database is a logical choice because account balances, payment records, and transaction histories require reliable relationships and transactional consistency.

**Sources:**
1. Reading: AWS — Relational vs. Non-Relational Databases
   https://aws.amazon.com/compare/the-difference-between-relational-and-non-relational-databases/
2. Video: IBM Technology — SQL vs. NoSQL
   https://www.youtube.com/watch?v=Q5aTUc7c4jg
3. AI: ChatGPT (OpenAI, 2026) — Comparison of database models, PostgreSQL, cloud database selection, and SQL vs. NoSQL.

---

## 2. COBOL — The Language Behind Legacy Financial Systems

COBOL stands for Common Business-Oriented Language and was developed in 1959 by a committee called the Conference on Data Systems Languages (CODASYL), with important contributions from the work of computer scientist Grace Hopper. It was designed to create a standardized programming language for business applications that could operate across different computer systems. Although COBOL is considered an older programming language, it remains deeply embedded in banking, insurance, government, payroll, and financial transaction processing. IBM has reported industry estimates indicating that COBOL supports more than 40% of online banking systems, approximately 80% of in-person credit card transactions, and approximately 95% of ATM transactions; these are estimates rather than a comprehensive census of every system in operation. The economic value of the systems running COBOL is enormous, but there is no single reliable global valuation of all COBOL-dependent infrastructure. A major challenge is the availability of experienced engineers: organizations have reported difficulty recruiting and retaining people with COBOL expertise, although a universally representative average age for COBOL programmers is not established by reliable public data. Replacing COBOL systems can be extremely expensive and risky because the original software often contains decades of business rules, financial calculations, integrations, and operational knowledge. Modernization does not necessarily require eliminating COBOL; organizations can preserve the existing core while introducing APIs, modern databases, cloud infrastructure, and contemporary application interfaces. The Balerica Legacy Bank exercise demonstrates this approach by using a modern Python/FastAPI application to communicate with an underlying COBOL banking program.

**Sources:**
1. Reading: Wikipedia — COBOL
   https://en.wikipedia.org/wiki/COBOL
2. Video: Fireship — COBOL in 100 Seconds
   https://www.youtube.com/watch?v=7d7-etf-wNI
3. AI: ChatGPT (OpenAI, 2026) — COBOL history, continuing use, modernization challenges, and financial infrastructure.

---

## 3. SWIFT — International Financial Messaging

SWIFT stands for the Society for Worldwide Interbank Financial Telecommunication. It was established in 1973 by 239 banks from 15 countries to create a standardized, secure, and reliable way for financial institutions to exchange international payment instructions. SWIFT went live in 1977 and eventually became a central component of international banking infrastructure. An important distinction is that SWIFT does not itself transfer or hold money; it transmits standardized financial messages between participating institutions, while the actual movement and settlement of funds occur through financial institutions and payment systems. SWIFT messages communicate information about the sender, recipient, amount, currency, and purpose of financial transactions. Historically, the MT message format was widely used, including MT103 for single customer credit transfers and MT202 for financial institution transfers. The industry has been migrating toward ISO 20022, a newer messaging standard that supports richer and more structured financial information. Under the CBPR+ migration, the ISO 20022 coexistence period ended on November 22, 2025, making native ISO 20022 messaging the standard for the relevant cross-border payment flows. MT103 corresponds broadly to pacs.008, while MT202 corresponds broadly to pacs.009; MT202 COV corresponds to pacs.009 COV. SWIFT faces alternatives and complementary systems such as Ripple-based payment networks, domestic payment infrastructures, Fedwire, and CHIPS, although these systems do not all perform precisely the same function. Replacing SWIFT would be difficult because its value comes not merely from its software but from its extensive institutional membership, international standards, operational trust, integrations, and established financial relationships.

**ISO 20022: Important Message Translations**

| Legacy MT message | ISO 20022 equivalent |
|---|---|
| MT103 | pacs.008 |
| MT202 | pacs.009 |
| MT202 COV | pacs.009 COV |

The coexistence period ended on November 22, 2025. This is an important distinction: the transition did not mean that every legacy MT message disappeared from every possible banking workflow. The migration applied to the relevant cross-border payment message flows, with limited contingency translation arrangements for certain messages.

**Sources:**
1. Reading: Wikipedia — SWIFT
   https://en.wikipedia.org/wiki/SWIFT
2. Video: a16z — Foreign Exchange 101
   https://www.youtube.com/watch?v=eoXdyO9oGJc
3. AI: ChatGPT (OpenAI, 2026) — SWIFT's history, messaging architecture, competitors, ISO 20022, and modernization.

Additional primary reference:
https://www.swift.com/standards/iso-20022/iso-20022-faqs/implementation

---

## 4. APIs — Application Programming Interfaces

An Application Programming Interface (API) is a defined way for different software applications or components to communicate with one another. APIs allow a program to request information or functionality from another program without needing to understand its internal implementation. The general concept of an API predates modern web development, so there is no single inventor of APIs; however, Roy Fielding formally described the REST architectural style in his 2000 doctoral dissertation. REST APIs commonly use HTTP methods such as GET, POST, PUT, PATCH, and DELETE to interact with resources. GET is generally used to retrieve information, while POST is commonly used to submit information or create resources. JSON is a widely used format for exchanging structured information between clients and servers. APIs are fundamental to cloud computing because they allow applications, services, databases, and infrastructure to interact programmatically. They are also important to artificial intelligence because AI applications frequently communicate with external models, databases, tools, and services through APIs. API security is a major concern because an insecure API can expose sensitive information, permit unauthorized transactions, or allow malicious users to manipulate an application. Proper authentication, authorization, encryption, rate limiting, and input validation are therefore essential. In the Balerica Legacy Bank exercise, FastAPI acts as the modern interface between HTTP requests and the underlying COBOL banking programs, demonstrating how APIs can make older software accessible to modern applications.

**Important concepts for the next lab:**

- GET: Retrieve information from a server.
- POST: Submit information to a server, often creating a resource or triggering an operation.
- JSON: A structured format for exchanging data.
- Input validation: Checking incoming information before an application processes it.
- HTTP status codes: Communicate whether a request succeeded or encountered an error.

**Sources:**
1. Reading: MDN — An Overview of HTTP
   https://developer.mozilla.org/en-US/docs/Web/HTTP/Guides/Overview
2. Video: IBM Technology — What Is a REST API?
   https://www.youtube.com/watch?v=lsMQRaeKNDk
3. AI: ChatGPT (OpenAI, 2026) — API history, REST, HTTP, JSON, security, and the importance of APIs to cloud computing and AI.

---

## 5. The Intersection of COBOL, SWIFT, APIs, and Databases

COBOL, SWIFT, APIs, and databases represent different but interconnected layers of modern financial infrastructure. COBOL provides the underlying business logic that processes transactions, validates accounts, and performs financial calculations. SWIFT provides standardized messaging that allows financial institutions to communicate payment instructions across international networks. APIs provide an interface through which modern applications can communicate with older systems without requiring those systems to be completely rewritten. Databases store the persistent information required to operate these applications, including customer accounts, transaction histories, payment records, and financial balances. This combination is important not only in banking but also in healthcare, government, education, and other industries that depend on long-running information systems. The U.S. Government Accountability Office's 2025 report on legacy IT modernization identified 11 particularly critical federal systems, some of which support essential government functions and rely on older technologies such as COBOL. The report highlighted cybersecurity vulnerabilities, increasing maintenance costs, obsolete technology, and shortages of personnel with specialized knowledge as major modernization concerns. Rather than replacing every legacy system immediately, organizations can introduce modern interfaces and infrastructure while preserving proven business logic. The Balerica Legacy Bank lab demonstrates this architecture: a FastAPI application receives HTTP requests, a COBOL bridge invokes legacy banking programs, those programs process fixed-width records, and SQLite maintains the database of record. This is a practical example of how organizations can modernize their infrastructure incrementally instead of attempting a complete replacement of critical systems.

**Architecture demonstrated in the lab:**

```text
             SWIFT Traffic Generator
                       |
                       v
                 HTTP / JSON
                       |
                       v
                    FastAPI
                       |
                       v
                 COBOL Bridge
                       |
                       v
              COBOL Banking Programs
                       |
                       v
                Fixed-Width Files
                       |
                       v
                    SQLite
```

**Sources:**
1. Reading: U.S. Government Accountability Office (2025) — Modernizing Critical Decades-Old Legacy Systems
   https://files.gao.gov/reports/GAO-25-107795/index.html
2. Video: Modernizing COBOL: From Mainframe to API
   https://www.youtube.com/watch?v=-CI8hb-077E
3. AI: ChatGPT (OpenAI, 2026) — Legacy modernization and the intersection of financial messaging, APIs, databases, and COBOL.

---

## Overall Conclusion

The central lesson from this research is that modern financial infrastructure does not necessarily mean that every component must be new. Many organizations continue to depend on established systems because they contain important business logic and have proven reliable over decades of operation. APIs allow those systems to communicate with modern applications, databases preserve the information those applications require, and financial messaging networks such as SWIFT allow institutions to coordinate transactions internationally. Cloud computing provides an opportunity to modernize the infrastructure surrounding these systems while preserving their essential functionality. Understanding how these components interact is important for anyone pursuing cloud engineering, DevOps, cybersecurity, or financial technology.
