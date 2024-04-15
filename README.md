# web-mission-3

Query 1:
``` sql
select username from users;
```

Query 2:
``` sql
select count(messages.from), users.username from messages inner join users on messages.from = users.id group by (users.username);
```

Query 3:
``` sql
with 

user_message as (
  select count(messages.to) as "number of received messages", users.username from messages 
  inner join users on messages.to = users.id 
  group by (users.username)
),

max_messages as (
  select max("number of received messages") from user_message
)

select * from user_message where "number of received messages"=(select * from max_messages);
```

Query 4:
``` sql
with user_message as (
  select count(messages.from), users.username from messages inner join users on messages.from = users.id group by (users.username)
)

select avg(count) as "average amount of messages" from user_message;
```
