## Supabase
link: https://drive.google.com/drive/folders/1BhFqWpMguHZpSV6Hl-tvFrZ-1aATHfUO?usp=drive_link
## SQL Queries

### Запрос 1
```sql
SELECT username FROM users;
```
### Запрос 2
```sql
SELECT 
    u.username,
    COUNT(m.id) AS "number of sent messages"
FROM 
    users u
LEFT JOIN 
    messages m ON u.id = m."from"
WHERE 
    u.id IN (1, 2)
GROUP BY 
    u.username;
```
### Запрос 3
```sql
SELECT 
    u.username,
    COUNT(m.id) AS "number of received messages"
FROM 
    users u
JOIN 
    messages m ON u.id = m."to"
GROUP BY 
    u.username
ORDER BY 
    COUNT(m.id) DESC
LIMIT 1;
```
### Запрос 4
```sql
SELECT 
    AVG(message_count) AS "average messages per user"
FROM (
    SELECT 
        u.id,
        COUNT(m.id) AS message_count
    FROM 
        users u
    LEFT JOIN 
        messages m ON u.id = m."from"
    WHERE
        u.id IN (1, 2)  -- только elizaveta и admin
    GROUP BY 
        u.id
) AS user_message_counts;
```
