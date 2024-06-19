```sql orders_by_day
SELECT 
    DATE_TRUNC('day',order_datetime) AS days,
    COUNT(*) AS num_orders_num0
FROM 
    orders
GROUP BY 
    days
```

<DateRange
    name="range_filtering_a_query"
    data={orders_by_day}
    dates=days
/>

```sql filtered_query
select 
    *
from ${orders_by_day}
where days between '${inputs.range_filtering_a_query.start}' and '${inputs.range_filtering_a_query.end}'
```
<DataTable
    data={filtered_query}
/>

<LineChart
    data={filtered_query}
    x=days
    y=num_orders_num0
/>




