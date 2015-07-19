# CFPB
CFPB_written_assessment
Please follow the below steps to reproduce my reporting results:
A)	Complaints and Survey file downloads:
1.	Download CFPB’s public complaint database (http://www.consumerfinance.gov/complaintdatabase/).
2.	Download income data from the 5-year ACS survey file from census.gov (http://www2.census.gov/acs2013_5yr/summaryfile/2009-2013_ACSSF_By_State_By_Sequence_Table_Subset/UnitedStates/All_Geographies_Not_Tracts_Block_Groups/20135us0015000.zip).
3.	The header information for the sequence file can be found in the Seq15.xls file in the zip file located here: http://www2.census.gov/programs-surveys/acs/summary_file/2013/data/2013_5yr_Summary_FileTemplates.zip.
4.	Download geography information for the 5-year ACS survey file from census.gov (http://www2.census.gov/acs2013_5yr/summaryfile/2009-2013_ACSSF_By_State_By_Sequence_Table_Subset/UnitedStates/All_Geographies_Not_Tracts_Block_Groups/g20135us.csv).
5.	The header information for the geography file can be found on page 10 of the technical document here: http://www2.census.gov/acs2013_5yr/summaryfile/ACS_2013_SF_Tech_Doc.pdf.

B)	PostgreSql Installation:
Download PostgreSql Version 9.4.4 from http://www.enterprisedb.com/products-services-training/pgdownload#windows
C)	After installation, open pgAdmin III and create following 3 tables and associated indexes  in postgres (database)->Schema(public)
-- Table: consumer_complaints
-- DROP TABLE consumer_complaints;
            CREATE TABLE consumer_complaints (  date_received date,  product character varying(50),  sub_product character varying(200),  issue character varying(200),  sub_issue character varying(1000),  consumer_compl_narr character varying(4000),  company_public_res character varying(4000),  company character varying(100),  state character(2),  zip_code character varying(15),  submitted_via character varying(30),  date_sent date,  company_res_to_cons character varying(4000),  timely_response character varying(4),  consumer_disputed character varying(4),  complaint_id integer)WITH (  OIDS=FALSE);
ALTER TABLE consumer_complaints  OWNER TO postgres;
-- Index: idx_consumer_complaints_1
-- DROP INDEX idx_consumer_complaints_1;
CREATE INDEX idx_consumer_complaints_1  ON consumer_complaints  USING btree  (zip_code COLLATE pg_catalog."default");
-- Table: geography_survey
-- DROP TABLE geography_survey;
CREATE TABLE geography_survey (  fileid character varying(6),
  stusab character varying(2),
  sumlevel character varying(3),
  component character varying(2),
  logrecno character varying(7),
  us character varying(1),
  region character varying(1),
  division character varying(1),
  statece character varying(2),
  state character varying(2),
  county character varying(3),
  cousub character varying(5),
  place character varying(5),
  tract character varying(6),
  blkgrp character varying(1),
  concit character varying(5),
  aianhh character varying(4),
  aianhhfp character varying(5),
  aihhtli character varying(1),
  aitsce character varying(3),
  aits character varying(5),
  anrc character varying(5),
  cbsa character varying(5),
  csa character varying(3),
  metdiv character varying(5),
  macc character varying(1),
  memi character varying(1),
  necta character varying(5),
  cnecta character varying(3),
  nectadiv character varying(5),
  ua character varying(5),
  blank_1 character varying(5),
  cdcurr character varying(2),
  sldu character varying(3),
  sldl character varying(3),
  blank_2 character varying(6),
  blank_3 character varying(3),
  zcta5 character varying(5),
  submcd character varying(5),
  sdelm character varying(5),
  sdsec character varying(5),
  sduni character varying(5),
  ur character varying(1),
  pci character varying(1),
  blank_4 character varying(6),
  blank_5 character varying(5),
  puma5 character varying(5),
  blank_6 character varying(5),
  geoid character varying(40),
  name character varying(1000),
  bttr character varying(6),
  btbg character varying(1),
  blank_7 character varying(44)) WITH (  OIDS=FALSE);
ALTER TABLE geography_survey  OWNER TO postgres;
-- Index: idx_geography_survey_1
-- DROP INDEX idx_geography_survey_1;
CREATE INDEX idx_geography_survey_1  ON geography_survey  USING btree  (zcta5 COLLATE pg_catalog."default");
-- Index: idx_geography_survey_2
-- DROP INDEX idx_geography_survey_2;
CREATE INDEX idx_geography_survey_2
  ON geography_survey
  USING btree
  (logrecno COLLATE pg_catalog."default");
-- Table: acs_survey_income
-- DROP TABLE acs_survey_income;
CREATE TABLE acs_survey_income(  fileid character varying(15),
  filetype character varying(15),
  stusab character varying(15),
  chariter character varying(15),
  sequence character varying(15),
  logrecno character varying(15),
  b06010_001 character varying(100),
  b06010_002 character varying(100),
  b06010_003 character varying(100),
  b06010_004 character varying(100),
  b06010_005 character varying(100),
  b06010_006 character varying(100),
  b06010_007 character varying(100),
  b06010_008 character varying(100),
  b06010_009 character varying(100),
  b06010_010 character varying(100),
  b06010_011 character varying(100),
  b06010_012 character varying(100),
  b06010_013 character varying(100),
  b06010_014 character varying(100),
  b06010_015 character varying(100),
  b06010_016 character varying(100),
  b06010_017 character varying(100),
  b06010_018 character varying(100),
  b06010_019 character varying(100),
  b06010_020 character varying(100),
  b06010_021 character varying(100),
  b06010_022 character varying(100),
  b06010_023 character varying(100),
  b06010_024 character varying(100),
  b06010_025 character varying(100),
  b06010_026 character varying(100),
  b06010_027 character varying(100),
  b06010_028 character varying(100),
  b06010_029 character varying(100),
  b06010_030 character varying(100),
  b06010_031 character varying(100),
  b06010_032 character varying(100),
  b06010_033 character varying(100),
  b06010_034 character varying(100),
  b06010_035 character varying(100),
  b06010_036 character varying(100),
  b06010_037 character varying(100),
  b06010_038 character varying(100),
  b06010_039 character varying(100),
  b06010_040 character varying(100),
  b06010_041 character varying(100),
  b06010_042 character varying(100),
  b06010_043 character varying(100),
  b06010_044 character varying(100),
  b06010_045 character varying(100),
  b06010_046 character varying(100),
  b06010_047 character varying(100),
  b06010_048 character varying(100),
  b06010_049 character varying(100),
  b06010_050 character varying(100),
  b06010_051 character varying(100),
  b06010_052 character varying(100),
  b06010_053 character varying(100),
  b06010_054 character varying(100),
  b06010_055 character varying(100),
  b06010pr_001 character varying(100),
  b06010pr_002 character varying(100),
  b06010pr_003 character varying(100),
  b06010pr_004 character varying(100),
  b06010pr_005 character varying(100),
  b06010pr_006 character varying(100),
  b06010pr_007 character varying(100),
  b06010pr_008 character varying(100),
  b06010pr_009 character varying(100),
  b06010pr_010 character varying(100),
  b06010pr_011 character varying(100),
  b06010pr_012 character varying(100),
  b06010pr_013 character varying(100),
  b06010pr_014 character varying(100),
  b06010pr_015 character varying(100),
  b06010pr_016 character varying(100),
  b06010pr_017 character varying(100),
  b06010pr_018 character varying(100),
  b06010pr_019 character varying(100),
  b06010pr_020 character varying(100),
  b06010pr_021 character varying(100),
  b06010pr_022 character varying(100),
  b06010pr_023 character varying(100),
  b06010pr_024 character varying(100),
  b06010pr_025 character varying(100),
  b06010pr_026 character varying(100),
  b06010pr_027 character varying(100),
  b06010pr_028 character varying(100),
  b06010pr_029 character varying(100),
  b06010pr_030 character varying(100),
  b06010pr_031 character varying(100),
  b06010pr_032 character varying(100),
  b06010pr_033 character varying(100),
  b06010pr_034 character varying(100),
  b06010pr_035 character varying(100),
  b06010pr_036 character varying(100),
  b06010pr_037 character varying(100),
  b06010pr_038 character varying(100),
  b06010pr_039 character varying(100),
  b06010pr_040 character varying(100),
  b06010pr_041 character varying(100),
  b06010pr_042 character varying(100),
  b06010pr_043 character varying(100),
  b06010pr_044 character varying(100),
  b06010pr_045 character varying(100),
  b06010pr_046 character varying(100),
  b06010pr_047 character varying(100),
  b06010pr_048 character varying(100),
  b06010pr_049 character varying(100),
  b06010pr_050 character varying(100),
  b06010pr_051 character varying(100),
  b06010pr_052 character varying(100),
  b06010pr_053 character varying(100),
  b06010pr_054 character varying(100),
  b06010pr_055 character varying(100),
  b06011_001 character varying(100),
  b06011_002 character varying(100),
  b06011_003 character varying(100),
  b06011_004 character varying(100),
  b06011_005 character varying(100),
  b06011pr_001 character varying(100),
  b06011pr_002 character varying(100),
  b06011pr_003 character varying(100),
  b06011pr_004 character varying(100),
  b06011pr_005 character varying(100),
  b06012_001 character varying(100),
  b06012_002 character varying(100),
  b06012_003 character varying(100),
  b06012_004 character varying(100),
  b06012_005 character varying(100),
  b06012_006 character varying(100),
  b06012_007 character varying(100),
  b06012_008 character varying(100),
  b06012_009 character varying(100),
  b06012_010 character varying(100),
  b06012_011 character varying(100),
  b06012_012 character varying(100),
  b06012_013 character varying(100),
  b06012_014 character varying(100),
  b06012_015 character varying(100),
  b06012_016 character varying(100),
  b06012_017 character varying(100),
  b06012_018 character varying(100),
  b06012_019 character varying(100),
  b06012_020 character varying(100),
  b06012pr_001 character varying(100),
  b06012pr_002 character varying(100),
  b06012pr_003 character varying(100),
  b06012pr_004 character varying(100),
  b06012pr_005 character varying(100),
  b06012pr_006 character varying(100),
  b06012pr_007 character varying(100),
  b06012pr_008 character varying(100),
  b06012pr_009 character varying(100),
  b06012pr_010 character varying(100),
  b06012pr_011 character varying(100),
  b06012pr_012 character varying(100),
  b06012pr_013 character varying(100),
  b06012pr_014 character varying(100),
  b06012pr_015 character varying(100),
  b06012pr_016 character varying(100),
  b06012pr_017 character varying(100),
  b06012pr_018 character varying(100),
  b06012pr_019 character varying(100),
  b06012pr_020 character varying(100) )
WITH (  OIDS=FALSE );
ALTER TABLE acs_survey_income  OWNER TO postgres;
-- Index: idx_acs_survey_income_1
-- DROP INDEX idx_acs_survey_income_1;
CREATE INDEX idx_acs_survey_income_1  ON acs_survey_income   USING btree   (logrecno COLLATE pg_catalog."default");
D)	Load downloaded files in their respective tables i.e. 
1.	Load Consumer_Complaints.csv into Consumer_Complaints table
2.	Load g20135us.csv into geography_survey table.
3.	Load e20135us0015000.txt & m20135us0015000.txt into acs_survey_income  table.
4.	Check the data in all the 3 tables and make sure they are valid.
E)	Open Postgres Sql editor and run the following sqls to generate reports and “export” the resultset as .csv file:
1.	Top 10 States having maximum complaints in last 5 years:
select state, count(*) as volume_of_complaints
from consumer_complaints
group by state
order by count(*) desc nulls last
limit 10;

