[[Disc Golf Course Map Overlay]] - **Cancelled** because of performance issues in GAIA/Chrome
[[Disc Golf Projects#Disc Golf Course Dataset Generation]]
[[Disc Golf Projects#Disc Golf Tournament Analyzer]]
[[2023-09-15 Disc Database]]
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