# Instagram-clone-using-Mysql

#question1
#write a sql query to find the actors who were cast in the movie 'Annie Hall'. return actor first name, last name and role.

use moviedb;
select * from movie_cast;
select * from actors;
select * from movie;

select a.act_fname, a.act_lname,
mc.role, m.mov_title
from actors as a
join movie_cast as mc
on a.act_id = mc.act_id
join movie as m
on mc.mov_id = m.mov_id
where mov_title = 'Annie Hall';


#question 2
# From the following tables write a sql query to find the director who directed a movie that casted a role for 'Eyes Wide Shut'. return director first name, last name and movie title.alter

select * from director;
select * from movie_direction;
select * from movie;

select d.dir_fname, d.dir_lname, mov_title
from director as d
inner join movie_direction as md
on d.dir_id = md.dir_id
join movie as m
on md.mov_id = m.mov_id
where mov_title='eyes wide shut';


#question 3
# write a sql query to find who directed a movie that casted a role as'Sean Maguire'. return director first name, last name and movie title

select * from director;
select * from movie_cast;
select * from movie;
select * from movie_direction;

select d.dir_fname, d.dir_lname,  m.mov_title
from director as d
join movie_direction as m1
on d.dir_id = m1.dir_id
join movie as m
on m1.mov_id = m.mov_id
join movie_cast as mc
on mc.mov_id = m.mov_id
where role = 'Sean Maguire';

#question 4
#write a sql query to find the actors who have not acted in any movies between 1990 and 2000. Return actor first name, last name, movie title and release year.

select * from actors;
select * from movie_cast;
select * from movie;

select a.act_fname, a.act_lname, m.mov_title, m.mov_year
from actors as a
join movie_cast as mc
on a.act_id = mc.act_id
join movie as m
on mc.mov_id = m.mov_id
where m.mov_year not between 1990 and 2000;

#question 5
#write a sql query to find the directors with the number of genres of movies. group the result set on director firstname,
#lastname and generic title. sort the result in ascending order by director firstname and lastname. return director firstname, last name and number of genres of movies

select * from director;
select * from movie_direction;
select * from movie_genres;
select * from genres;

select d.dir_fname, d.dir_lname, g.gen_title, count(g.gen_title)
from director as d
join movie_direction as md
on d.dir_id = md.dir_id
join movie_genres as mg
on md.mov_id = mg.mov_id
join genres as g
on mg.gen_id = g.gen_id
group by d.dir_fname, d.dir_lname, g.gen_title
order by d.dir_fname, d.dir_lname;
