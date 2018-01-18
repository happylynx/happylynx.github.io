# Postgres anonymous code blocks

* It allows to languages other than pure SQL, most often plpgsql.
* Queries in anonymous code blocks cannot return any value thus `SELECT` has to be replace by `PERFORM`. `PERFORM` has same 
  syntax as `SELECT` but discatds result of the query.

Example:

```sql
DO $$
BEGIN
    UPDATE tmpx SET val = '{}' WHERE id = 40;
    PERFORM 'SELECT 1'; -- it just returns text
    PERFORM GetAllFromVmIcons();
    PERFORM * from vms;
    IF (TRUE) THEN BEGIN END; END IF;
    RAISE NOTICE 'a';
END;
$$ LANGUAGE plpgsql;
```
