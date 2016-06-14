## Query Format

> Query

```SQL
SELECT * FROM {metric} 
 WHERE entity = {entity} 
 AND tags.{tagkey} = '/' 
 AND time > {startTime} 
 AND time < {endTime}
```
