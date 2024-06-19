```sql sales_by_day
WITH daily_aggregates AS (
    SELECT 
        DATE_TRUNC('day', order_datetime) AS day,
        category,
        SUM(sales) AS sales_usd0k,
    FROM 
        orders
    GROUP BY 
        DATE_TRUNC('day', order_datetime), 
        category
)
SELECT 
    day,
    category,
    sales_usd0k
FROM 
    daily_aggregates
ORDER BY 
    day,
    category
```

<DateRange
    name="range_filtering_a_query"
    data={sales_by_day}
    dates=day
/>

```sql filtered_query
select * 
from ${sales_by_day}
where day between '${inputs.range_filtering_a_query.start}' and '${inputs.range_filtering_a_query.end}'
```

<LineChart
    data={filtered_query}
    title="Sales by Day, {inputs.category.label}" 
    series=category
/>

<DataTable 
    data={filtered_query}
    title="Table for sales by Month"
    search=true
/>

