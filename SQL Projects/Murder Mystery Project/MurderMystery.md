![sql murdermystery csreport](https://github.com/cristellperez/portfolio/assets/140837511/deff9943-c703-4fad-9871-7b60a51c7576)
![Uploading sql.murdermystery.witness2.png…]()
![Uploading sql.murdermystery.witness1.png…]()
![Uploading sql.murdermystery.gymmembers.png…]()
![Uploading sql.murdermystery.transcripts.png…]()
![Uploading sql.murdermystery.jb.png…]()
![Uploading sql.murdermystery.realvillain.png…]()

**📚 Table of Contents**
* Business Task: [Knight Lab's SQL Murder Mystery Project](https://mystery.knightlab.com/)
* [Entity Relationship Diagram](https://github.com/cristellperez/SQL/wiki/_new#entity-relationship-diagram)
* [Question and Solution](https://github.com/cristellperez/SQL/wiki/_new#question-and-solution)

***

## Business Task

A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.

***

## Entity Relationship Diagram
![](https://mystery.knightlab.com/schema.png)

First, I want to get a sense of the database structure and how everything connects.

***
## Question and Solution
Start by retrieving the corresponding crime scene report from the police department’s database.

```SQL
SELECT *
FROM crime_scene_report 
WHERE date = 20180115
AND type = 'murder'
AND city = 'SQL City';
```           

First witness
```SQL
SELECT *
FROM person
WHERE address_street_name = "Northwestern Dr"
ORDER BY address_number DESC
LIMIT 1;
```  


Second Witness
```SQL
SELECT *
FROM person
WHERE address_street_name = "Franklin Ave"
AND name LIKE "Annabel%";
```  

Interview Transcripts
```SQL
SELECT *
FROM interview
WHERE person_id = 14887
OR person_id = 16371;
```

Gym member with id and check-in date
```SQL              
SELECT gm.id, gm.name 
FROM get_fit_now_member gm
JOIN get_fit_now_check_in gc
ON gm.id = gc.membership_id
WHERE gm.id LIKE "48Z%" 
AND gc.check_in_date = 20180109;
```

```SQL
SELECT p.name, dl.plate_number
FROM person p
JOIN drivers_license dl
ON p.license_id = dl.id
WHERE p.name = "Joe Germuska" OR p.name = "Jeremy Bowers";
```

Check Solution
```SQL
INSERT INTO solution VALUES (1, 'Jeremy Bowers');
        SELECT value FROM solution;
```

Find real villain
```SQL
SELECT p.name, i.transcript
FROM person p
JOIN interview i
ON p.id = i.person_id
WHERE p.name = "Jeremy Bowers";
```

```SQL
SELECT p.name, dl.height, dl.hair_color, fb.event_name, fb.date
FROM person p
JOIN drivers_license dl
ON p.license_id = dl.id
JOIN facebook_event_checkin fb
ON p.id = fb.person_id
WHERE fb.event_name LIKE "SQL%"
AND dl.hair_color = "red"
AND dl.car_make = "Tesla";
```


```SQL
INSERT INTO solution VALUES (1, 'Miranda Priestly');
        SELECT value FROM solution;
```
![Uploading sql.murdermystery.realvillain2.png…]()
![Uploading sql.murdermystery.complete.png…]()
