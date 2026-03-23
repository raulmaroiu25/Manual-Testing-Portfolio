# SQL Queries for QA Testing

This document contains essential SQL queries commonly used by QA engineers to validate data, check backend consistency, and support manual testing activities.  
These queries cover registration, login, profile management, search, and data validation scenarios.

---

# 📌 1. Basic SQL Queries

1.1 Retrieve all users
Useful for verifying that new users appear in the database after registration.

SELECT * FROM users;


1.2 Find a user by email
Used to confirm that a specific user exists.

SELECT * FROM users
WHERE email = 'test@example.com';


1.3 Check if a user already exists (duplicate validation)
Useful for testing registration scenarios.

SELECT COUNT(*) AS user_count
FROM users
WHERE email = 'test@example.com';


1.4 Validate login credentials (email + password hash)
Used to confirm backend authentication logic.

SELECT * FROM users
WHERE email = 'student@example.com'
AND password_hash = 'hashed_value';


1.5 Get all users ordered by registration date
Useful for verifying sorting and recent registrations.

SELECT * FROM users
ORDER BY created_at DESC;


1.6 Search users by partial name
Used to test search functionality at database level.

SELECT * FROM users
WHERE name LIKE '%john%';


1.7 Detect duplicate emails in the system
Useful for negative testing and data integrity checks.

SELECT email, COUNT(*) AS occurrences
FROM users
GROUP BY email
HAVING COUNT(*) > 1;


1.8 Validate profile information update
Used after testing profile edit functionality.

SELECT name, phone, address
FROM users
WHERE user_id = 123;

2. Advanced SQL Queries

2.1 Users who never logged in
Good for analytics and backend validation.

SELECT * FROM users
WHERE last_login IS NULL;


2.2 Users registered in the last 7 days
Useful for verifying time‑based filters.

SELECT * FROM users
WHERE created_at >= NOW() - INTERVAL 7 DAY;


2.3 Count users by country
Useful for testing aggregated data.

SELECT country, COUNT(*) AS total_users
FROM users
GROUP BY country;


2.4 Get last 5 registered users
Quick check for recent activity.

SELECT * FROM users
ORDER BY created_at DESC
LIMIT 5;


These SQL queries cover the most common scenarios a QA tester encounters:

validating registration

checking login

verifying profile updates

detecting duplicates

testing search

analyzing backend data
