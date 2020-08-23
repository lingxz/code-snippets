# SQL

### Sliding window distinct count \(e.g. 7DAU, 28DAU\)

```sql
SELECT b.day, count(DISTINCT a.user_id)
from glip_production.presences_1d a,
 (SELECT distinct(day), TIMESTAMPADD(day,-6, day) dt_start
  from glip_production.presences_1d t1) b
where a.day >= b.dt_start and a.day <= b.day
group by b.day
```

