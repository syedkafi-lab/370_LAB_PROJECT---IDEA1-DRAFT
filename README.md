#Smart Career & Job Fair Management System — Lab Report

-->Project Summary
A combined database-driven platform to manage student resumes, job/internship postings, and job fair participation. Implements skill-based matching, recruiter reviews, and analytics.

-->Deliverables in this package
- `Smart_Career_JobFair_Schema_Complete.sql` — full schema + indexes + views + stored procedures + triggers + sample data
- Flask API scaffold: `app.py`, `requirements.txt`, `Dockerfile`
- ERD, Use Case, and DFD diagrams (export images separately)
- README (this file) with demo steps and queries for the viva

-->How to run (Docker Compose recommended)
1. Install Docker & Docker Compose.
2. Place `Smart_Career_JobFair_Schema_Complete.sql` into a folder `./db/init/01_schema.sql` so MySQL initializes it.
3. Use the provided `docker-compose.yml` (example earlier provided) to run MySQL + Adminer + API.
4. Alternatively, run MySQL locally and import the SQL file:
   ```bash
   mysql -u root -p < Smart_Career_JobFair_Schema_Complete.sql
   ```

-->Important SQL demo queries
- Top matches for job id 1:
  ```sql
  CALL sp_get_top_matches(1, 5);
  ```
- Search resumes by keyword:
  ```sql
  CALL sp_search_resumes('ML', 10);
  ```
- Job fair attendees count:
  ```sql
  SELECT jf.name, COUNT(jfp.participation_id) AS attendees
  FROM JobFairEvent jf
  LEFT JOIN JobFairParticipation jfp ON jf.event_id = jfp.event_id
  GROUP BY jf.event_id;
  ```
-->Screenshots to include in report
1. Adminer showing `Student` table.
2. Result of `CALL sp_get_top_matches(1,5);` in Adminer/console.
3. API curl result for `/api/jobpositions`.

-->Notes for evaluation
- DB logic (matching, shortlisting) uses stored procedures & triggers.
- Schema normalized to 3NF.
- Seed data provided for quick demos.
