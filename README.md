CREATE TABLE demographics (id INTEGER, name TEXT, gender TEXT, eth TEXT, score INTEGER);
ALTER TABLE demographics
ADD id INTEGER;
INSERT INTO demographics VALUES (1, "Matt", "Male", "White", "5");
INSERT INTO demographics VALUES (2, "Jodie", "Female", "White", "10");
INSERT INTO demographics VALUES (3, "Marisa", "Female", "White", "6")
INSERT INTO demographics VALUES (4, "Jack", "Male", "Black", "7");
CREATE TABLE outcomes (id INTEGER, self_control INTEGER, social_interaction INTEGER);
INSERT INTO outcomes VALUES(1, 10, 5);
INSERT INTO outcomes VALUES(2, 6, 4);
INSERT INTO outcomes VALUES(3, 5, 9);
INSERT INTO outcomes VALUES(4, 8, 3);
INSERT INTO outcomes (self_awareness)
VALUES (10);
ALTER TABLE outcomes
ADD self_awareness INTEGER;
/* Here I am selecting all values from demographics */
SELECT * FROM demographics;
/* Here I am selecting only the rows for the name column from the demographics table */
SELECT name FROM demographics;
/* Here I am going to select all rows and then order by name */
SELECT * FROM demographics ORDER BY name;
/*Here I am going to select using a where clause where we can use greater than or less to limit our results */
SELECT * FROM demographics WHERE score > 5 ORDER BY name;
/*Get the sum of a particular row*/
SELECT SUM(score) FROM demographics;
SELECT MAX(score) FROM demographics;
/*Here I am summing by another variable gender.  Summing all males and all females score values*/
SELECT gender, SUM(score) FROM demographics GROUP BY gender;
/*Here I selecting from demo where score is greater than 5 and eth is equal to white and then ordering the values in decending order (small to biggest)*/
SELECT * FROM demographics WHERE score > 5 AND eth = "White" ORDER BY score;
/*Same as above just with or.  And comes first when using both and or*/
SELECT * FROM demographics WHERE score > 5 OR eth = "White" ORDER BY score;

/*Here we are substitution the OR statement with the IN statment that says look for white or black and return them*/
SELECT * FROM demographics WHERE eth IN ("White", "Black");

/*Here we are not saying all expect those that are white and black which excludes everyone*/
SELECT * FROM demographics WHERE eth NOT IN ("White", "Black");
SELECT * FROM demographics WHERE eth IN ("White", "Black");

SELECT * FROM demographics WHERE score IN (SELECT self_control FROM outcomes WHERE self_control > 5);

/*Here I am selecting values from the column score that match any value in the social_interaction variable from the outcomes table*/
SELECT * FROM demographics WHERE score IN (SELECT social_interaction FROM outcomes);

/* Could use the like option if you want to find a response with a paritcular word in the example.  For exmple if you want to all ethnicities that include black in an open ended response, then you could use the like option to do this*/

/*Here we are saying sum the score by eth and then create a column score_eth, which we can later subset using the HAVING function which I say only those with greater than 7 which means only white is left*/
SELECT eth, SUM(score) AS score_eth FROM demographics GROUP BY eth HAVING score_eth > 7; 

SELECT COUNT(*) FROM demographics WHERE score > 5;
