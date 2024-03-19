# SQL and Databases 

1. Please translate the following resources using your favourite method (mine is firefox plugin): 
- [DB 1](https://github.com/DonatasNoreika/Python-pamokos/wiki/SQL-1-u%C5%BEduotys)
- [DB 2](https://github.com/DonatasNoreika/Python-pamokos/wiki/SQL-2-u%C5%BEduotys)
- [DB 3](https://github.com/DonatasNoreika/Python-pamokos/wiki/SQL-3-u%C5%BEduotys)
- [DB 4](https://github.com/robotautas/kursas/blob/master/DB/db4/uzduotis.md)

2. 
- Design databases (on paper, using https://draw.io or code comments) ) for the following scenarios. In each case, we outline the tables you should create and the properties each table should have
- We outline the tables that you should create. 
- Don't forget about database constraints! 
- Afterwards, implement your designs via SQL commands (CREATE TABLE ... ) think about a few ways put data into these tables and interesting things to query from this table.

### Online Course Platform
- Users: (user_id, username, email, password)
- Courses: (course_id, title, description, instructor_id)	
- Enrollments: (enrollment_id, user_id, course_id, completion_status)

### E-commerce Store
- Products: (product_id, name, description, price, stock_quantity)
- Categories: (category_id, name) (Optional - for product categorization)	
- Orders: (order_id, user_id, order_date, total_price, status)	
- Order_Items: (order_item_id, order_id, product_id, quantity, price)

### Social Media Platform
- Users (user_id, username, email, password)	
- Posts (post_id, user_id, content, timestamp)	
- Follows (follower_id, following_id) (Optional - for a follow relationship)	
- Likes (user_id, post_id) (Optional - for likes on posts)

### Movie Database:
- Movies (movie_id, title, release_date, director, genre)	
- Actors (actor_id, name, birth_date)
- Cast (movie_id, actor_id, character_name)
- Reviews (review_id, user_id, movie_id, rating, comment) (Optional - for user reviews)