2.	Top 10 Companies having maximum complaints in last 5 years
select Company, count(*) as volume_of_complaints
from consumer_complaints
group by company
order by count(*) desc nulls last
limit 10;

3.	Top 10 Products having maximum complaints in last 5 years:
select product, count(*) as volume_of_complaints
from consumer_complaints
group by product
order by count(*) desc nulls last
limit 10;

4.	Year/State wise break down of complaints:
CREATE EXTENSION tablefunc;
select * from crosstab(
  $$select to_char(Date_received,'yyyy') as complaint_received,state, COUNT(*)
  from consumer_complaints where state is not null
  group by to_char(Date_received,'yyyy'),state ORDER BY 1,2 $$,
  $$ select distinct state from consumer_complaints where state in ('CA',
'FL',
'TX',
'NY',
'GA',
'NJ',
'PA',
'IL',
'VA',
'MD') order by 1 $$
) as (
  year varchar,
  "CA" varchar,
"FL" varchar,
"TX" varchar,
"NY" varchar,
"GA" varchar,
"NJ" varchar,
"PA" varchar,
"IL" varchar,
"VA" varchar,
"MD" varchar
);

5.	Top 8 zip_code complaint volume vis-a-vis income analysis:
select (select distinct state from consumer_complaints cc_2 where cc_2.zip_code=x.zip_code and state is not null limit 1) as state, x.*
from (
 select (select zcta5 from geography_survey g where g.logrecno=c.logrecno) as zip_code,cast(c.b06010_001 as integer) as Total_population,cast(c.b06010_003 as integer),
 (cast(c.b06010_003 as  float8)/cast(c.b06010_001 as  float8))*100 as Earning_pop_percent,
 ((cast(c.B06010_009 as  float8)+cast(c.B06010_010 as  float8)+cast(c.B06010_011 as  float8))/cast(c.b06010_001 as  float8))*100 as Median_to_total_pop_percent,
 ((cast(c.B06010_009 as  float8)+cast(c.B06010_010 as  float8)+cast(c.B06010_011 as  float8))/cast(c.b06010_003 as  float8))*100 as Median_to_Earning_pop_percent
   from acs_survey_income_2 c
 where exists (select 1 
               from consumer_complaints A,
                    geography_survey B
               where  a.zip_code=b.zcta5 
                  and b.logrecno=c.logrecno
                  and c.filetype='2013e5' 
                  and a.zip_code in (select c1.zip_code from (select  cc.zip_code,count(*) as volume_of_complaints
							from consumer_complaints cc where cc.zip_code is not null
							group by  cc.zip_code 
							order by count(*) desc nulls last
							limit 10) c1
		              )
                )
         )x;

           
 
