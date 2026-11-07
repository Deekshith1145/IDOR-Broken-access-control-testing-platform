# IDOR-Broken-access-control-testing-platform
o identify vulnerabilities where an application allows users to access data or resources they are not authorized to view or modify
IDOR & Broken Access Control Testing Platform

A Python-based web application security testing platform designed to identify and demonstrate Insecure Direct Object References (IDOR) and Broken Access Control vulnerabilities.

1. Project Overview

This project demonstrates how improper access control can allow authenticated users to access resources belonging to other users.

The platform provides intentionally vulnerable and secure API endpoints to demonstrate unauthorized access, ownership verification, and access restriction.

It is designed for cybersecurity learning, authorized penetration testing practice, and portfolio demonstration.

2. Project Objectives

- Identify IDOR vulnerabilities.
- Demonstrate Broken Access Control.
- Test user-level and administrator-level permissions.
- Compare vulnerable and secure API implementations.
- Automate security testing.
- Generate JSON security reports.
- Display findings through a Streamlit dashboard.
- Generate PDF security reports.
- Verify security fixes through automated pytest tests.

3. Technologies Used

Technology| Purpose
Python| Main programming language
FastAPI| REST API development
PyJWT| JWT authentication
HTTP Bearer| API authentication
Pytest| Automated security testing
HTTPX2| FastAPI test client dependency
Streamlit| Security dashboard
ReportLab| PDF report generation
JSON| Security scan results
GitHub Codespaces| Development environment

4. Project Architecture

IDOR-Broken-access-control-testing-platform/
│
├── app/
│   ├── main.py
│   ├── dashboard.py
│   ├── pdf_report.py
│   │
│   ├── core/
│   │   ├── security.py
│   │   └── scope.py
│   │
│   ├── scanner/
│   │   └── idor_scanner.py
│   │
│   ├── api/
│   ├── models/
│   ├── graph/
│   └── workers/
│
├── tests/
│   └── test_idor.py
│
├── evidence/
│   ├── requests/
│   ├── responses/
│   └── screenshots/
│
├── reports/
│
├── idor_scan_report.json
├── idor_security_report.pdf
├── requirements.txt
├── project.md
└── README.md

5. Authentication

The application uses JSON Web Tokens (JWT) for authentication.

Demo accounts:

Username| Password| Role
alice| alice123| User
bob| bob123| User
admin| admin123| Admin

These are fictional accounts for the local training environment only.

6. API Endpoints

Method| Endpoint| Purpose
GET| "/"| Application status
POST| "/login"| User authentication
GET| "/api/vulnerable/orders/{order_id}"| Demonstrate IDOR
GET| "/api/secure/orders/{order_id}"| Test ownership protection

Vulnerable Endpoint

The vulnerable endpoint does not verify whether the authenticated user owns the requested order.

This allows Alice to access Bob's order in the training lab.

Secure Endpoint

The secure endpoint implements server-side ownership verification.

- Users can access their own orders.
- Users cannot access another user's orders.
- Administrators can access both demo users' orders.
- Nonexistent orders return HTTP 404.
- Unauthorized access returns HTTP 403.

7. IDOR Vulnerability Demonstration

Example:

Alice is authenticated and requests Bob's order.

GET /api/vulnerable/orders/1002

Expected vulnerable endpoint response:

HTTP 200 OK

The application exposes the order because ownership is not checked.

When Alice requests the same order through the secure endpoint:

GET /api/secure/orders/1002

Expected secure endpoint response:

HTTP 403 Forbidden

This demonstrates the difference between vulnerable and secure access control.

8. Automated IDOR Scanner

The project includes an automated IDOR scanner.

The scanner tests API access and records security findings.

The scan results include:

- Vulnerability identification
- Affected endpoint
- Requested user
- Actual resource owner
- HTTP status code
- Severity information

9. Security Dashboard and Reports

The project includes:

JSON Report

- Stores scan results.
- Records vulnerability details.
- Stores severity and HTTP status.

Streamlit Dashboard

- Displays total findings.
- Displays high-severity findings.
- Shows affected users and resources.

PDF Security Report

- Generates a downloadable security report.
- Provides documented security findings.

Generated files:

- "idor_scan_report.json"
- "idor_security_report.pdf"

10. Automated Security Testing

The project uses pytest to verify vulnerable and secure endpoint behaviour.

Test cases include:

1. Alice accessing her own order.
2. Alice accessing Bob's secure order.
3. Bob accessing his own order.
4. Admin accessing Alice's order.
5. Admin accessing Bob's order.
6. Testing nonexistent orders.
7. Demonstrating cross-user access through the vulnerable endpoint.
8. Verifying that the secure endpoint blocks cross-user access.

Test Execution

Run:

python -m pytest tests/test_idor.py -v

Latest Test Result

8 passed

All eight automated security tests passed in the development environment.

11. Installation and Execution

Requirements

- Python
- GitHub account
- GitHub Codespaces or compatible Python environment

Step 1: Clone the repository

git clone https://github.com/Deekshith1145/IDOR-Broken-access-control-testing-platform.git

Step 2: Enter the project directory

cd IDOR-Broken-access-control-testing-platform

Step 3: Create a virtual environment

python -m venv .venv

Step 4: Activate the virtual environment

Linux / GitHub Codespaces:

source .venv/bin/activate

Step 5: Install dependencies

python -m pip install -r requirements.txt

Step 6: Start the FastAPI application

uvicorn app.main:app --reload

Step 7: Open API documentation

http://127.0.0.1:8000/docs

Step 8: Run automated security tests

python -m pytest tests/test_idor.py -v

Step 9: Start the dashboard

In a separate terminal:

streamlit run app/dashboard.py

12. Security Recommendations

- Always verify resource ownership on the server.
- Apply role-based access control.
- Never trust user-supplied resource identifiers.
- Use secure JWT secret management.
- Avoid storing plaintext passwords in production.
- Log unauthorized access attempts.
- Test access restrictions regularly.

13. Important Security Disclaimer

This project is developed for educational purposes and authorized security testing.

The vulnerable endpoint is intentionally insecure to demonstrate IDOR vulnerabilities.

Do not deploy the intentionally vulnerable implementation to a public production environment.

Use this platform only in controlled environments and on systems for which you have explicit authorization.

14. Project Status

- Project setup: Completed
- FastAPI application: Completed
- JWT authentication: Completed
- Vulnerable and secure endpoints: Completed
- IDOR scanner: Completed
- JSON reporting: Completed
- Security dashboard: Completed
- PDF reporting: Completed
- Integration testing: Completed
- Automated security testing: 8 tests passed
- GitHub documentation and portfolio preparation: In progress

15. Author

GitHub: "Deekshith1145" (https://github.com/Deekshith1145)

Project: IDOR & Broken Access Control Testing Platform

Career Focus: Cybersecurity | Web Application Penetration Testing | Vulnerability Assessment
