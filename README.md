# Airbnb Clone Project
The backend of the Airbnb Clone project is built to deliver a reliable and scalable system that handles user interactions, property listings, reservations, and payment processing. It is designed to replicate Airbnb’s essential features, providing a seamless experience for both users and hosts.

## Project Goals
* **User Management:** Build a secure framework for user sign-up, login, and profile handling.

* **Property Management:** Enable users to create, update, and view property listings.

* **Booking System:** Implement functionality that allows users to book properties and manage their reservations.

* **Payment Processing:** Set up a payment gateway to process transactions and maintain payment records.

* **Review System:** Let users submit ratings and reviews for listed properties.

* **Data Optimization:** Optimize database performance for fast and efficient data access and storage.

## Technology Stack
* **Django:** Powers the backend logic for user authentication, property listings, bookings, and payments.

* **Django REST Framework (DRF):** Builds and manages the API endpoints consumed by the frontend.

* **PostgreSQL:** Stores structured data like users, listings, bookings, and reviews.

* **GraphQL:** Enables the frontend to fetch only the data it needs. Thereby improving performance and flexibility.

* **Celery:** Manages background tasks such as sending booking confirmations and handling asynchronous jobs.

* **Redis:** Supports caching, Celery task queuing, and session management for faster responses.

* **Docker:** Ensures consistent environments for development, testing, and deployment.

* **CI/CD Pipelines:** Automates code testing and deployment for faster, reliable delivery of updates.


## Team Roles
* **Business Analyst (BA):** Defines project requirements by analyzing user needs and workflows, ensuring the development team builds features like bookings, listings, and reviews aligned with business goals.

* **Product Owner (PO):** Owns the product vision, prioritizes the feature backlog (e.g. payment integration, property listings) and ensures the final product meets user expectations and market needs.

* **Project Manager (PM):** Coordinates timelines, team tasks, and progress to ensure smooth delivery of the Airbnb clone within budget and deadline, managing Agile iterations and communication.

* **UI/UX Designer:** Designs intuitive user flows and interfaces for booking properties, viewing listings, managing profiles, and leaving reviews, ensuring a seamless user experience across devices.

* **Software Architect:** Defines the system architecture (e.g. Django backend + PostgreSQL + Redis), selects tools like Celery for background tasks, and ensures scalable, secure software structure.

* **Backend Developer:** Builds and maintains core application logic. APIs for property listings, bookings, user management, payment processing, database schemas, and background tasks with Celery.

* **Frontend Developer:** Implements the user-facing interface. Develops responsive pages for browsing, booking, reviews, and dashboards, integrating with backend APIs.

* **Quality Assurance Engineer:** Manually tests the app’s functionality. Validating that bookings, payments, and user actions perform correctly under various conditions.

* **Test Automation Engineer:** Creates automated tests for critical flows like login, bookings, and payments to ensure reliable updates and quick feedback during development.

* **Devops Engineer:** Sets up and manages CI/CD pipelines, Docker environments, and deployment workflows, enabling fast, stable, and consistent releases.

## Database Design

### 1. **User**
Represents both guests and hosts.

**Important Fields:**
- `id`: Unique identifier
- `name`: Full name of the user
- `email`: Email address (unique)
- `role`: Either 'guest' or 'host'
- `date_joined`: Account creation date

**Relationships:**
- A user can list multiple properties (as a host)
- A user can make multiple bookings (as a guest)
- A user can leave multiple reviews

---

### 2. **Property**
Represents a place listed by a host.

**Important Fields:**
- `id`: Unique identifier
- `title`: Title of the listing
- `description`: Detailed property info
- `location`: Address or city
- `price_per_night`: Rental cost per night

**Relationships:**
- Each property is owned by one user (host)
- A property can have many bookings
- A property can have many reviews
- A property can have multiple images
- A property can have availability records

---

### 3. **Booking**
Represents a reservation made by a guest.

**Important Fields:**
- `id`: Unique identifier
- `user_id`: Guest making the booking
- `property_id`: Booked property
- `start_date`: Check-in date
- `end_date`: Check-out date

**Relationships:**
- Each booking is linked to one user (guest)
- Each booking is for one property
- Each booking can be linked to one payment

---

### 4. **Review**
Captures feedback from guests about properties.

**Important Fields:**
- `id`: Unique identifier
- `user_id`: Reviewer (guest)
- `property_id`: Reviewed property
- `rating`: Score (e.g., 1–5)
- `comment`: Optional review text

**Relationships:**
- A review belongs to one user
- A review belongs to one property

---

### 5. **Payment**
Tracks transactions for bookings.

**Important Fields:**
- `id`: Unique identifier
- `booking_id`: Related booking
- `amount`: Total paid
- `payment_status`: e.g., 'paid', 'pending', 'failed'
- `payment_date`: Timestamp of payment

**Relationships:**
- Each payment is linked to one booking

---

### 6. **PropertyImage**
Stores images of a listed property.

**Important Fields:**
- `id`: Unique identifier
- `property_id`: Associated property
- `image_url`: Path or URL to the image
- `is_featured`: Boolean to mark main image

**Relationships:**
- A property can have multiple images

---

### 7. **Availability**
Defines available dates for a property.

