How many users are there?
=>	50
	SELECT COUNT(*) FROM users

What are the 5 most expensive items?
=>	"9984"
	"9859"
	"9790"
	"9390"
	"9341"
	SELECT price FROM items ORDER BY price DESC LIMIT 5

What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?)
=>	"1496"
	SELECT price FROM items WHERE category = "Books" ORDER BY price ASC LIMIT 1

=>	No, still "1496"
	SELECT price FROM items WHERE category LIKE "%book%" ORDER BY price ASC LIMIT 1	

Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address?
=>	"Corrine Little"
	SELECT first_name, last_name FROM users
	INNER JOIN addresses ON users.id = addresses.user_id
	WHERE street = "6439 Zetta Hills"

Correct Virginie Mitchell's address to "New York, NY, 10108".
=>	UPDATE addresses SET city = "New York" , zip = "10108" WHERE id = 41;

How much would it cost to buy one of each tool?
=>	"46477"
	SELECT SUM(price) FROM items WHERE category LIKE "%tool%"; 

How many total items did we sell?
=>	"2125"
	SELECT SUM(quantity) FROM orders

How much was spent on books?
=>	"1081352"
	SELECT SUM(items.price * orders.quantity) FROM orders
	INNER JOIN items ON items.id = orders.item_id
	WHERE items.category LIKE "%book%"

Simulate buying an item by inserting a User for yourself and an Order for that User.
=>
	INSERT INTO users (id, first_name, last_name, email) VALUES (51, "brian", "baumgartner", "b@b.com")
	
	INSERT INTO orders (id, user_id, item_id, quantity, created_at) VALUES (378, 51, 91, 1, CURRENT_TIMESTAMP)

What item was ordered most often? Grossed the most money?
=>	item_id [10, 46, 65]
	SELECT item_id, COUNT(item_id) count FROM orders GROUP BY item_id ORDER BY count DESC

=>	item_id = 46
	SELECT id, price FROM items WHERE id IN (10, 46, 65) ORDER BY price DESC LIMIT 1

What user spent the most?
=> "639386"

SELECT user_id, SUM(items.price * orders.quantity) orderPrice FROM orders
INNER JOIN items ON items.id = orders.item_id
GROUP BY user_id ORDER BY orderPrice DESC limit 1











