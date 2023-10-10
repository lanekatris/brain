# Use Case
> I want to easily alter and generate data to upload into gaia

# Requirements
- Limit 1000 features per file
- Manually attribute courses so I can filter them out of maps

# Stretch Goals
- Automate knowing which courses I've played
- after uploading a disc, ild like to know what changed (temporal query)

# Problems
GAIA doesn't handle all the waypoints very well, I got out of memory errors - Potential solution is split up **waypoints by state**

# Tasks
#### Data Attribution
> Has played course?
- [x] Load all courses into ESDB (test max events can insert) ✅ 2022-07-03
- [x] Load udisc played courses ✅ 2022-07-04
- [x] Create mappings from Udisc to PDGA in db ✅ 2022-07-04
- [x] create course played events ✅ 2022-07-04
- [x] ~~mapping ui~~ and api ✅ 2022-07-04
	- [x] Show played courses ✅ 2022-07-04

> I don't have a round for certain courses I've played, I'd like to see this captured
- [x] Create events for `CoursePlayed` with a source of `Scorecard` or `Manual` ✅ 2022-07-04
- [x] UI / API ✅ 2022-07-04

> I don't want to play here (exclude)
- [x] create structure for course ignored ✅ 2022-07-04
- [x] course ignored ui and api ✅ 2022-07-04

> I want the map to allow me to filter out played courses or color them differently
- [x] When getting all courses, attribute with played ✅ 2022-07-05
- [x] ", attribute with excluded ✅ 2022-07-05
- [x] When exporting filter out played and excluded ✅ 2022-07-09
- [x] Rename the parsed course and the esdb course eh? ✅ 2022-07-11
- [x] All buckets referenced need to be in constants.ts and a module init needs added to make sure the buckets exist ✅ 2022-07-11

> I need to easily know the name and id of the courses to exclude (course search)
- [x] Create way or link off to pdga to be able to search for course names ✅ 2022-07-16

> I need a way to say I've played a course without having a scorecard for it
- [x] Do same thing as excluded ✅ 2022-07-17

#### Cancelled
Create ingress for minio (both ports)
Use password from secret in yaml
 Once prod masterchief is done getting all the HTML from pdga.com, let's create a zip of that and put it on S3 just in case
Create a preview functionality for thi sdata load
 Create an apply functionality for this data load

> When you are auditing your disc golf purchases on Amazon you can easily search like [this](https://www.amazon.com/gp/your-account/order-history/ref=ppx_yo2ov_dt_b_search?opt=ab&search=disc)

# Snippets

If you need to filter data from CLI:
```
cat ..\..\data\discs-source.json | jq -c '.[] | select(.model == "Truth" and .color == "Blue")'
```