---
layout: post
title:  useful sql
date:   
---

### **Dates**
```  
> DATE_PART( ‘hour’, event_date ) AS event_hour
> DATE_DIFF( ‘day’, start_date, end_date ) AS date_difference
> DATE_TRUNC( ‘week’, event_date )  AS start_of_event_week
> event_date + (‘14 days’)::INTERVAL AS 14_days_after_event_date
> event_timestamp::DATE AS event_timestamp_to_date
> DAY( )
> YEAR( )
```

### **Functions**
```
> NTILE( 100 ) OVER( ORDER BY spend_amount ) AS percentile
> ROUND( number , 2 ) AS rounded_to_2_decimal_places
> LENGTH( ) AS length
> NVL()
```
### **Sequencing**
```
> LAG( event_date, 1 ) OVER( PARTITION BY user_id ORDER BY event_date ASC ) AS previous_event
> LEAD( event_date, 1 ) OVER( PARTITION BY user_id ORDER BY event_date ASC ) AS next_event
> COUNT( event_date ) OVER( PARTITION BY user_id ORDER BY event_date ASC ) AS event_number
> ROW_NUMBER( ) OVER( PARTITION BY user_id ORDER BY event_date ASC ) AS event_number
```

### **Joins & Unions**
```
> JOIN (aka INNER JOIN)
> LEFT JOIN
> RIGHT JOIN
> OUTER JOIN
> UNION
> UNION ALL
> INTERSECT
```
