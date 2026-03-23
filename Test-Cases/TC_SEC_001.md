TC_SEC_001 – SQL injection attempt

Module: Security

Steps:
1. Navigate to a login or search field
2. Enter a SQL injection string (e.g., ' OR 1=1 --)
3. Submit the form

Expected Result:
System blocks the input and does not expose data.

Priority: High
Status: Not executed
