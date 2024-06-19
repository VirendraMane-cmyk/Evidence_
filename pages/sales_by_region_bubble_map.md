```sql sales_by_region
SELECT 
    CAST(z.lat AS DOUBLE) AS lat,
    CAST(z.lng AS DOUBLE) AS lng,
    z.zip, 
    SUM(o.sales) AS total_sales
FROM 
    needful_things.orders o
JOIN 
    needful_things.zipcodes z 
ON 
    o.zipcode = CAST(z.zip AS INTEGER)
GROUP BY 
    lat, 
    lng, 
    z.zip
```

<BubbleMap 
    data={sales_by_region} 
    lat=lat
    long=lng
    size=total_sales 
    maxSize=5
/>
