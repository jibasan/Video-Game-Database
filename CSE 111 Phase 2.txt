CREATE TABLE IF NOT EXISTS 'VideoGame' (	
	v_GameKey		INTEGER		NOT NULL, 	//PRIMARY KEY
	v_ProdKey		INTEGER		NOT NULL,
	v_GameName		VARCHAR (50)	NOT NULL,
	v_devkey		INTEGER		NOT NULL,
	v_pubkey		INTEGER		NOT NULL,
	v_Genre			VARCHAR (20)	NOT NULL,
	v_platkey		INTEGER		NOT NULL,
	v_YearReleased		DATE		NOT NULL,
	v_Rating		VARCHAR (30)	NOT NULL,
	v_Score			INTEGER		NOT NULL,
	v_Price			DOUBLE		NOT NULL,


CREATE TABLE Customer (
	c_customerKey		INTEGER		NOT NULL,	//PRIMARY KEY
	c_Name			VARCHAR	(30)	NOT NULL,
	c_regionkey		VARCHAR	(30)	NOT NULL,
	C_nationkey		VARCHAR	(30)	NOT NULL,
	c_Address		VARCHAR		NOT NULL,
	c_PhoneNumber		INT		NOT NULL,
	c_Email			VARCHAR		NOT NULL,
	c_cokey 		INTEGER		NOT NULL


CREATE TABLE Store (
	s_storekey		INTEGER		NOT NULL,	//PRIMARY KEY
	s_cokey			INTEGER		NOT NULL,
	s_address 		VARCHAR		NOT NULL,
	s_nationkey		INTEGER		NOT NULL,		
	s_ProdKey		INTEGER		NOT NULL,
	s_Name			VARCHAR		NOT NULL,
	s_Available		INT		NOT NULL,
	s_Sold			INT		NOT NULL


CREATE TABLE Collection (
	co_cokey 		INTEGER		NOT NULL,	//PRIMARY KEY
	co_ProdKey		INTEGER		NOT NULL,
	Co_quantity		INTEGER		NOT NULL,
	co_price		INTEGER		NOT NULL //Price


CREATE TABLE Developer (
	d_devkey		INTEGER		NOT NULL,	//PRIMARY KEY
	d_name			VARCHAR		NOT NULL,
	d_nationkey		VARCHAR		NOT NULL,
	d_networth		DOUBLE		NOT NULL,
	d_address		VARCHAR		NOT NULL


CREATE TABLE Publisher
	p_pubkey		INTEGER		NOT NULL,	//PRIMARY KEY
	p_name			VARCHAR		NOT NULL,
	p_nationkey		VARCHAR		NOT NULL,
	p_address		VARCHAR		NOT NULL


CREATE Table Platform
	pl_platkey		INTEGER		NOT NULL,	//PRIMARY KEY
	pl_ProdKey		VARCHAR 	NOT NULL,
	pl_name			VARCHAR		NOT NULL,
	pl_price		DOUBLE 		NOT NULL

CREATE Table Nation
	n_nationkey		INTEGER		NOT NULL,	//PRIMARY KEY
	n_regionkey		INTEGER		NOT NULL,
	n_name			VARCHAR		NOT NULL
	
CREATE Table Region
	r_regionkey		INTEGER		NOT NULL,	//PRIMARY KEY
	r_name			VARCHAR		NOT NULL	




//Sample Queries 

1.
INSERT INTO ‘Platform’ (‘pl_platkey, pl_ProdKey,  pl_name, pl_year’ ) VALUES
	(1, 1, ‘PC’ , ‘1981’ ),
	(2, 2,  ‘Playstation’ , ‘1994’),
	(3, 3, ‘Playstation 2’ , ‘2000’),
	(4, 4, ‘Playstation 3’ , ‘2006’),
	(5, 5, ‘Playstation 4’ , ‘2013’),
	(6,6,  ‘Xbox’ , ‘2001’),
	(7, 7, ‘Xbox 360’ , ‘2005’),
	(8, 8, ‘Xbox One’ , ‘2013’),
	(9, 9, ‘Nintendo DS’ , ‘2004’),
	(10, 10, ‘Nintendo 3DS’ , ‘2011’),
	(11, 11,  ‘Nintendo Wii’ , ‘2006’),
	(12, 12, ‘Wii U’ , ‘2012’),
	(13, 13, ‘Nintendo Switch’ , ‘2017’),
	(14, 14, ‘Nintendo Gamecube’ , ‘2001’)


2. Insert “Call of Duty: Modern Warfare” for PC into database
INSERT INTO VideoGame (v_ProdKey, v_GameName, v_devkey, v_pubkey, v_Genre, v_platkey, v_YearReleased, v_Rating, v_Score, v_Price)
values(5, ‘Call of Duty: Modern Warfare’, 3, 4, ‘FPS’, 1, 2019, ‘M’, .8, 59.99)



1. Show all the available games
SELECT v_GameName
FROM VideoGame	




2. Find the amount of games available on the PC platform
SELECT COUNT(v_GameName)
FROM VideoGame v
WHERE v_PlatKey = 1



3. list all games published by Nintendo
SELECT v_GameName
FROM VideoGame v, Developer d
WHERE v_DevKey == d_devkey AND
d_devkey = 1


4. List all the games that start with super
SELECT v_GameName	
FROM VideoGame v
WHERE v_GameName LIKE "Super%"




5. List all games made in 2001
SELECT v_GameName
FROM VideoGame
WHERE v_YearReleased LIKE "2001%"



6. List all games that cost more than $30
SELECT v_GameName	
FROM VideoGame
WHERE v_Price >= 30


7. List all games with a rating of “M”
SELECT v_GameName
FROM VideoGame
WHERE v_Rating = "M"


8.List all the FPS that are available for the PC
SELECT v_GameName	
FROM VideoGame
WHERE v_Genre = ‘FPS’ AND
v_Platkey = 1

9. Average rating of “Grand Theft Auto” games
SELECT AVG(v_Score)
FROM VideoGame
WHERE v_GameName LIKE "Grand Theft Auto%"


10. Find the lowest price game available for the PlayStation and list the name
SELECT v_GameName, MIN(v_Price)
FROM VideoGame v
WHERE v_PlatKey = 2


11. Find the highest price available game released in 2005


SELECT v_GameName, MAX(v_Price)
FROM VideoGame v
WHERE v_YearReleased = "2005"






12. Find the number of games available for the Nintendo 64. List the platform and the count
SELECT COUNT(v_GameName), pl_name
FROM VideoGame v, Platform pl
WHERE v_ProdKey = pl_ProdKey 


13.  Find the customer’s name with the most valuable collection in Thailand 
SELECT MAX(v_price)
FROM Collection, Customer, Nation, VideoGame
WHERE co_colKey == c_colkey AND co_prodkey == v_prodkey AND c_nationkey == n_nationkey AND n_NationName == "Thailand" AND (SELECT SUM(v_price) FROM collection, videogame WHERE co_prodkey == v_prodkey GROUP BY co_colkey)


14. Find the list of available Playstation platforms 
SELECT pl_name
FROM platform
WHERE pl_name LIKE 'PlayStation%%'



15.    Find the games starting with Pokemon and list their developer
SELECT v_GameName, p_name
FROM Publisher, VideoGame
WHERE v_pubkey == p_pubkey AND v_GameName LIKE 'Pokemon%%%%%%%%%'


16.    Find the sum of collection prices available
SELECT SUM(co_price)
FROM Collection, Customer, VideoGame
WHERE co_colKey == c_colkey AND co_prodkey == v_prodkey
GROUP BY co_colkey



17. show region of customerkey 1
SELECT r_name
FROM Customer, Nation, Region
WHERE c_nationkey == n_nationkey AND r_regionkey == n_regionkey AND c_customerkey == '1'

18. Show inventory of storekey 5
SELECT v_GameName
FROM Store, Collection, VideoGame
WHERE s_storekey == '5' AND s_colkey == co_colkey AND v_prodkey == co_prodkey



19. Show the number of available FPS games
SELECT COUNT(v_GameName)
FROM VideoGame v
WHERE v_Genre = "FPS"




20. Find which games were released in 2011 and had a score of 1
SELECT v_GameName
FROM VideoGame v
WHERE v_YearReleased = "2011" AND
v_Score = "1"




21.  Update the amount of Pokemon Sword sold at storekey 5.    
UPDATE store
SET s_Sold == s_Sold + 1
FROM Store, VideoGame
WHERE s_ProdKey == v_ProdKey AND v_GameName == ‘Pokemon Sword’ AND s_storekey = ‘5’