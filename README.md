# library
16.5 Studio : Library SQL practice

WARM UP QUERIES
#1
SELECT title, isbn FROM book 
WHERE genre_id = (SELECT genre_id FROM genre WHERE genres = "Mystery");

#2
SELECT title, first_name, last_name 
FROM book
INNER JOIN author ON book.author_id = author.author_id
WHERE deathday IS null;

LOAN OUT A BOOK
#1
UPDATE book 
SET available = 0
WHERE title = "Little Women";

#2
INSERT INTO loan(patron_id,date_out,book_id)
VALUES (1, curdate(),21);

#3
UPDATE patron
SET loan_id = (SELECT MAX(loan_id) FROM loan)
WHERE patron_id = 1;

CHECK A BOOK BACK IN
#1
UPDATE book
SET available = 1
WHERE title = "Little Women";

#2
UPDATE loan
SET date_in = curdate()
WHERE patron_id = 1;

#3
UPDATE patron
SET loan_id = null
WHERE patron_id = 1;

WRAP IT UP
SELECT patron.first_name, patron.last_name, genre.genres FROM loan INNER JOIN patron ON patron.patron_id = loan.patron_id
INNER JOIN book ON loan.book_id = book.book_id
INNER JOIN genre ON book.genre_id = genre.genre_id
WHERE loan.date_in IS NULL;