Top 10 States having maximum complaints in last 5 years           
           
State Volume_of_Complaints          
CA 62054          
FL 40370          
TX 30672          
NY 28719          
GA 18181          
NJ 17046          
PA 15000          
IL 14710          
VA 13490          
MD 13449          
           
Top 10 Companies having maximum complaints in last 5 years           
           
Company Volume_of_complaints          
Bank of America 48444          
Wells Fargo 34454          
JPMorgan Chase 27274          
Experian 21773          
Equifax 21348          
Citibank 20381          
Ocwen 17598          
TransUnion 16583          
Capital One 12627          
Nationstar Mortgage 10290          
           
Top 10 Products having maximum complaints in last 5 years           
           
Product Volume_of_complaints          
Mortgage 152886          
Debt collection 71399          
Credit reporting 62083          
Credit card 52202          
Bank account or service 48297          
Consumer loan 14258          
Student loan 12503          
Payday loan 2746          
Money transfers 2513          
Prepaid card 850          
           
           
Year/State wise break down of complaints           
           
Year CA FL TX NY GA NJ PA IL VA MD 
2011 446 247 99 82 69 90 208 85 149 88 
2012 11701 7008 3354 2588 2575 2998 5456 2460 3651 2176 
2013 16912 10634 4883 3649 3633 4504 7415 3923 7082 3408 
2014 21249 14590 6197 5321 4657 6163 10010 5488 13040 5218 
2015 11746 7891 3648 3070 2515 3291 5630 3044 6750 2600 
           
           
Top 8 zip_code complaint volume vis-a-vis income analysis           
           
State Zip_code Total_population Earning_population Earning_pop_percent Median_to_total_pop_percent Median_to_earning_pop_percent     
MI 48382 16788 14751 87.8663331 38.11651179 43.38010982     
AR 76116 37154 32753 88.15470743 19.07466222 21.63771258     
CA 92101 34462 30380 88.15506935 34.04909756 38.6240948     
CA 92626 43635 37456 85.83934915 31.31202017 36.47746689     
ME 20744 42346 37818 89.30713645 40.04392387 44.83843672     
ME 20774 35328 31417 88.92946105 42.83004982 48.16182322     
GA 33071 30403 25899 85.18567247 27.6946354 32.51090776     
FL 33173 29703 24906 83.85011615 19.32464734 23.04665542     
 
