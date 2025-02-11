# FortiKey - Documentation T3A2-A

 ### Table of Contents:

- [Team Members](#team-members)
- [Discription](#description)
    - [Purpose](#purpose)
    - [Functionality/Features](#functionality--features)
    - [Target Audience](#target-audience)
    - [Tech Stack](#tech-stack)
    - [Additional Highlights](#additional-highlights)
- [Dataflow Diagram](#dataflow-diagram)
- [Application Architecture Diagram](#application-architecture-diagram)
- [User Stories](#user-stories)
- [Design](#design)
- [Project Management](#project-management)

### Team members

- Nathan Keen
- Kenny Hefford

## Description

### Purpose:
The purpose of this project is to provide businesses with a **easy-to-implement and secure Two-Factor Authentication (2FA) platform**.  The platform enables businesses to protect thier users' accounts from unathorised access by introducing a second layer of authentication beyond the more traditional *username and password* logins.  This platform is designed to help businesses address increasing security concerns in a cost-effective way, without requiring extensive technical expertise to intergrate the solution.  

Additionally, the platform offers a dashboard and API documentation to make integration seamless and user-friendly for developers working with businesses.


### Functionality / Features:

1. **Business Registration and Login:**
    - Businesses can register for an account using their email and password.  
    - Once logged in, they can access their API key for 2FA integration.  
    - Option to reset or regenerate API keys for security purposes.  

2. **Two-Factor Authentication API:**  
    - **Generate QR Code for TOTP Setup:** Businesses can use an endpoint to generate a QR code for their users to scan using apps like Google Authenticator or Authy.  
    - **Validate OTP:** Businesses can use another endpoint to validate OTPs entered by their users during login.  
    - **Usage Logs API:** Businesses can query usage logs to monitor 2FA activity (e.g., the number of successful and failed verifications).  

3. **Backup Codes:** 
    - Businesses can use the API to generate backup codes for users, which can be used in case they lose access to their TOTP device.  

4. **Business Dashboard:**  
    - **A web interface for businesses to:**  
        - View their account details and manage API keys.  
        - Access usage analytics (e.g., total number of 2FA verifications, failed OTP attempts).  
        - View and download API integration documentation.  
    - The dashboard will be responsive, providing seamless access on desktop and mobile devices.  

5. **API Documentation:**  
    - A detailed, developer-friendly guide to help businesses integrate 2FA into their applications.  
    - Includes examples of API requests and responses in JSON format, making the onboarding process smooth.  

6. **Security Features:**  
    - All sensitive data (e.g., passwords, API keys, TOTP secrets) is stored securely using best practices (e.g., hashed with bcrypt, encrypted TOTP secrets).  
    - API rate limiting middleware to prevent abuse (express-rate-limit library).  
    - Detailed logs and monitoring to track unauthorised attempts and system performance.  

### Target Audience:
1. **Small-to-Medium Businesses:**  
    - Companies looking for a simple, plug-and-play 2FA solution to enhance their platform's security.  
    - Businesses that don't have the technical bandwidth to build a custom 2FA solution.  

2. **Developers:**  
    - Developers tasked with adding 2FA functionality to a business's existing applications.  
    - Developers who need an easy-to-follow API with integration examples to minimise time-to-market.  

3. **Security-Conscious Enterprises:**  
    - Larger organisations seeking to add robust authentication mechanisms without diverting resources into building their own solutions.  

4. **Freelance Developers or Agencies:**  
    - Professionals providing services to *small-to-medium sized businesses* that need secure user authentication.  


### Tech Stack:  

- **Frontend:**
    - ***React.js*** for building the business dashboard with reusable components and responsive design.  
    - ***Axios*** for handling API requests between the dashboard and backend.  

- **Backend:**  
    - ***Node.js*** with ***Express*** to create scalable and secure API services.  
    - ***OTPAuth*** to handle TOTP generation and OTP validation.  
    - **Middlewares:** 
        - ***express-rate-limit*** to secure APIs from abuse and brute force attacks.  
        - ***Helmet*** Enhances security by setting HTTP headers to protect against common vulnerabilities. 
        - ***CORS*** Manages cross-origin resource sharing to allow secure communication between the frontend and backend.

- **Database:**  
    - ***MongoDB Atlas*** a cloud database solution to store business and user-related data, including *TOTP secrets and logs*.  

- **Authentication:**  
    - ***JSON Web Tokens (JWT)*** for session and API authentication.  

- **Hosting:**  
    - **Frontend:** ***Netlify*** for fast, reliable, and secure static hosting.  
    - **Backend:**  ***Render*** to host backend services with scalability in mind.  

- **Additional Tools and Libraries:**  
    - ***Bcrypt*** Used to hash and securely store passwords in the database.  
    - ***Dotenv:*** Manages environment variables for configuration (e.g., API keys, database credentials).  
    - ***Winston:*** A logging library for tracking system activity, errors, and performance metrics.  
    - ***Jest:*** A testing framework for writing unit and integration tests to ensure code reliability.  

### Additional Highlights:  
1. **Scalability:**  
    - Designed to handle multiple businesses and their users with minimal latency.  
    - Can support future additions like SMS-based OTP, email verification, or push notifications.  

2. **Flexibility:**  
    - Businesses can easily integrate the API into existing applications regardless of their tech stack.  

3. **Ease of Use:** 
    - Focused on delivering an intuitive dashboard and detailed API documentation to make integration effortless.  

4. **Security:**  
    - Sensitive data (e.g., passwords, API keys, TOTP secrets) is encrypted and stored securely.
    - Rate limiting and monitoring tools prevent abuse and ensure system performance.

- [Back to Top](#table-of-contents)  

## 	Dataflow Diagram

### Level 0: Context Diagram  
The Context Diagram presents a high-level view of the 2FA platform and its interactions with external entities.  The primary users include ***Business Users***, who register, log in, and manage API keys; ***Business Applications***, which integrate 2FA functionalities; ***End Users***, who interact with 2FA through OTPs or QR codes; and ***Developers***, who access API documentation.  The 2FA Platform serves as the central system, handling user authentication, OTP generation, and validation. Data stores, such as the Business Database (storing business details and API keys) and the TOTP Secrets Database (securely storing encrypted TOTP secrets), support these interactions.  Key data flows include registration and login requests, API requests for OTP validation, QR code generation, and access to API documentation.  

![Dataflow Diagram level 0](docs/Level-0-DFD.png)  

### Level 1: High-Level Overview  
At a more detailed level, the system is broken down into five main processes: ***Business Registration & Login***, which handles account creation and authentication; ***API Key Management***, responsible for generating and managing API keys; ***TOTP Management***, which deals with QR code generation, OTP validation, and TOTP secret management; ***Usage Logs***, which track 2FA activity for security and analytics; and ***Dashboard & API Docs***, which provide a user interface and documentation access. The Business Database and TOTP Secrets Database continue to support these processes, ensuring secure and efficient handling of business credentials, API keys, and TOTP secrets.  Data flows at this level specify how different system components interact, such as a business user generating an API key or an end user scanning a QR code.  

![Dataflow Diagram level 1](docs/Level-1-DFD.png)  

### Level 2: Detailed View  
At the most detailed level, each key process is further expanded to outline specific workflows and data exchanges.  ***Register Business*** & ***Authenticate Business*** show how business users register and authenticate using email and password credentials, storing data in the Business Database.  ***Generate API key*** outlines how business users request, generate, and retrieve API keys for integrating the 2FA system into their applications. ***Generate QR Code*** & ***Validate OTP*** covers the generation of QR codes, secure storage of TOTP secrets, and OTP validation by end users.  Data flows illustrate how the TOTP Secrets Database is accessed for encrypting and retrieving stored secrets during authentication. This level provides a granular view of the authentication process, ensuring the secure and efficient implementation of 2FA.

![Dataflow Diagram level 2](docs/Level-2-DFD.png)  


- [Back to Top](#table-of-contents)  

## Application Architecture Diagram

![Application Architecture Diagram](<docs/Application Architecture Diagram_.drawio.png>)

### 1. Frontend (React.js App)
The frontend is a **React.js application** to be deployed on **Netlify** that serves as the user interface for businesses.  It includes a **Business Dashboard** where businesses can register, log in, manage API keys, and view usage analytics.  Additionally, it provides **API Documentation** for developers to intergrate the 2FA API into their applications.  The frontend communicates with the backend via REST API calls to handle business operations and display relevant data.  Building with **Axios** for efficient API requests and **React Router** for seamless navigation, the frontend ensures a responsive and intuitive experience across devices.  

### 2. Backend (Express.js App)  
The backend is an **Express.js Application** that handles all user/business logic and API requests.  It will be deployed on **Render** and includes an **API Gateway** to manage incoming requests, enforce rate limiting, and route requests to the appropriate services.  The backend consists of several services: the **Business Service** for registration and API key management, the **TOTP Service** for QR code Generation and OTP validation, and the **Usage Logs Service** for tracking 2FA activity.  It interacts with the database to store and retrieve data and responds to requests from the frontend and external business applications.  Building with **Node.js**, the backend is scalable and secure, leveraging middleware like **express-rate-limit** and **Helmet** to protect against abuse and vulnerabilities.  

### 3. Database (MongoDB Atlas)  
The database, built with **MongoDB Atlas**, stores all persistent data for the application. It includes two main collections: the **Business Collection**, which stores business account details, API keys, and usage logs, and the **TOTP Secrets Collection**, which stores encrypted TOTP secrets and backup codes for end users. The database communicates with the backend to provide data for business operations, TOTP management, and usage analytics. MongoDB Atlas ensures high availability, scalability, and security, making it an ideal choice for handling sensitive data like TOTP secrets and business information.  

### 4. Business Applications  
**Business Applications** are external systems developed by businesses that integrate the 2FA API. These applications interact with the backend to provide 2FA functionality to their end users. They request QR codes for TOTP setup, send OTPs for validation, and handle user interactions (e.g., displaying QR codes and prompting for OTPs). The backend processes these requests and returns the necessary data (e.g., QR codes, validation results) to ensure secure authentication. The API is designed to be **tech stack-agnostic**, allowing businesses to integrate 2FA seamlessly into their existing applications, regardless of their programming language or framework.

- [Back to Top](#table-of-contents)  

## User Stories  

### Freelance Developer Integrates 2FA for Client Projects  
As a freelance developer building secure web applications for clients,
I want to seamlessly integrate a reliable Two-Factor Authentication (2FA) system using an easy-to-implement API,
So that I can enhance security for my clients' platforms and provide them with a trusted authentication solution.  

#### Acceptance Criteria  
1. ***API Integration***
    - I can generate API keys to securely integrate 2FA into my client's application.  
    - I can follow clear API documentation with example requests and responses.  
    - I can test the 2FA system in a sandbox environment before deployment.  

2. ***User Authentication***  
    - I can generate QR codes for users to scan with a TOTP authenticator app.  
    - I can validate OTP codes provided by users during login.  
    - I can generate backup codes for users in case they lose access to their TOTP app.  

3. ***Security & Best Practices***  
    - API keys are securely generated and can be rotated or deactivated.  
    - All sensitive authentication data is encrypted and never stored in plain text.  
    - Rate limiting prevents brute-force attacks on OTP validation endpoints.  

4. ***Monitoring & Debugging***   
    - I can view logs of 2FA events, including failed and successful OTP validations.  
    - I can access error messages and troubleshooting guides for integration issues.

5. ***Deployment & Client Handoff***  
    - I can provide my clients with a setup guide to enable 2FA on their platform. 
    - I can monitor API usage and ensure smooth operation post-deployment.  

### Business Admin Monitors 2FA Analytics & Manages API Keys
As a business administrator responsible for security oversight,
I want to monitor 2FA authentication analytics and manage API keys through the dashboard, so that I can track authentication trends, identify security risks, and ensure secure API integration.  

#### Acceptance Criteria  

1. ***API Key Management***  
    - I can generate API keys for integrating 2FA with my platform.  
    - I can revoke or regenerate API keys for security purposes.  
    - I can see a list of all active API keys  

2. ***2FA Analytics Dashboard***  
    - I can view the total number of 2FA authentication attempts over time.  
    - I can see a breakdown of successful vs. failed OTP validations.  
    - I can filter authentication logs by date range.  
    - I can download reports of 2FA activity for compliance and security audits.  

3. ***Security Monitoring***  
    - I can view trends in failed OTP attempts, helping identify possible brute-force attacks.  
    - I can receive alerts for unusual spikes in failed 2FA authentication attempts.  


### Business Owner Integrates 2FA for Enhanced Security
As a business owner managing a platform with user accounts,
I want to easily integrate a secure Two-Factor Authentication (2FA) system through a dashboard and an API,
so that I can protect my users from unauthorized access and build trust by improving security.

#### Acceptance Criteria:
1. ***Account Management***
    - I can register and log in using my email and password.
    - I can reset my password if needed.
2. ***Dashboard Features***
    - I can view and manage my API key(s).
    - I can see usage statistics, including successful and failed OTP validations.
    - I can access API documentation with integration guides and examples.
3. ***2FA API***
    - I can generate QR codes for TOTP setup.
    - I can validate OTPs entered by my users.
    - I can generate backup codes for users who lose access to their TOTP app.
4. ***Security***
    - API keys are securely generated and can be regenerated or deactivated.
    - Sensitive data is encrypted and stored securely.
    - API rate limiting prevents abuse.
5. ***Analytics and Reporting***
    - I can view 2FA activity trends and logs.
    - I can download detailed reports for compliance or review.


### End User Uses 2FA for Secure Login  
As an end user accessing a platform with sensitive information,  
I want to use Time-Based One-Time Passwords (TOTP) for enhanced login security,  
so that I can protect my account from unauthorized access and ensure my data remains secure.

#### Acceptance Criteria:  

1. **Account Setup**  
   - I can enable 2FA by scanning a QR code using my preferred authenticator app (e.g., Google Authenticator or Authy).  
   - I receive a set of backup codes during setup for emergency access.  

2. ***Login Process***  
   - After entering my username and password, I am prompted to input a TOTP generated by my authenticator app.  
   - I am notified if the TOTP is incorrect or expired, and I can retry with a valid code.  

3. ***Backup Codes***  
   - If I lose access to my authenticator app, I can use a backup code to log in.  
   - Backup codes can only be used once and can be regenerated if needed.  

4. ***Error Handling***
   - If I fail multiple login attempts, I am notified and may be required to wait for a cooldown period.  
   - I receive clear feedback on issues during login, such as expired codes or incorrect entries.  

5. ***Security Features***
   - I receive confirmation after successful logins via email or notifications.  
   - I can disable or reset 2FA from my account settings if necessary, with proper authentication.  

6. ***User Experience***
   - The process to set up, use, and manage 2FA is intuitive and easy to follow across devices.  
   - The interface provides guidance for troubleshooting common issues, like app setup or backup code use.  


- [Back to Top](#table-of-contents)  

## Design 
The goal of the UI was to promote a clean user-friendly and seamless navigation. For a business app focused on security, professionalism, and modernity, a blue + white + gray color scheme was appropriate. 

### Design
1. Headings, outlines and buttons: #007BFF
2. Normal Text: #343A40
3. Highlights: #F2F4F8
4. Backgrounds: #FFFFFF
5. Normal Font: Roboto
6. Dashboard/headings Font: Montserrat

### Logo
![FortiKey Logo](docs/FortiKeyLogo.png)

The logo design of a shield with a keyhole is inspired by core concepts of security, protection, and access control, which aligns perfectly with the purpose of this app. 

### WireFrames
The App will consist of 5 pages in total which will be responsive to Desktop and Mobile. Dashboard will be organised in Tabs.
1. Landing 
2. Login 
3. Sign Up 
4. QR Scan 
5. Dashboard
    - Dashboard Overview
    - Accounts
    - Usage Analytics
    - API Documentation
    - Manage API Key's
    - Admin Dashboard

#### Landing 
Simple Landing Page that gives potential customers an overview of the app and ability to contact the sales team. 
![Landing Page Desktop](./docs/Desktop%20Landing%20Page.png)
![Landing Page Mobile](./docs/Mobile%20Landing%20Page.png)

#### Login
Easy to use Login Page using your company/business email address.
![Login Desktop](./docs/Desktop%20Login.png)
![Login Mobile](./docs/Mobile%20Login.png)

#### Company Sign up
Sign up using the QR Code.
![Sign Up Desktop](./docs/Sign%20Up%20Desktop.png)
![Sign Up Mobile](./docs/Sign%20Up%20Mobile.png)

#### QR Scan
Generated QR Codes.
![QR Desktop](./docs/QR%20Desktop.png)
![QR Mobile](./docs/QR%20Mobile.png)

#### Dashboards
***Dashboard Overview***
Quick Overview of company stats.
![Dashboard Overview](./docs/Dashboard%20Overview.png)
***Accounts***
View users in your own business.
![Accounts](./docs/Accounts.png)
***Usage Analytics***
Access Usage Analytics
![Usage Analytics](./docs/Usage%20Analytics.png)
***API Documentation***
Your guides for any API related tasks
![API Documentation](./docs/API%20Documentation.png)
***Manage API Key's***
Manage your current keys.
![Manage API Key's](./docs/Manage%20API%20KEY.png)

***Admin Dashboard***
Company Dashboard to view current businesses. The company will say administrator.
![Admin Dashboard](./docs/Admin%20Dashboard.png)



- [Back to Top](#table-of-contents)  

## Project Management
### Why We Used Kanban in Trello  
For this project, we used Trello with the Kanban methodology to streamline task management and keep the workflow organised.  Trello's visual board made it easy to track progress, assign tasks, and collaborate efficiently.

By structuring our board with ***Backlog***, ***To Do***, ***Doing***, ***Peer Review***, ***Testing*** and ***Complete*** columns, we ensured that tasks moved smoothly through different stages.  This helped the team stay focused, identify bottlenecks early, and adjust priorities as needed.

Kanban's flexibility and transparency allowed us to manage work efficiently while keeping everyone aligned on project goals.  Trello's simple drag-and-drop interface made it easy to update tasks, maintain visibility, and ensure steady progress throughout development.  

* Trello board link - https://trello.com/b/L7dyKFHE/fortikey

### Week 1
![Trello board Start](docs/TrelloW1-1.png)  

![Trello card Screenshots](docs/TrelloW1-2.png)   

![Trello card Description](docs/TrelloW1-3.png)  

![Trello card AAD](docs/TrelloW1-4.png)  

![Trello card DFD](docs/TrelloW1-5.png)  

![Trello cards midway through](docs/TrelloW1-6.png)

### Week 2
![Trello card User Stories](docs/TrelloW2-1.png)   

![Trello card Wireframes](docs/TrelloW2-2.png)  

![Trello cards end of week 2](docs/TrelloW2-3.png)  

### Week 3 
![Trello card Submitting Checklist](docs/TrelloW3-1.png)  

![Trello cards end of project planning stage](docs/TrelloW3-2.png)

- [Back to Top](#table-of-contents)