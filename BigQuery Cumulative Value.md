
- Cumulative Value

```
WITH
  seq_dates AS (
  SELECT
    num AS num,
    DATE_ADD(PARSE_DATE('%Y%m%d', '20220101'), INTERVAL num DAY) AS seq_date
  FROM
    UNNEST(GENERATE_ARRAY(0, 10)) AS num )
SELECT
  seq.seq_date,
  SUM(value) AS cumulative
FROM
  seq_dates seq
CROSS JOIN (
  SELECT
    PARSE_DATE('%Y%m%d',  '20220109') AS d,
    1 AS value
  UNION ALL
  SELECT
    PARSE_DATE('%Y%m%d', '20220111') AS d,
    2 AS value
) data
WHERE
  (data.d<=seq.seq_date)
GROUP BY seq.seq_date
```

- Output

```
seq_date	cumul
2022-01-09	1
2022-01-10	1
2022-01-11	3
```
