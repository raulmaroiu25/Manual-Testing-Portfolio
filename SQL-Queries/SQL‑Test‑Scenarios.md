# SQL Test Scenarios for QA

This document contains SQL-based test scenarios used to validate backend data for core functionalities such as Login, Registration, Search, and Profile Management.  
These scenarios help ensure that the database reflects the expected behavior after UI or API actions.

---

📌 1. Registration – SQL Test Scenarios

Scenario 1: Verify that a new user is created in the database
Action: Register a new user in the application  

SQL Validation:
SELECT * FROM users
WHERE email = 'newuser@example.com';

Expected Result: One record is returned with correct name, email, and creation date.

---

Scenario 2: Verify that duplicate emails are not allowed
Action: Try registering with an email that already exists
SQL Validation:

SELECT COUNT(*) AS duplicates
FROM users
WHERE email = 'existing@example.com';

Expected Result: duplicates = 1 (no new record created)

---

Scenario 3: Validate password hashing
Action: Register a user
SQL Validation:

SELECT password_hash FROM users
WHERE email = 'newuser@example.com';

Expected Result: password_hash is NOT equal to the plain password.

---

📌 2. Login – SQL Test Scenarios

Scenario 4: Validate login with correct credentials
Action: Log in with valid email + password
SQL Validation:

SELECT * FROM users
WHERE email = 'user@example.com';

Expected Result: User exists AND last_login timestamp updates.

---

Scenario 5: Validate login attempt with incorrect password
Action: Log in with wrong password
SQL Validation:

SELECT failed_attempts FROM users
WHERE email = 'user@example.com';

Expected Result: failed_attempts increases by 1 (if system tracks it)

---

Scenario 6: Check if locked accounts are flagged
Action: Enter wrong password multiple times
SQL Validation:

SELECT is_locked FROM users
WHERE email = 'user@example.com';

Expected Result: is_locked = TRUE (if lockout policy exists)

---

📌 3. Search – SQL Test Scenarios

Scenario 7: Validate search results match database records
Action: Search for “john” in UI
SQL Validation:

SELECT * FROM users
WHERE name LIKE '%john%';

Expected Result: UI results match SQL results exactly.

---

Scenario 8: Validate empty search returns no results
Action: Search with empty input
SQL Validation:

SELECT * FROM users
WHERE name LIKE '%%';

Expected Result: Should return all users, but UI should block this.

---

Scenario 9: Validate search for non-existing user
Action: Search for “xyz123”
SQL Validation:

SELECT * FROM users
WHERE name LIKE '%xyz123%';

Expected Result: 0 rows returned.

📌 4. Profile Management – SQL Test Scenarios

Scenario 10: Validate profile update is saved in DB
Action: Update name, phone, address
SQL Validation:

SELECT name, phone, address
FROM users
WHERE user_id = 123;

Expected Result: Updated values appear in DB.

---

Scenario 11: Validate profile picture upload
Action: Upload a new profile picture
SQL Validation:

SELECT profile_picture_url
FROM users
WHERE user_id = 123;

Expected Result: URL/path is updated.

---

Scenario 12: Validate invalid file upload does NOT update DB
Action: Upload unsupported file
SQL Validation:

SELECT profile_picture_url
FROM users
WHERE user_id = 123;

Expected Result: Value remains unchanged.

📌 5. Data Integrity – SQL Test Scenarios

Scenario 13: Check for duplicate users

SELECT email, COUNT(*) AS duplicates
FROM users
GROUP BY email
HAVING COUNT(*) > 1;

Expected Result: No duplicates.

---

Scenario 14: Check for users without required fields

SELECT * FROM users
WHERE email IS NULL OR name IS NULL;

Expected Result: 0 records.

---

Scenario 15: Validate timestamps

SELECT created_at, updated_at
FROM users
WHERE user_id = 123;

Expected Result: updated_at > created_at after profile update.
