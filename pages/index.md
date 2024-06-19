
```sql categories
  select
      category
  from needful_things.orders
  group by category
```

<Dropdown data={categories} name=category value=category>
    <DropdownOption value="%" valueLabel="All Categories"/>
</Dropdown>

<Dropdown name=year>
    <DropdownOption value=% valueLabel="All Years"/>
    <DropdownOption value=2019/>
    <DropdownOption value=2020/>
    <DropdownOption value=2021/>
</Dropdown>

```sql orders_by_category
  select 
      date_trunc('month', order_datetime) as month,
      sum(sales) as sales_usd,
      category
  from needful_things.orders
  where category like '${inputs.category.value}'
  group by all
  order by sales_usd desc
```

<DateRange
    name="range_filtering_a_query"
    data={orders_by_category}
    dates=month
/>

```sql filtered_orders_by_category
select * 
from ${orders_by_category}
where month between '${inputs.range_filtering_a_query.start}' and '${inputs.range_filtering_a_query.end}'
```

<BarChart
    data={filtered_orders_by_category}
    title="Sales by Month, {inputs.category.label}"
    x=month
    y=sales_usd
    series=category
/>

