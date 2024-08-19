
# Understanding the Sakila Database

## Introduction

The Sakila database is a well-known sample database designed for learning and practicing SQL, relational database design, and concepts like normalization. It is widely used by developers and database administrators to explore SQL features and best practices in a real-world scenario. The database models a DVD rental store, providing a practical example of how a business might organize and manage data.

## ER Diagram

Below is the Entity-Relationship (ER) diagram of the Sakila database, which visually represents the relationships between the various entities (tables) in the database.

![Sakila ER Diagram](./sakila-er-diagram.png)

## Key Entities and Relationships

### 1. **Film**
   - **Attributes**: `film_id`, `title`, `description`, `release_year`, `language_id`, `original_language_id`, `rental_duration`, `rental_rate`, `length`, `replacement_cost`, `rating`, `special_features`, `last_update`.
   - **Relationships**: 
     - **Inventory**: A film can have multiple copies in the inventory.
     - **Category**: Each film is associated with one or more categories through the `film_category` table.
     - **Actor**: Actors are linked to films through the `film_actor` table, representing the many-to-many relationship between films and actors.

### 2. **Actor**
   - **Attributes**: `actor_id`, `first_name`, `last_name`, `last_update`.
   - **Relationships**: 
     - **Film**: Connected to films through the `film_actor` table. This many-to-many relationship allows each actor to appear in multiple films, and each film can feature multiple actors.

### 3. **Inventory**
   - **Attributes**: `inventory_id`, `film_id`, `store_id`, `last_update`.
   - **Relationships**: 
     - **Film**: Links directly to the `film` table to represent which films are available in the inventory.
     - **Store**: Each inventory item is associated with a specific store.
     - **Rental**: Inventory items are rented out to customers, linking the inventory to rentals.

### 4. **Customer**
   - **Attributes**: `customer_id`, `store_id`, `first_name`, `last_name`, `email`, `address_id`, `activebool`, `create_date`, `last_update`.
   - **Relationships**: 
     - **Rental**: Customers rent inventory items, creating a relationship between the customer and rental tables.
     - **Payment**: Customers make payments for their rentals, linking the customer to the payment table.
     - **Store**: Customers are associated with a specific store.

### 5. **Rental**
   - **Attributes**: `rental_id`, `rental_date`, `inventory_id`, `customer_id`, `return_date`, `staff_id`, `last_update`.
   - **Relationships**: 
     - **Inventory**: Rentals involve specific inventory items.
     - **Customer**: Each rental is made by a customer.
     - **Staff**: Staff members handle the rental process.

### 6. **Payment**
   - **Attributes**: `payment_id`, `customer_id`, `staff_id`, `rental_id`, `amount`, `payment_date`.
   - **Relationships**: 
     - **Customer**: Payments are made by customers.
     - **Rental**: Payments are linked to specific rentals.
     - **Staff**: Staff members process the payments.

### 7. **Staff**
   - **Attributes**: `staff_id`, `first_name`, `last_name`, `address_id`, `email`, `store_id`, `active`, `username`, `password`, `last_update`.
   - **Relationships**: 
     - **Store**: Each staff member works at a specific store.
     - **Rental**: Staff members manage rentals.
     - **Payment**: Staff members process payments.

### 8. **Store**
   - **Attributes**: `store_id`, `manager_staff_id`, `address_id`, `last_update`.
   - **Relationships**: 
     - **Staff**: Stores have a manager and other staff members.
     - **Inventory**: Stores hold inventory items.
     - **Customer**: Customers are associated with a specific store.

## Database Normalization

The Sakila database follows the principles of normalization to minimize redundancy and improve data integrity. Key normalization concepts include:

- **First Normal Form (1NF)**: All tables are organized in such a way that each column contains atomic values, and there are no repeating groups.
- **Second Normal Form (2NF)**: All non-key attributes are fully dependent on the primary key.
- **Third Normal Form (3NF)**: All attributes are dependent only on the primary key, ensuring no transitive dependency.

## SQL Concepts Illustrated by Sakila

The Sakila database is an excellent resource for practicing various SQL concepts, including:

- **Joins**: Demonstrating inner, left, right, and full joins using the relationships between tables.
- **Subqueries**: Practicing nested queries to retrieve specific data.
- **Group By and Aggregation**: Using `GROUP BY` and aggregate functions like `COUNT`, `SUM`, and `AVG` on the data.
- **Views**: Creating views for complex queries.
- **Stored Procedures and Triggers**: Implementing stored procedures and triggers for database automation.

## Sample Queries

### 1. Retrieve All Movies in the Action Category
```sql
SELECT f.title
FROM film f
JOIN film_category fc ON f.film_id = fc.film_id
JOIN category c ON fc.category_id = c.category_id
WHERE c.name = 'Action';
```

### 2. Find the Top 5 Most Rented Movies
```sql
SELECT f.title, COUNT(r.rental_id) AS rental_count
FROM film f
JOIN inventory i ON f.film_id = i.film_id
JOIN rental r ON i.inventory_id = r.inventory_id
GROUP BY f.title
ORDER BY rental_count DESC
LIMIT 5;
```

### 3. List All Staff Members and Their Assigned Stores
```sql
SELECT s.first_name, s.last_name, st.store_id
FROM staff s
JOIN store st ON s.store_id = st.store_id;
```

## Summary

The Sakila database offers a comprehensive example of a well-designed relational database, making it an ideal tool for learning and mastering SQL. By exploring its structure and practicing with its data, you can gain a deep understanding of SQL concepts, relational database design, and the practical application of normalization principles.

## Further Reading

For a deeper dive into the Sakila database, consider exploring the official [Sakila documentation](https://dev.mysql.com/doc/sakila/en/).
