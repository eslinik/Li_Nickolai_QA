select name_genre, sum(buy_book.amount) as Количество
from 
   genre inner join book using(genre_id)
         inner join buy_book using(book_id)
group by name_genre
having sum(buy_book.amount) = 
(select max(sum_amount) as max_sum_amount
                      from (select genre_id, sum(buy_book.amount) as sum_amount
                                           from buy_book
                                           inner join book using(book_id)
                                           inner join author using(author_id)
                                           group by genre_id) query_in
                           );

