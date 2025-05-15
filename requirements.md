## 📋 Project Requirements

### 1. **Database Schema**

The application uses a **relational database** with the following tables/entities:

#### 🧑 User
- **Fields:** `user_id`, `first_name`, `last_name`, `email`, `password_hash`, `phone_number`, `role`, `created_at`
- **Constraints:**
  - `email` must be unique
  - Non-null for essential fields
  - `role` is an ENUM (`guest`, `host`, `admin`)

#### 🏠 Property
- **Fields:** `property_id`, `host_id`, `name`, `description`, `location`, `price_per_night`, `created_at`, `updated_at`
- **Constraints:**
  - `host_id` is a foreign key referencing `User(user_id)`
  - Non-null for essential fields

#### 📅 Booking
- **Fields:** `booking_id`, `property_id`, `user_id`, `start_date`, `end_date`, `total_price`, `status`, `created_at`
- **Constraints:**
  - Foreign keys: `property_id` → `Property`, `user_id` → `User`
  - `status` is an ENUM (`pending`, `confirmed`, `cancelled`, `completed`)

#### 💳 Payment
- **Fields:** `payment_id`, `booking_id`, `amount`, `payment_date`, `payment_method`
- **Constraints:**
  - `booking_id` is a foreign key referencing `Booking(booking_id)`

#### ⭐ Review
- **Fields:** `review_id`, `property_id`, `user_id`, `rating`, `comment`, `created_at`
- **Constraints:**
  - Foreign keys: `property_id` → `Property`, `user_id` → `User`
  - `rating` must be between 1 and 5

#### 💬 Message
- **Fields:** `message_id`, `sender_id`, `recipient_id`, `message_body`, `sent_at`
- **Constraints:**
  - `sender_id` and `recipient_id` are foreign keys referencing `User(user_id)`

---

### 2. **Data Types & Constraints**
- UUIDs used as primary keys for uniqueness
- ENUM types used for `role` and `status` fields
- Non-null constraints on essential fields
- Unique constraint on `email` in the `User` table

---

### 3. **Indexing**
- Primary keys are automatically indexed
- Additional indexes include:
  - `email` in the `User` table
  - `property_id` in `Property` and `Booking`
  - `booking_id` in `Booking` and `Payment`

---

### 4. **Entity Relationships**
- A **User** can host multiple **Properties**
- A **User** can make multiple **Bookings**
- Each **Booking** is linked to one **Property** and one **User**
- A **Booking** has one associated **Payment**
- A **User** can leave multiple **Reviews** for various **Properties**
- **Users** can message each other using the **Message** system

---

### 5. **Functionality Overview**
- User registration and role management (guest, host, admin)
- Host property listings: creation, update, and deletion
- Booking management with price calculation and status tracking
- Payment processing linked to bookings
- Review system for properties
- Messaging between users

---

### 6. **Installation & Setup**
- Install PostgreSQL or your preferred RDBMS
- Configure environment variables:
  ```env
  DATABASE_URL=postgresql://<user>:<password>@localhost:5432/<dbname>
  ```
- Run migrations:
  ```bash
  # Example with Sequelize or Prisma
  npx prisma migrate dev
  ```
- Start the server:
  ```bash
  npm run dev
  ```

---

### 7. **Contribution Guidelines**
- Use consistent coding standards (ESLint, Prettier, or PEP8)
- Fork the repo and create a new branch for each feature:
  ```bash
  git checkout -b feature/your-feature-name
  ```
- Test your code before pushing
- Open a pull request with clear description and reference to any related issue
