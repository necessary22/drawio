Интернет магазин
![image](https://github.com/necessary22/drawio/assets/93242683/3dcb9490-c351-4d98-bb42-0e225c5083e9)



CREATE TABLE users (
	id INT PRIMARY KEY NOT NULL,
	login varchar(16)
	password TEXT
	);
	
CREATE TABLE categories (
	id INT PRIMARY KEY NOT NULL,
	title varchar(64)
	);
	


CREATE TABLE product (
	id INT PRIMARY KEY NOT NULL,
	title TEXT,
	discription TEXT,
	price DOUBLE,
	category_id INT,
	constraint fk_category_category_id FOREIGN KEY (category_id) references category(id),
	);

CREATE TABLE purchase_history (
	id INT PRIMARY KEY NOT NULL,
	price DOUBLE,
	date_buy DATE,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	);

CREATE TABLE cart (
	id INT PRIMARY KEY NOT NULL,
	constraint fk_product_product_id FOREIGN KEY (product_id) references product(id)
	constraint fk_profile_profile_id FOREIGN KEY (profile_id) references profile(id)
	);

CREATE TABLE profile (
	id INT PRIMARY KEY NOT NULL,
	user_id INT,
	first_name text,
	second_name text,
	number varchar(11),
	email varchar(64),
	birth_date date,
	history_id INT
	constraint fk_purchase_history_history_id FOREIGN KEY (history_id) references purchase_history(id)
	constraint fk_user_user_id FOREIGN KEY (user_id) references user(id)
	);
	

