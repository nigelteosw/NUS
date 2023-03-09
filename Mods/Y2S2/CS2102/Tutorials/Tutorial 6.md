### Q1. 
```sql
CREATE OR REPLACE FUNCTION max_min( IN stu_id integer, OUT max_cid integer, OUT min_cid integer ) 
RETURNS RECORD as $$ 
DECLARE 
	max_score integer; 
	min_score integer; 
BEGIN
	SELECT cid
	FROM exams
	WHERE sid = stu_id
	ORDER BY score DESC
	LIMIT 1
	INTO max_cid

	SELECT cid
	FROM exams 
	WHERE sid = stu_id
	ORDER BY score ASC
	LIMIT 1
	INTO min_cid

IF min_cid IS NOT NULL and min_cid >= max_cid THEN
	min_cid := NULL
END IF;

RETURN QUERY SELCT max_cid, min_cid;
END; 
$$ LANGUAGE plpgsql;
```


### Q2.
```sql
CREATE OR REPLACE FUNCTION revised_avg( IN stu_id integer, OUT r_avg float ) 
RETURNS float as $$ 
DECLARE
	max_score INTEGER; 
	min_score INTEGER; 
	total_score INTEGER := 0; 
	num_records INTEGER := 0;
BEGIN
	SELECT MAX(score) INTO max_score
	FROM exams
	WHERE sid = stu_id

	SELECT MIN(score) INTO min_score
	FROM exams
	WHERE sid = stu_id

	FOR record IN (SELECT score FROM exams WHERE sid = stu_id)
	LOOP 
		IF record.score <> max_score AND record.score <> min_score THEN
			total_score := total_score + record.score
			num_records := num_records + 1
		END IF;
	END LOOP;

	IF num_records >= 3 THEN 
		RETURN total_score / num_records;
	ELSE
		RETURN NULL; -- Less than 3 records return null
	END IF;
END;
$$ LANGUAGE plpgsql;
```


### Q3.
```sql
CREATE OR REPLACE FUNCTION list_r_avg() 
RETURNS TABLE ( stu_id integer, ravg float ) AS $$ 
DECLARE 
	curs CURSOR FOR (SELECT sid, score from exams order by sid);
	max_score INTEGER; 
	min_score INTEGER; 
	total_score INTEGER := 0; 
	num_records INTEGER := 0;
BEGIN 

	OPEN curs;
	LOOP
		FETCH curs into r;
		SELECT MAX(r.score) INTO max_score
		FROM r
		WHERE r.sid = stu_id
	
		SELECT MIN(r.score) INTO min_score
		FROM r
		WHERE r.sid = stu_id
	
		FOR record IN (SELECT r.score FROM exams WHERE sid = stu_id)
		LOOP 
			IF record.score <> max_score AND record.score <> min_score THEN
				total_score := total_score + record.score
				num_records := num_records + 1
			END IF;
		END LOOP;
	
		IF num_records >= 3 THEN 
			RETURN total_score / num_records;
		ELSE
			RETURN NULL; -- Less than 3 records return null
		END IF;

		RETURN NEXT;
	END LOOP;
	
END; 
$$ LANGUAGE plpgsql
```


### Q4.
```sql
CREATE OR REPLACE FUNCTION list_scnd_highest()
RETURNS TABLE (sid INTEGER, second_highest_score INTEGER) as $$
DECLARE
	cur CURSOR FOR SELECT DISTINCT sid FROM exams;
	cur_rec exams%ROWTYPE;
	highest_score INTEGER:
	second_highest_score INTEGER;
BEGIN
	FOR cur_rec IN cur LOOP
		sid := cur_rec.sid
		highest_score := NULL;
		second_highest_score := NULL;
		
		FOR rec IN (SELECT score FROM exams WHERE sid = curr_rec.sid ORDER BY score)
		LOOP
			IF highest_score IS NULL THEN
				highest_score := rec.score;
			ELSIF second_highest_score IS NULL AND rec.score < highest_socre THEN
				second_highest_score := rec.score;
			END IF;
		END LOOP;
		
		RETURN NEXT;
	END LOOP;
END;
$$ LANGUAGE plpsql;

```