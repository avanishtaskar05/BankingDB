select id,likes,sum(likes) over(partition by id, order by likes desc) as rank from posts;

select id,likes, dense_rank() over (order by likes desc) as rank from posts; 
