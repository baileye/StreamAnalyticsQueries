```sql
SELECT I1.GUID, I1.svcname, I1.vmname, I1.status, 
I1.timestamp,I1.status AS status2, 
DATEDIFF(minute, I1.timestamp, I2.timestamp) AS DurationInMinute
INTO hackathonoutput
FROM testinputhackathon I1 TIMESTAMP BY timestamp
LEFT OUTER JOIN testinputhackathon I2 TIMESTAMP BY timestamp
ON I1.GUID = I2.GUID
AND I1.vmname = I2.vmname
AND DATEDIFF(ms, I1, I2) BETWEEN 1 AND 120000
WHERE I1.status = 'OK'
AND I2.status IS NULL
```
