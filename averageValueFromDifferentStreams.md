Expected output is an average for the cpuUsage and a count of unique RoleInstance values, the output will be generated every 10 minutes

Sample input (time automatically appended by Event Hubs):

```
cpuUsage    |    RoleInstance
5           |    1
10          |    2
4           |    1
```

```sql
WITH roles AS (SELECT
    AVG(cpuUsage) AS Average, 
	COUNT(RoleInstance) AS roleInstances
FROM
    [cpu-values] 
GROUP BY 
	roleinstance, 
	TumblingWindow(minute, 10)
)
SELECT 
	AVG(Average) AS [avg], 
	System.Timestamp AS systimestamp, 
	COUNT(roleInstances) AS roleinstance
INTO
    [testoutput]
FROM
    [roles]
GROUP BY 
	TumblingWindow(minute, 5)
```
