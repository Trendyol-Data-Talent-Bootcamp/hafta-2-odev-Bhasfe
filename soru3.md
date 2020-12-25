
## Soru 3) "sample.pageview": tablosunda 1 gün içerisinde trendyol.com a gelen tüm ziyaretlerin logu var.

```SQL
with task3
as
(
select
timestamp_trunc(view_ts , minute) as time,
approx_count_distinct(deviceid) as active_users
from `dsmbootcamp.baris_hasdemir.pageview` 
group by time
)
select time,
sum(active_users) over(order by time asc rows between 4 preceding and 0 following) as active_cnt
from task3 
order by time desc;
```
