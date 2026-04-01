# Data

- [Data](#data)
  - [Raw gradesheet data files](#raw-gradesheet-data-files)
  - [Data dictionary](#data-dictionary)
    - [Notes:](#notes)
    - [Key data fields](#key-data-fields)
    - [Python dictionary](#python-dictionary)
  - [Ground truth labels](#ground-truth-labels)

## Raw gradesheet data files

The raw gradesheet data files can be found in the following Google Drive folders: [Google Drive folder](https://drive.google.com/drive/folders/1KpqachwEKbI2hJ0-V-40Y_VuetCTV1ha).

| File Name                       | Description                               | Remarks                                                                                                 |
| ------------------------------- | ----------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `NEST(OTHER)_2nd.xlsx`          |                                           | Not used as `CLASS` values are `FLEX` / `OTHER`                                                         |
| `NEST(150-159).xlsx`            | Data from BWC batches 150 to 159.         | Not used as target column (`AWC_stream`) values are not available.                                      |
| `NEST(160-169).xlsx`            | Data from BWC batches 160 to 169.         |                                                                                                         |
| `NEST(170-179).xlsx`            | Data from BWC batches 170 to 179.         |                                                                                                         |
| `NEST(180-189).xlsx`            | Data from BWC batches 180 to 190.         |                                                                                                         |
| `NEST(190-197)_fixedup.xlsx`    | Partial data from BWC batches 190 to 197. |                                                                                                         |
| `NEST(1-11-23 to 23-1-24).xlsx` | BWC data from 01 Nov 2023 to 23 Jan 2024. |                                                                                                         |
| `NEST(23-1-24 to 2-4-24).xlsx`  | BWC data from 23 Jan 2024 to 02 Apr 2024. |                                                                                                         |
| `NEST(3-4-24 to 18-8-24).xlsx`  | BWC data from 03 Apr 2024 to 18 Aug 2024. | Came from Lockheed Martin with 28 missing columns. Still used as key columns are still inside the data. |
| `NEST(19-8-24 to 4-3-25).xlsx`  | BWC data from 19 Aug 2024 to 04 Mar 2025. |                                                                                                         |
| `NEST(4-3-25 to 31-3-25).xlsx`  | BWC data from 04 Mar 2025 to 31 Mar 2025. |                                                                                                         |
| `NEST(1-4-25 to 1-5-25).xlsx`   | BWC data from 01 Apr 2025 to 01 May 2025. | BWC 201 and onwards, less some of 200CHONGT's scores.                                                    |
| `NEST(1-5-25 to 29-5-25).xlsx`  | BWC data from 01 May 2025 to 29 May 2025. | BWC 201 and onwards.                                                                                    |
| `NEST(3-6-25 to 30-6-25).xlsx`  | BWC data from 03 Jun 2025 to 30 Jun 2025. | BWC 201 and onwards.                                                                                    |
| `JULY 25.xlsx`                  | BWC data from July 2025.                  |                                                                                                         |
| `LM_BWC201to205_data_pulled_as_of_end_Jan2026.xlsx` | Data from BWC batches 201 to 205 as of end Jan 2026. |                                                                          |
| `LM_BWC206to207_data_pulled_as_of_end_Jan2026.xlsx` | Data from BWC batches 206 to 207 as of end Jan 2026. |                                                                          |

## Data dictionary

The raw Lockheed Martin TIMS data contains the following fields:

| S/N | Field                             | Description                                                                                       | Pandas dtype |
| --- | --------------------------------- | ------------------------------------------------------------------------------------------------- | ------------ | 
| 1   | `STUDENT_ID`                      | The identification of an employee. Used instead of full name in certain parts of the application.<br>The groupby column.| `string` |
| 2   | `STUDENT_FIRST_NAME`              | The employee's first name.                                                                        | `string` |
| 3   | `STUDENT_LAST_NAME`               | The employee's last name.                                                                         | `string` |
| 4   | `STUDENT_DISPLAY_NAME`            | A combination of the person's last and first name (appears in certain places of the application). | `string` |
| 5   | `STUDENT_TITLE`                   | A description of the employee's title (e.g. Manager, QFI, Technician).                            | `string` |
| 6   | `STUDENT_RANK`                    | The description of the employee's job rank (e.g. Captain, Major, Lieutenant).                     | `string` |
| 7   | `STUDENT_RANK_ABBREV`             | An abbreviation of the job rank (used to save space).                                             | `string` |
| 8   | `COURSE`                          | The name of the template used to create the course.                                               | `string` |
| 9   | `CLASS_TEMP_DS_ID`                | The unique identifier for the template used.                                                      | `string` |
| 10  | `CLASS`                           | The name of the class on the course. Suffixes:<br>-`W`: WSO trainee undergoing BWC WSO course.<br>-`F`: Trainee has completed basic BWC course and is going for FWC next, so he needs to complete BWC-F lessons first.<br>-`B`/`A`: Basic BWC course. |  `string` |
| 11  | `CLASS_DS_ID`                     | The unique identifier for the class.                       | `string` |
| 12  | `COURSE_START_DATE`               | The scheduled date the course should start.                | `datetime64[us]` |
| 13  | `COURSE_END_DATE`                 | The scheduled date the course should end.                  | `datetime64[us]` |
| 14  | `COURSE_ACTUAL_START_DATE`        | The actual date the course starts.                         | `datetime64[us]` |
| 15  | `COURSE_ACTUAL_END_DATE`          | The actual date the course ends.                           | `datetime64[us]` |
| 16  | `MODULE_NAME`                     | The name of the module within the class.                   |  `string` |
| 17  | `MODULE_DS_ID`                    | The unique identifier for the module.                      |  `string` |
| 18  | `MODULE_TEMP_NAME`                | The name of the lesson template used to create the module. |  `string` |
| 19  | `MODULE_TEMP_DS_ID`               | The unique identifier for the module template.             |  `string` |
| 20  | `LESSON_START_DATE`               | The scheduled date the lesson should start.                | `datetime64[us]` |
| 21  | `LESSON_END_DATE`                 | The scheduled date the lesson should end.                  | `datetime64[us]` |
| 22  | `LESSON_ACTUAL_START_DATE`        | The actual date the lesson should start.                   | `datetime64[us]` |
| 23  | `LESSON_ACTUAL_END_DATE`          | The actual date the lesson should end.                     | `datetime64[us]` |
| 24  | `LESSON_NUMBER`                   | The name of the lesson. Training feature. Suffixes:<br>-`R`: repeat. Repeated attempts do not count in score tabulation. <br>-`FLEX`/`FL`: loosely used by the instructors to mean flexible or that lesson may or may not be graded eventually. Usually the `EMP_EVAL_COMMENTS` column will further mention `NG` (not graded) or in some other wording. When a trainee hasn't flown in a long time, then they have to FLEX, i.e., re-do the last module where they left off. There are two kinds of FLEX - mandatory FLEX and optional FLEX. For example, if a trainee finishes GH3 but haven't flown in a while, but needs to proceed to GH4, the instructor will let him clock a FLEX before going to GH4 so that he doesn't clock a fail.<br>-`GS`/`G/S`: Ghosted solo/sortie, basically a solo flight but with the instructor at the backseat (possibly due weather), without the instructor saying anything during the sortie. Usually will have `NG` in `EMP_EVAL_COMMENTS`. |
| 25  | `LESSON_DS_ID`                    | The unique identifier of the lesson.                                        | `string` |
| 26  | `LESSON_DESCRIPTION`              | The description of the lesson.                                              | `string` |
| 27  | `PLAN_DISPLAY_ID`                 | An ID used for tracking records application side.                           | `string` |
| 28  | `LESSON_TEMPLATE_COMMENTS`        | Any comments on the lesson                                                  | `string` |
| 29  | `LESSON_TEMP_NAME`                | The name given to the lesson template.                                      | `string` |
| 30  | `LESSON_TEMP_DS_ID`               | A unique identifier for the lesson template.                                | `string` |
| 31  | `PLAN_TEMPLATE_DURATION`          | A number representing the duration of the plan.                             | `Float64` |
| 32  | `PLAN_TEMPLATE_DURATION_TYPE`     | The units for the plan template duration.                                   | `string` |
| 33  | `PLAN_TEMPLATE_DS_ID`             | A unique identifier for the plan template record.                           | `string` |
| 34  | `PLAN_TYPE_ID`                    | Holds the ID of a plan type (e.g. Plan, Lesson, Non-Training event).        | `string` |
| 35  | `SUB_PLAN_TYPE_ID`                | Breaks down plan type even further (e.g. Flight, Vacation, Briefing).       | `string` |
| 36  | `PLAN_CATEGORY_ID`                | The ID of the plan category (e.g. SOLO-1 meaning First Solo).               | `string` |
| 37  | `ABORT_REASON`                    | A descriptive reason for the abort code (e.g. weather conditions).          | `string` |
| 38  | `ABORT_CODE`                      | A code given to show type of mission abort (e.g. Abort, Reschedule, Delay). | `string` |
| 39  | `TAKE_OFF_TIME`                   | The actual takeoff time of a lesson or when the aircraft was accepted.      | `datetime64[us]` |
| 40  | `LANDING_TIME`                    | The actual time the aircraft was landed.                                    | `datetime64[us]` |
| 41  | `ACTUAL_FLIGHT_HOURS`             | The duration of the flight event.                                           | `Float64` |
| 42  | `DUTY_STATUS_DESCRIPTION`         | The status of the mission.<br>`DCO`: Duty Carried Out<br>`DNCO`: Duty Not Carried Out. Do not count scores where DNCO.<br>`DPCO`: Duty Partially Carried Out. Major objectives of the mission met and can move onto next flight, where trainee will try to finish up the unmet minor objectives. | `string` |
| 43  | `WEATHER_CODE_DESCRIPTION`        | A description of the weather conditions.                        | `string` |
| 44  | `SOLO_SHEET_MAN_NOT`              | Not used.                                                       | `string` |
| 45  | `INSTRUCTOR_ID`                   | The employee ID of the assigned instructor.                     | `string` |
| 46  | `INSTRUCTOR_FIRST_NAME`           | The instructor’s first name.                                    | `string` |
| 47  | `INSTRUCTOR_LAST_NAME`            | The instructor’s last name.                                     | `string` |
| 48  | `INSTRUCTOR_DISPLAY_NAME`         | Combination of instructor’s last and first name.                | `string` |
| 49  | `INSTRUCTOR_TITLE`                | The description of the instructor’s job.                        | `string` |
| 50  | `INSTRUCTOR_RANK`                 | The job rank of the instructor.                                 | `string` |
| 51  | `INSTRUCTOR_RANK_ABBREV`          | Abbreviation of the instructor’s rank.                          | `string` |
| 52  | `AVERAGE_SCORE`                   | The average score for the student.                              | `Float64` |
| 53  | `ADJUSTED_SCORE`                  | The overridden score for the student evaluation. Might be empty. If present, can try using it instead of `EMP_EVAL_SCORE`. <br> `1`: fail<br>`2`: marginal<br>`3`: low average              | `Float64` |
| 54  | `EMP_EVAL_COMMENTS`               | Additional notes given by the instructor. If starts with`"NG"`, means not graded. Score is not used for evaluation. | `string` |
| 55  | `EMP_EVAL_SCORE`                  | Score for the evaluation of the lesson. Training feature. Out of 7. Usually 1/7 is a fail. But for some modules, 4/7 is the passing mark.                                     | `Float64` |
| 56  | `EMP_EVAL_RANKING`                | Not used.                                                       | `Float64` |
| 57  | `EVALUATOR_ACKNOWLEDGED`          | True/False if the instructor acknowledged the evaluation.       | `boolean` |
| 58  | `EVALUATOR_ACKNOWLEDGED_DATE`     | The date of the acknowledgement.                                | `datetime64[us]` |
| 59  | `EVAL_ACK_BY_EMPLOYEE_DS_ID`      | Record of instructor who acknowledged evaluation.               | `string` |
| 60  | `EMPLOYEE_ACKNOWLEDGED`           | True/False if the employee acknowledged their score.            | `boolean` |
| 61  | `EMPLOYEE_ACKNOWLEDGED_DATE`      | The date of the employee acknowledgement.                       | `datetime64[us]` |
| 62  | `EMP_ACK_BY_EMPLOYEE_DS_ID`       | Record of the employee/student who acknowledged the evaluation. | `string` |
| 63  | `OBJECTIVE_ID`                    | The name given to an objective.                                 | `string` |
| 64  | `OBJECTIVE_DESCRIPTION`           | The description of the objective.                               | `string` |
| 65  | `OBJECTIVE_RAW_SCORE`             | The raw score given by the instructor.                          | `Float64` |
| 66  | `OBJECTIVE_WEIGHTED_SCORE`        | The final score after being weighted.                           | `Float64` |
| 67  | `OBJECTIVE_SCORE_WEIGHT`          | Weight assigned to the objective.                               | `Float64` |
| 68  | `OBJECTIVE_CRITICAL`              | True/False if the objective is critical.                        | `boolean` |
| 69  | `OBJECTIVE_ACCEPTABLE_SCORE`      | Acceptable score for the objective (-1 or 0).                   | `Float64` |
| 70  | `OBJECTIVE_EXPECTED_SCORE`        | Expected score for the objective.                               | `Float64` |
| 71  | `OBJECTIVE_ACCEPTABLE_SCORE_DSC`  | Acceptable score description (e.g. 4C, 2B, 3b).                 | `string` |
| 72  | `OBJECTIVE_EXPECTED_SCORE_DSC`    | Expected score description (e.g. 4C, 2B, 3b).                   | `string` |
| 73  | `OBJECTIVE_COMMENTS`              | Any comments on the objective during the lesson.                | `string` |

### Notes:

- A lesson is made out of many objectives.
- It is possible that the passing mark for a given objective is more than half of the total score.
- Some objectives are more crucial than others. For example:
  - Let's say that a lesson has 10 objectives. The last 4 objectives are more important than the first 6 objectives.
  - If a trainee gets 8/10 for the first 6 objectives but 2/10 for the last 4 objectives, he still fails.
- Overriding scores is done on LM's TIMS.
- TLDR: Only use first valid sortie attempt for evaluating a trainee.
  - (Following consultation with QFI Siege) Rows where `LESSON_NUMBER` is suffixed with `R` (indicating repeat) or `GS` (ghosted sortie) should be dropped as instructors do not use these for evaluation.
  - (Following consultation with QFI Siege) Rows where `EMP_EVAL_COMMENTS` start with `'NG'` should be dropped as this indicates that the particular sortie was considered to be not graded, and hence the scores will not be used by instructors to evaluate the trainee.
  - (Following consultation with QFI Siege) Rows with `DNCO` in `DUTY_STATUS_DESCRIPTION` should be dropped as this indicated duty not carried out for the sortie, and instructors will not use the scores for this sortie to evaluate the trainee.
- (Following consultation with data analyst Tommy) Replace `EMP_EVAL_SCORE` with `ADJUSTED_SCORE` where available. `ADJUSTED_SCORE` definitions - 1: fail, 2: low marginal, 3: average
- GH 9 was originally PROG CHK, GH 35 was originally GHT, GH 40 was originally BHT
- Module 1 Components - GH 1 to GH 22 (No GH 16 or GH 18 or GH 20)
- Module 2 Components - GH 24 to GH 35 and GHT (No GH 26)
- Module 3 Components - IF 1 to IF 6 and IFT
- Module 6 Components - AN 1 to AN 7

### Key data fields

| S/N | Field                             | Description                                                                                       | Pandas dtype |
| --- | --------------------------------- | ------------------------------------------------------------------------------------------------- | ------------ | 
| 1   | `STUDENT_ID`                      | The identification of an employee. Used instead of full name in certain parts of the application.<br>The groupby column.| `string` |
| 10  | `CLASS`                           | The name of the class on the course. Suffixes:<br>-`W`: WSO trainee undergoing BWC WSO course.<br>-`F`: Trainee has completed basic BWC course and is going for FWC next, so he needs to complete BWC-F lessons first.<br>-`B`/`A`: Basic BWC course. |  `string` |
| 24  | `LESSON_NUMBER`                   | The name of the lesson. Training feature. Suffixes:<br>-`R`: repeat. Repeated attempts do not count in score tabulation. <br>-`FLEX`/`FL`: loosely used by the instructors to mean flexible or that lesson may or may not be graded eventually. Usually the `EMP_EVAL_COMMENTS` column will further mention `NG` (not graded) or in some other wording. When a trainee hasn't flown in a long time, then they have to FLEX, i.e., re-do the last module where they left off. There are two kinds of FLEX - mandatory FLEX and optional FLEX. For example, if a trainee finishes GH3 but haven't flown in a while, but needs to proceed to GH4, the instructor will let him clock a FLEX before going to GH4 so that he doesn't clock a fail.<br>-`GS`/`G/S`: Ghosted solo/sortie, basically a solo flight but with the instructor at the backseat (possibly due weather), without the instructor saying anything during the sortie. Usually will have `NG` in `EMP_EVAL_COMMENTS`. | `string` |
| 42  | `DUTY_STATUS_DESCRIPTION`         | The status of the mission.<br>`DCO`: Duty Carried Out<br>`DNCO`: Duty Not Carried Out. Do not count scores where DNCO.<br>`DPCO`: Duty Partially Carried Out. Major objectives of the mission met and can move onto next flight, where trainee will try to finish up the unmet minor objectives. | `string` |
| 53  | `ADJUSTED_SCORE`                  | The overridden score for the student evaluation. Might be empty. If present, can try using it instead of `EMP_EVAL_SCORE`. <br> `1`: fail<br>`2`: marginal<br>`3`: low average              | `Float64` |
| 54  | `EMP_EVAL_COMMENTS`               | Additional notes given by the instructor. If starts with`"NG"`, means not graded. Score is not used for evaluation. | `string` |
| 55  | `EMP_EVAL_SCORE`                  | Score for the evaluation of the lesson. Training feature. Out of 7. Usually 1/7 is a fail. But for some modules, 4/7 is the passing mark.                                     | `Float64` |

### Python dictionary

```python
DTYPE_MAP = {
    "STUDENT_ID": "string",
    "STUDENT_FIRST_NAME": "string",
    "STUDENT_LAST_NAME": "string",
    "STUDENT_DISPLAY_NAME": "string",
    "STUDENT_TITLE": "string",
    "STUDENT_RANK": "string",
    "STUDENT_RANK_ABBREV": "string",
    "COURSE": "string",
    "CLASS_TEMP_DS_ID": "string",
    "CLASS": "string",
    "CLASS_DS_ID": "string",
    "COURSE_START_DATE": "datetime64[us]",
    "COURSE_END_DATE": "datetime64[us]",
    "COURSE_ACTUAL_START_DATE": "datetime64[us]",
    "COURSE_ACTUAL_END_DATE": "datetime64[us]",
    "MODULE_NAME": "string",
    "MODULE_DS_ID": "string",
    "MODULE_TEMP_NAME": "string",
    "MODULE_TEMP_DS_ID": "string",
    "LESSON_START_DATE": "datetime64[us]",
    "LESSON_END_DATE": "datetime64[us]",
    "LESSON_ACTUAL_START_DATE": "datetime64[us]",
    "LESSON_ACTUAL_END_DATE": "datetime64[us]",
    "LESSON_NUMBER": "string",
    "LESSON_DS_ID": "string",
    "LESSON_DESCRIPTION": "string",
    "PLAN_DISPLAY_ID": "string",
    "LESSON_TEMPLATE_COMMENTS": "string",
    "LESSON_TEMP_NAME": "string",
    "LESSON_TEMP_DS_ID": "string",
    "PLAN_TEMPLATE_DURATION": "Float64",
    "PLAN_TEMPLATE_DURATION_TYPE": "string",
    "PLAN_TEMPLATE_DS_ID": "string",
    "PLAN_TYPE_ID": "string",
    "SUB_PLAN_TYPE_ID": "string",
    "PLAN_CATEGORY_ID": "string",
    "ABORT_REASON": "string",
    "ABORT_CODE": "string",
    "TAKE_OFF_TIME": "datetime64[us]",
    "LANDING_TIME": "datetime64[us]",
    "ACTUAL_FLIGHT_HOURS": "Float64",
    "DUTY_STATUS_DESCRIPTION": "string",
    "WEATHER_CODE_DESCRIPTION": "string",
    "SOLO_SHEET_MAN_NOT": "string",
    "INSTRUCTOR_ID": "string",
    "INSTRUCTOR_FIRST_NAME": "string",
    "INSTRUCTOR_LAST_NAME": "string",
    "INSTRUCTOR_DISPLAY_NAME": "string",
    "INSTRUCTOR_TITLE": "string",
    "INSTRUCTOR_RANK": "string",
    "INSTRUCTOR_RANK_ABBREV": "string",
    "AVERAGE_SCORE": "Float64",
    "ADJUSTED_SCORE": "Float64",
    "EMP_EVAL_COMMENTS": "string",
    "EMP_EVAL_SCORE": "Float64",
    "EMP_EVAL_RANKING": "Float64",
    "EVALUATOR_ACKNOWLEDGED": "boolean",
    "EVALUATOR_ACKNOWLEDGED_DATE": "datetime64[us]",
    "EVAL_ACK_BY_EMPLOYEE_DS_ID": "string",
    "EMPLOYEE_ACKNOWLEDGED": "boolean",
    "EMPLOYEE_ACKNOWLEDGED_DATE": "datetime64[us]",
    "EMP_ACK_BY_EMPLOYEE_DS_ID": "string",
    "OBJECTIVE_ID": "string",
    "OBJECTIVE_DESCRIPTION": "string",
    "OBJECTIVE_RAW_SCORE": "float64",
    "OBJECTIVE_WEIGHTED_SCORE": "float64",
    "OBJECTIVE_SCORE_WEIGHT": "float64",
    "OBJECTIVE_CRITICAL": "boolean",
    "OBJECTIVE_ACCEPTABLE_SCORE": "string",
    "OBJECTIVE_EXPECTED_SCORE": "float64",
    "OBJECTIVE_ACCEPTABLE_SCORE_DSC": "string",
    "OBJECTIVE_EXPECTED_SCORE_DSC": "string",
    "OBJECTIVE_COMMENTS": "string",
}

REQUIRED_COLUMNS = {
    "STUDENT_ID",
    "CLASS",
    "LESSON_NUMBER",
    "DUTY_STATUS_DESCRIPTION",
    "EMP_EVAL_SCORE",
    "ADJUSTED_SCORE",
    "EMP_EVAL_COMMENTS",
}
```

## Ground truth labels

Ground truth labels for BWC batches 160 to 200 are taken from Joel's [BWC_AWCstream_NON_EMPTY.csv](https://drive.google.com/file/d/1aEAdyc9XmPjcaxyyw6wH6I5jvok9NjA9/view?usp=sharing) dated 12 July 2025.

| Field        | Values / Description                                                                                                       |
| ------------ | -------------------------------------------------------------------------------------------------------------------------  |
| `AWC_stream` | 1 = FTR<br>2 = Rotary<br>3 = Transport<br>4 = NFTC FTR<br>5 = ITAF FTR<br>6 = IERW Heli<br>7 = SUPT FTR (Early Stream Out) |
| `av_creoc`   | Indicates whether trainee passed or failed AWC.<BR>1 = Fail<br>2 = Pass                                                                                                       |

Ground truth labels for BWC batches 201 to 207 are taken from `BWC201t207_Status_as_of_end_Feb2026.xlsx` as sent over by Tommy on Defence mail on 13 March 2026.

| Field             | Values / Description               |
| ----------------- | ---------------------------------- |
| `STUDENT_ID_ORIG` | original `STUDENT_ID` from gradesheet data. |
| `Batch`           | BWC batch number.                  |
| `BWC_Status`      | - Pass: `["Pass", "DNF(SUPT)"]` <br>- Fail: ` ["Fail"]`<br>- Others: `["Ongoing", "DNF(Disciplinary)", "Suspended(PsyReview)", "Airsick", "DNF(medrollBWCXXX i.e. rollover to future BWC course xxx due to medical reasons)", "DNF(UGPS i.e. trainee has disrupted pilot training to pursue undergraduate studies)"]`  |
| `Stream_Group`    | Fighter, Transport, or Heli        |
| `Stream_Unit`     | - Fighter: `["FWC", "SUPT", "ITAF", "NFTC"]`<br>- Transport: `["TWC"]`<br>- Heli: `["RWC", "IERW"]`                |
