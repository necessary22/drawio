Интернет магазин
![image](https://github.com/necessary22/drawio/assets/93242683/3dcb9490-c351-4d98-bb42-0e225c5083e9)
## Заполненные 
```sql
CREATE TABLE users (
	id INT PRIMARY KEY NOT NULL, 
	login varchar(16),
	password TEXT 
	);
INSERT INTO users (id, login, password)
VALUES
  (1, 'user1', 'password1'),
  (2, 'user2', 'password2'),
  (3, 'user3', 'password3'),
  (4, 'user4', 'password4'),
  (5, 'user5', 'password5');

CREATE TABLE category (
	id INT PRIMARY KEY NOT NULL, 
	title varchar(64) 
	);
INSERT INTO category (id, title)
VALUES
  (1, 'Electronics'),
  (2, 'Clothing'),
  (3, 'Books'),
  (4, 'Home and Kitchen'),
  (5, 'Sports and Outdoors');
  
CREATE TABLE product (
	id INT PRIMARY KEY NOT NULL,
	title TEXT, 
	description TEXT, 
	price numeric, 
	category_id INT, 
	constraint fk_category_category_id FOREIGN KEY (category_id) references category(id) 
	);
INSERT INTO product (id, title, description, price, category_id)
VALUES
  (1, 'Product 1', 'Description 1', 19.99, 1),
  (2, 'Product 2', 'Description 2', 29.99, 2),
  (3, 'Product 3', 'Description 3', 14.99, 1),
  (4, 'Product 4', 'Description 4', 39.99, 3),
  (5, 'Product 5', 'Description 5', 9.99, 2),
  (6, 'Product 6', 'Description 6', 24.99, 1),
  (7, 'Product 7', 'Description 7', 34.99, 2),
  (8, 'Product 8', 'Description 8', 49.99, 3),
  (9, 'Product 9', 'Description 9', 19.99, 1),
  (10, 'Product 10', 'Description 10', 59.99, 3);
	

CREATE TABLE profile (
	id INT PRIMARY KEY NOT NULL, 
	user_id INT, 
	first_name text, 
	second_name text, 
	number varchar(11), 
	email varchar(64), 
	birth_date date, 
	constraint fk_user_user_id FOREIGN KEY (user_id) references users(id) 
	);
INSERT INTO profile (id, user_id, first_name, second_name, number, email, birth_date)
VALUES
  (1, 1, 'John', 'Doe', '1234567890', 'john.doe@example.com', '1990-01-01'),
  (2, 2, 'Jane', 'Smith', '9876543210', 'jane.smith@example.com', '1985-05-15'),
  (3, 3, 'Alice', 'Johnson', '5551234567', 'alice.johnson@example.com', '1995-08-22'),
  (4, 4, 'Bob', 'Williams', '7778889999', 'bob.williams@example.com', '1980-11-10'),
  (5, 5, 'Eva', 'Brown', '1112223333', 'eva.brown@example.com', '1992-04-30');

CREATE TABLE purchase_history (
	id INT PRIMARY KEY NOT NULL, 
	price numeric, 
	date_buy DATE, 
	product_id INT,
	profile_id INT, 
	constraint fk_profile_profile_id FOREIGN KEY (profile_id) references profile(id),
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);
INSERT INTO purchase_history (id, price, date_buy, product_id, profile_id)
VALUES
  (1, 50.00, '2023-01-01', 1, 1),
  (2, 30.00, '2023-02-05', 2, 2),
  (3, 25.50, '2023-03-10', 3, 2),
  (4, 40.00, '2023-04-15', 1, 1),
  (5, 60.00, '2023-05-20', 4, 3),
  (6, 15.00, '2023-06-25', 2, 4),
  (7, 55.50, '2023-07-30', 5, 5),
  (8, 33.75, '2023-08-04', 3, 3),
  (9, 48.20, '2023-09-09', 4, 4),
  (10, 22.30, '2023-10-14', 5, 5);

CREATE TABLE cart (
	id INT PRIMARY KEY NOT NULL, 
	product_id INT,
	profile_id INT,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id), 
	constraint fk_profile_profile_id FOREIGN KEY (profile_id) references profile(id) 
	);
INSERT INTO cart (id, product_id, profile_id)
VALUES
  (1, 1, 1),
  (2, 2, 1),
  (3, 3, 2),
  (4, 1, 3),
  (5, 4, 3),
  (6, 2, 4),
  (7, 5, 4),
  (8, 3, 5),
  (9, 4, 5),
  (10, 5, 1);

CREATE TABLE feedback (
	id INT PRIMARY KEY NOT NULL,
	product_id INT,
	description TEXT,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);
INSERT INTO feedback (id, product_id, description)
VALUES
  (1, 1, 'Great product!'),
  (2, 3, 'Fast shipping, excellent service.'),
  (3, 2, 'Quality could be better.'),
  (4, 4, 'Satisfied with the purchase.'),
  (5, 1, 'Would buy again.'),
  (6, 5, 'Not what I expected.'),
  (7, 3, 'Product arrived damaged.'),
  (8, 2, 'Average product.'),
  (9, 4, 'Excellent customer support.'),
  (10, 5, 'Product as described.');

	
CREATE TABLE status (
	id INT PRIMARY KEY NOT NULL,
	description TEXT
	);
INSERT INTO status (id, description)
VALUES
  (1, 'Pending'),
  (2, 'Processing'),
  (3, 'Shipped');
	
CREATE TABLE orders (
	id INT PRIMARY KEY NOT NULL,
	user_id INT,
	status_id INT,
	total_cost numeric,
	date DATE,
	constraint fk_users_user_id FOREIGN KEY (user_id) references users(id),
	constraint fk_status_status_id FOREIGN KEY (status_id) references status(id)
	);
INSERT INTO orders (id, user_id, status_id, total_cost, date)
VALUES
  (1, 1, 1, 100.00, '2023-01-01'),
  (2, 2, 2, 150.50, '2023-02-02'),
  (3, 3, 1, 200.75, '2023-03-03'),
  (4, 4, 3, 75.25, '2023-04-04'),
  (5, 5, 2, 120.00, '2023-05-05'),
  (6, 1, 3, 90.50, '2023-06-06'),
  (7, 2, 1, 180.25, '2023-07-07'),
  (8, 3, 2, 210.75, '2023-08-08'),
  (9, 4, 3, 95.00, '2023-09-09'),
  (10, 5, 1, 130.50, '2023-10-10');

CREATE TABLE orders_details (
	id INT PRIMARY KEY NOT NULL,
	order_id INT,
	product_id INT,
	amount numeric,
	constraint fk_orders_order_id FOREIGN KEY (order_id) references orders(id),
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);
INSERT INTO orders_details (id, order_id, product_id, amount)
VALUES
  (1, 1, 1, 2),
  (2, 1, 2, 1),
  (3, 2, 3, 3),
  (4, 2, 4, 1),
  (5, 3, 5, 2),
  (6, 3, 6, 1),
  (7, 4, 7, 2),
  (8, 4, 8, 1),
  (9, 5, 9, 3),
  (10, 5, 10, 2);


CREATE TABLE photo (
	id INT PRIMARY KEY NOT NULL,
	path TEXT,
	product_id INT,
	main_picture BOOLEAN,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);
INSERT INTO photo (id, path, product_id, main_picture)
VALUES
  (1, '/images/photo1.jpg', 1, true),
  (2, '/images/photo2.jpg', 1, false),
  (3, '/images/photo3.jpg', 2, true),
  (4, '/images/photo4.jpg', 2, false),
  (5, '/images/photo5.jpg', 3, true),
  (6, '/images/photo6.jpg', 3, false),
  (7, '/images/photo7.jpg', 4, true),
  (8, '/images/photo8.jpg', 4, false),
  (9, '/images/photo9.jpg', 5, true),
  (10, '/images/photo10.jpg', 5, false);
```
# Triggers

## 1. Триггер для обновления общей стоимости заказа при изменении его деталей (orders_details):
```sql
CREATE OR REPLACE FUNCTION update_order_total_cost()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE orders
    SET total_cost = (
        SELECT SUM(product.price * orders_details.amount)
        FROM orders_details
        INNER JOIN product ON orders_details.product_id = product.id
        WHERE orders_details.order_id = NEW.order_id
    )
    WHERE id = NEW.order_id;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_order_cost_trigger
AFTER INSERT OR UPDATE OR DELETE ON orders_details
FOR EACH ROW
EXECUTE FUNCTION update_order_total_cost();
```
## Этот триггер обновляет общую стоимость заказа (total_cost) в таблице orders, когда происходят изменения в таблице orders_details (например, при добавлении, обновлении или удалении деталей заказа).

## Пример для триггера 
```sql
-- Предположим, мы изменили количество продукта с id = 2 в заказе с order_id = 1
UPDATE orders_details
SET amount = 5
WHERE order_id = 1 AND product_id = 2;
```

## 1.1 Триггер для автоматического обновления общей суммы покупок пользователя при добавлении записи в историю покупок:
```sql
CREATE OR REPLACE FUNCTION update_user_total_purchase_amount()
RETURNS TRIGGER AS $$
BEGIN
    UPDATE orders
    SET total_cost = total_cost + NEW.price
    WHERE id = NEW.profile_id;
    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER update_user_total_purchase_amount_trigger
AFTER INSERT ON purchase_history
FOR EACH ROW
EXECUTE FUNCTION update_user_total_purchase_amount();
```
## Проверка 
```sql
-- Добавьте новую запись в таблицу purchase_history
INSERT INTO purchase_history (id, price, date_buy, product_id, profile_id)
VALUES (11, 75.50, '2023-11-15', 6, 2);

-- Проверьте обновление общей суммы покупок для id = 2
SELECT total_cost FROM orders WHERE id = 2;
```

## (не работает) 2. Триггер для проверки количества товара в корзине перед оформлением заказа:
```sql
CREATE OR REPLACE FUNCTION check_cart_items()
RETURNS TRIGGER AS $$
DECLARE
    cart_count INTEGER;
BEGIN
    SELECT COUNT(*) INTO cart_count
    FROM cart
    WHERE profile_id = NEW.profile_id;

    IF cart_count = 0 THEN
        RAISE EXCEPTION 'Невозможно оформить заказ. Корзина пуста.';
    END IF;

    RETURN NEW;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER check_cart_items_trigger
BEFORE INSERT ON orders
FOR EACH ROW
EXECUTE FUNCTION check_cart_items();
```
## Этот триггер проверяет, есть ли товары в корзине (cart), прежде чем будет создан новый заказ (orders). Если корзина пуста при попытке создания заказа, то будет сгенерировано исключение.



## 3. Триггер для запрета удаления категории, если у этой категории есть продукты:
```sql
-- Создание триггера для временной таблицы
CREATE OR REPLACE FUNCTION prevent_category_deletion()
RETURNS TRIGGER AS $$
BEGIN
    IF EXISTS (SELECT 1 FROM category WHERE id = OLD.id) THEN
        RAISE EXCEPTION 'у этой категории есть связанные продукты';
    END IF;
    RETURN OLD;
END;
$$ LANGUAGE plpgsql;

CREATE TRIGGER prevent_category_deletion_trigger
BEFORE DELETE ON category
FOR EACH ROW
EXECUTE FUNCTION prevent_category_deletion();
```
## Этот триггер предназначен для предотвращения удаления категории, если у этой категории есть связанные продукты. 

## Пример для триггера
```sql
-- Попытка удалить категорию с продуктами
DELETE FROM test_category_product WHERE category_id = 1;

```



## Голые таблицы
```sql
CREATE TABLE users (
	id INT PRIMARY KEY NOT NULL, 
	login varchar(16),
	password TEXT 
	);
	
CREATE TABLE category (
	id INT PRIMARY KEY NOT NULL, 
	title varchar(64) 
	);
	
CREATE TABLE product (
	id INT PRIMARY KEY NOT NULL,
	title TEXT, 
	description TEXT, 
	price numeric, 
	category_id INT, 
	constraint fk_category_category_id FOREIGN KEY (category_id) references category(id) 
	);
	
CREATE TABLE purchase_history (
	id INT PRIMARY KEY NOT NULL, 
	price numeric, 
	date_buy DATE, 
	product_id INT,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);

CREATE TABLE profile (
	id INT PRIMARY KEY NOT NULL, 
	user_id INT, 
	first_name text, 
	second_name text, 
	number varchar(11), 
	email varchar(64), 
	birth_date date, 
	history_id INT,
	constraint fk_purchase_history_history_id FOREIGN KEY (history_id) references purchase_history(id),
	constraint fk_user_user_id FOREIGN KEY (user_id) references users(id) 
	);
	
CREATE TABLE cart (
	id INT PRIMARY KEY NOT NULL, 
	product_id INT,
	profile_id INT,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id), 
	constraint fk_profile_profile_id FOREIGN KEY (profile_id) references profile(id) 
	);
	
CREATE TABLE feedback (
	id INT PRIMARY KEY NOT NULL,
	product_id INT,
	description TEXT,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);
	
CREATE TABLE status (
	id INT PRIMARY KEY NOT NULL,
	description TEXT
	);
	
CREATE TABLE orders (
	id INT PRIMARY KEY NOT NULL,
	user_id INT,
	status_id INT,
	total_cost numeric,
	date DATE,
	constraint fk_users_user_id FOREIGN KEY (user_id) references users(id),
	constraint fk_status_status_id FOREIGN KEY (status_id) references status(id)
	);

CREATE TABLE orders_details (
	id INT PRIMARY KEY NOT NULL,
	order_id INT,
	product_id INT,
	amount numeric,
	constraint fk_oreders_order_id FOREIGN KEY (order_id) references orders(id),
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);

CREATE TABLE photo (
	id INT PRIMARY KEY NOT NULL,
	path TEXT,
	product_id INT,
	main_picture BOOLEAN,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);
```