**Important Fields:**
- `id`: Unique identifier
- `property_id`: Associated property
- `start_date`: Start of availability window
- `end_date`: End of availability window

**Relationships:**
- A property can have multiple availability periods

## 🚀 Feature Breakdown

### 1. **User Management**
Enables users to register, log in, and manage their profiles. It supports role-based access for guests and hosts, ensuring a secure and personalized user experience.

### 2. **Property Management**
Allows hosts to create, update, and delete property listings with details such as title, description, price, and images. This feature gives hosts full control over the properties they offer on the platform.

### 3. **Booking System**
Enables guests to browse available properties and make reservations by selecting dates and confirming bookings. This is the core transactional feature that facilitates short-term stays and property rentals.

### 4. **Payment Processing**
Handles secure online payments for bookings, including tracking payment status and storing transaction records. This feature ensures a smooth and trustworthy payment experience for both guests and hosts.

### 5. **Review System**
Allows guests to leave reviews and rate properties after their stay. It fosters trust and transparency by helping future guests make informed booking decisions based on past experiences.

### 6. **Availability Management**
Enables hosts to define when their properties are available or blocked out for booking. It prevents double bookings and ensures that only available dates can be reserved.

### 7. **Image Upload and Management**
Supports uploading and displaying property images to enhance listing appeal. Hosts can showcase their property visually, which plays a vital role in influencing guest bookings.

### 8. **Search and Filtering**
Allows users to search for properties by location, price, availability, and more. This feature enhances the user experience by helping guests quickly find listings that match their preferences.

### 9. **Notifications**
Sends booking confirmations, payment receipts, and other alerts via email or in-app messages. It keeps users informed and enhances platform communication and reliability.

### 10. **Admin Dashboard**
Provides platform administrators with oversight of users, properties, bookings, and payments. It aids in moderating content, managing disputes, and maintaining overall system health.

## 🔒 API Security

Ensuring the security of the platform is essential to protect user data, prevent misuse, and maintain trust. The following measures will be implemented:

### 1. **Authentication**
All API endpoints will be secured using token-based authentication (e.g., JWT). This ensures that only registered and verified users can access protected resources and perform actions within the system.

> 🔐 Why it matters: Authentication protects sensitive user data and prevents unauthorized access to personal profiles, bookings, and listings.

---

### 2. **Authorization**
Role-based access control (RBAC) will be used to determine what each user (guest, host, or admin) can do. For example, only hosts can manage properties, while only guests can make bookings.

> 🔐 Why it matters: Authorization ensures users can only perform actions appropriate to their roles, preventing privilege abuse or data tampering.

---

### 3. **Rate Limiting**
Rate limiting will be applied to throttle excessive or suspicious requests from a single IP address or user account. This protects against brute-force attacks, spam, and denial-of-service (DoS) attempts.

> 🔐 Why it matters: Rate limiting helps maintain system stability and reduces the risk of automated attacks.

---

### 4. **Input Validation & Data Sanitization**
All user input will be validated and sanitized to prevent injection attacks (e.g., SQL injection, XSS). Validation will be enforced at both the frontend and backend levels.

> 🔐 Why it matters: Prevents malicious data from compromising the system, leaking data, or corrupting the database.

---

### 5. **Secure Payment Handling**
All payment-related operations will be handled through a trusted third-party gateway (e.g., Stripe or PayPal), ensuring compliance with industry standards like PCI DSS.

> 🔐 Why it matters: Protecting financial transactions is critical to avoid fraud, chargebacks, and loss of user trust.

---

### 6. **HTTPS Enforcement**
All communication with the API will be encrypted via HTTPS to prevent interception and man-in-the-middle attacks.

> 🔐 Why it matters: Encrypting data in transit protects login credentials, payment details, and personal information from being exposed.

---

### 7. **Error Handling & Logging**
Sensitive information will be excluded from error messages. Logs will be securely stored and monitored for suspicious behavior.

> 🔐 Why it matters: Proper error handling prevents information leakage, and secure logging supports incident detection and debugging.

---

Together, these security measures create a robust shield around the platform, safeguarding users, their data, and the integrity of the entire system.

## ⚙️ CI/CD Pipeline

### What is CI/CD?

**CI/CD** stands for **Continuous Integration** and **Continuous Deployment/Delivery**. It's a set of practices and tools that automate the process of testing, building, and deploying code. With CI/CD, every code change is automatically tested and deployed to ensure the application is always in a release-ready state.

### Why It's Important

Implementing CI/CD in this project ensures:
- Faster and more reliable deployments
- Early detection of bugs through automated testing
- Consistent and reproducible development environments
- Reduced manual errors and downtime during updates

This is especially valuable for a platform like an Airbnb clone, where user experience, data accuracy, and uptime are critical.

### Recommended Tools

- **GitHub Actions:** Automates testing and deployment workflows directly from the GitHub repository.
- **Docker:** Creates consistent environments across development, testing, and production.
- **Docker Compose:** Simplifies multi-container application setups (e.g., app, database, Redis).
- **Heroku / AWS / Render / Railway:** For automated deployments to production environments.
- **pytest / unittest:** For running automated tests during the CI phase.
- **Coverage.py:** Measures code test coverage to ensure quality.

By combining these tools, the CI/CD pipeline will help deliver robust, scalable, and secure software efficiently.
