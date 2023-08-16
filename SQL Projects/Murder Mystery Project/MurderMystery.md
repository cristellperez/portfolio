# Knight Lab's Murder Mystery

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
![sql murdermystery csreport](https://github.com/cristellperez/portfolio/assets/140837511/ef2bb370-8551-4dfa-8885-b0ec521f6a69)

First witness
```SQL
SELECT *
FROM person
WHERE address_street_name = "Northwestern Dr"
ORDER BY address_number DESC
LIMIT 1;
```  

![sql murdermystery witness1](https://github.com/cristellperez/portfolio/assets/140837511/9fd9a086-0fe4-4132-89d8-344602057122)

Second Witness
```SQL
SELECT *
FROM person
WHERE address_street_name = "Franklin Ave"
AND name LIKE "Annabel%";
```  
![sql murdermystery witness2](https://github.com/cristellperez/portfolio/assets/140837511/2859d737-bdb4-414d-b06b-2f8b760dc006)

Interview Transcripts
```SQL
SELECT *
FROM interview
WHERE person_id = 14887
OR person_id = 16371;
```
![sql murdermystery transcripts](https://github.com/cristellperez/portfolio/assets/140837511/f7aa50be-425e-47c2-ba75-e8004ef2fa2d)

Gym member with id and check-in date
```SQL              
SELECT gm.id, gm.name 
FROM get_fit_now_member gm
JOIN get_fit_now_check_in gc
ON gm.id = gc.membership_id
WHERE gm.id LIKE "48Z%" 
AND gc.check_in_date = 20180109;
```
![sql murdermystery gymmembers](https://github.com/cristellperez/portfolio/assets/140837511/be477c48-9080-40a4-83bb-ef8df8a74e10)

```SQL
SELECT p.name, dl.plate_number
FROM person p
JOIN drivers_license dl
ON p.license_id = dl.id
WHERE p.name = "Joe Germuska" OR p.name = "Jeremy Bowers";
```
![sql murdermystery plates](https://github.com/cristellperez/portfolio/assets/140837511/117d22eb-409e-405f-a89b-f1aed1d7fdad)


Check Solution
```SQL
INSERT INTO solution VALUES (1, 'Jeremy Bowers');
        SELECT value FROM solution;
```
![sql murdermystery jb](https://github.com/cristellperez/portfolio/assets/140837511/1422c5ef-7914-4403-98ff-3aa6feaf79de)


Find real villain
```SQL
SELECT p.name, i.transcript
FROM person p
JOIN interview i
ON p.id = i.person_id
WHERE p.name = "Jeremy Bowers";
```
![sql murdermystery realvillain](https://github.com/cristellperez/portfolio/assets/140837511/c8950584-c0b7-49d5-aba7-5842fdbccd89)

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
![sql murdermystery realvillain2](https://github.com/cristellperez/portfolio/assets/140837511/0656133c-6831-49e9-868a-3768dad1da64)


```SQL
INSERT INTO solution VALUES (1, 'Miranda Priestly');
        SELECT value FROM solution;
```
![sql murdermystery complete](https://github.com/cristellperez/portfolio/assets/140837511/4bbdff05-714e-49f1-b3d4-2beab2b02763)
