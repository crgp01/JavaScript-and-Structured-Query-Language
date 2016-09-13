                                        Assignment: The Biblioteca database

1. Who checked out the book 'The Hobbit’?

		select  name from member, book, checkout_item where checkout_item.member_id = member.id and 
		checkout_item.book_id=book.id and book.title = "The Hobbit"
		GROUP BY name;

Answer: "Anand Beck"


2. How many people have not checked out anything?

            select count (name) from member where member.id not in (Select checkout_item.member_id from checkout_item)
            
            Answer: 37

3. What books and movies aren't checked out?

	select id, title from book where book.id not in 
	(select checkout_item.book_id from checkout_item where checkout_item.book_id is not null)
	union
	select id, title from movie where movie.id not in 
	(select checkout_item.movie_id from checkout_item where checkout_item.movie_id is not null)

Answer: 

	    "2"	"Fellowship of the Ring"
	    "6"	"1984"
	    "6"	"Thin Red Line"
	    "7"	"Crouching Tiger, Hidden Dragon"
	    "7"	"Tom Sawyer"
	    "8"	"Catcher in the Rye"
	    "8"	"Lawrence of Arabia"
	    "9"	"Office Space"
	    "9"	"To Kill a Mockingbird"
	    "10"	"Domain Driven Design"

4. Add the book 'The Pragmatic Programmer', and add yourself as a member. Check out 'The Pragmatic Programmer'. 
Use your query from question 1 to verify that you have checked it out. Also, provide the SQL used to update the database.

		insert into book (title) values ("The Pragmatic Programmer");
		      
		insert into member (name) values ("Cristina Rivera”);
		      
		insert into checkout_item (member_id, book_id) values 
		((select id from member where member.name="Cristina Rivera"), 
		(select id from book where book.title= "The Pragmatic Programmer"));
		      
		select  name from member, book, checkout_item where checkout_item.member_id = member.id 
		and checkout_item.book_id=book.id and book.title like "The Pragmatic Programmer";
		      
		Answer: Cristina Rivera

5. Who has checked out more that 1 item?  Tip: Research the GROUP BY syntax.

		select name from member 
		where member.id in
		(select member_id 
		from  checkout_item 
		group by checkout_item .member_id
		having count(checkout_item.member_id) > 1)
		    
		Answer: 
		    
		"Anand Beck"
		"Frank Smith"

