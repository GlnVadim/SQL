# Deloitte SQL Interview
## RANK DESC & RANK ASC | Population Density
Source: [Deloitte SQL Interview | RANK DESC & RANK ASC | Population Density](https://www.youtube.com/shorts/ftFSXYOllHI)
```SQL
CREATE TABLE Cities
  (Country VARCHAR(100),
  City VARCHAR(100),
  Population INT,
  Area DECIMAL(10, 2) -- Area in square meter
  );

INSERT INTO Cities (Country, City, Population, Area)
VALUES
  ('Germany', 'Berlin', 3769000, 891.68),
  ('France', 'Paris', 2148000, 105.40),
  ('Japan', 'Tokyo', 13929000, 2191.00),
  ('Brazil', 'São Paulo', 12330000, 1521.11),
  ('USA', 'New York', 8419000, 783.80),
  ('Germany', 'Fuerth', 132000, 0);

SELECT
  c.City,
  c.Density
FROM
  (SELECT
  City,
  Population / Area AS Density,
  RANK() OVER (ORDER BY Population / Area DESC) AS RankUp,
  RANK() OVER (ORDER BY Population / Area ASC) AS RankDown
FROM
  Cities
WHERE
  Area <> 0
  ) AS c
WHERE
  RankUp = 1
  OR RankDown = 1
```
# LinkedIn SQL Interview Question - Data Science Skills
Source: [LinkedIn SQL Interview Question | DataLemur](https://datalemur.com/questions/matching-skills)
``` SQL
SELECT
  candidate_id,
  SUM(PythonSkill) AS PythonSkill,
  SUM(TableauSkill) AS TableauSkill,
  SUM(PostgreSQLSkill) AS PostgreSQLSkill
FROM
  (SELECT 
    skill, 
    candidate_id,
    CASE 
      WHEN skill = 'Python' THEN  1 
      ELSE 0 
    END AS PythonSkill,
    CASE 
      WHEN skill = 'Tableau' THEN  1 
      ELSE 0 
    END AS TableauSkill,
    CASE 
      WHEN skill = 'PostgreSQL' THEN  1 
      ELSE 0 
    END AS PostgreSQLSkill
  FROM 
    candidates
  WHERE
    skill IN ('Python', 'Tableau', 'PostgreSQL')) AS subq
GROUP BY
  candidate_id
HAVING
  PythonSkill = 1 
  AND TableauSkill = 1 
  AND PostgreSQLSkill = 1
  
```
