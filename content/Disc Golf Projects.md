[[Disc Golf Course Map Overlay]] - **Cancelled** because of performance issues in GAIA/Chrome
[[Disc Golf Projects#Disc Golf Course Dataset Generation]]
[[Disc Golf Projects#Disc Golf Tournament Analyzer]]
[[2023-09-15 Disc Database]]

> This disc golf service - every transition change is captured, why'd you buy a new disc, you moved from in bag to missing, how'd that happen. Could be simple sqlite and golang/nextjs or temporal etc. - expose CSV and RSS feed, or the disc lineage idea like blockchain, like trading discs with JJhackn.

> I envision kestra, windmill, or temporal to generate my list of datasets and populate disc golf course dataset and let me know, also knowing courses I've played notification. Maybe a notification that is idempotent, Lane went to a new course. Or this could be rendered on the feed and highlighted as new course, and this could be charted in graph

> [!error] I have to manually delete a record because there are 2 `Par` users for a round. 

> [!error] My udisc parser doesn't match Udisc any more, need to fix this

- [x] Show one stat from my udisc scorecard parser ✅ 2024-03-03
- [x] put name on crave found ✅ 2024-03-03
- [x] compare escape, avenger ss, sidewinder, gstar mystere ✅ 2024-03-03
- [x] go thru and update what's in my bag ✅ 2024-03-03

- [ ] display a unique list of courses and potentially search
- [ ] I would like to join and be able to filter my discs by "mid-range"
- [ ] add forgotten list to the daily note template
- [ ] what is my current goal for disc golf, link to disc golf and link to now in blog.... Turnover and backhand form
- [ ] I would like to click the brand and filter my discs same as Marshall Street 
- [ ] talk about having 2 of them, so red rhyno and white factory second
- [ ] explain that deputy's are my main putter and I have 5, well 6 (do format like corey ellis' in the bag, what info he gives/questions asked)
- [ ] tennis ball to help my cart
- [ ] it would be cool to do disc transactions to keep track of lineage like toro - and like integrating my lkat modules with disc golf to fitness to feed, all enable then data sync
- [ ] compare toro and pig, image recognition training to load your discs if you don't want to do it manually
- [ ] add to gear, I have a camo dd disc tube
- [ ] bring disc golf links from raindrop to blog
- [ ] process for lost discs queue
- [ ] discs could live as workflow in temporal forever, like I took pig out cuz I have a toro and a rhyno already
- [ ] Disc Golf Stickers Idea

# Disc Golf Course Dataset Generation

**To Do**
- [x] Bring in code to the monorepo and refactor ✅ 2023-07-29
- [x] Move my database file elsewhere, into the data folder ✅ 2023-07-29
- [ ] Load individual course data to pull html and pluck off whatever
	- [ ] Load map link
	- [ ] Load lat/long
- [ ] Set individual course data in sqlite
- [ ] Create csv
- [ ] How to know you have latest data from pdga.com
- [ ] Use the latest course approach, so we can poll for new data and update
- [ ] Figure out why I'm one course off
- [ ] Link off to kaggle since the db will be to big, and warn them to get the db if its not there already so we don't needlessly hammer their server

#### Why web scrape PDGA?

There are no APIs or public datasets to my knowledge; so I have to resort to web scraping.

In my mind there are 3 sources of disc golf course data:
- Udisc
- Pdga.com
- discgolfscene.com

Udisc.com is the #1 choice I think in disc golf data, but it is modern. Using a SPA experience makes scrapingi data from them difficult.

discgolfscene.com is more old school with SSR but their search is not as powerful as pdga.com.

pdga.com has the best search with SSR. Because of this, I think it is easiest to pull data from.

Also, if there ever was a concern about data being up to date, in respects to tournaments; the PDGA would have to have data on a course for a sanctioned tournament. So *they* are the master of course data in my opinion. I imagine there are integrations with the other sites behind the scenes, but being *the* organization makes me feel that using them as a source is a good choice.

## Design Decisions

**Singiular Approach**
I don't want to abuse their webservers. I want to call them as little as possible. So, every call I do make I cache locally to not abuse. I could use parallelism to speed up data ingestion but there is no need, I can be patient.

**Cacheing**
Mentioned above, I want to call them as little as possible, so I cache every request to them to not make it again unless needed.

Another benefit with having a copy of the HTML locally is testing your query selectors. Having the the html locally, you can create easy unit tests for edge cases.



### Nice To Have
- [ ] Notification component if there is a new course based on your location filters
- [ ] Course count by state
- [ ] Load world wide data, only 3k more than US


# Stats

#### First Load
Loading 7636 individual courses took synchronously ~ 10106 seconds (2.8 hours), average 1.5s for each course to load

The code I brought over, actually had 0 errors, so I just let it run and it chugged along

Currently, without loading course detail data into the db, sqlite is: **589 MB** (of course the majority of that is the html responses I capture)


# Disc Golf Tournament Analyzer

This would use discgolfscene.com, still thinking on this...

# Log

**2024-03-02**
- [ ] Might need to verify the schema of this file: https://memos.lkat.io/m/je64HP5zjTBLtzMfXmJmHC