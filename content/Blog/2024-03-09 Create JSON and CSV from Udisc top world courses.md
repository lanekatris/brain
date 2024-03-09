---
title: Generate JSON and CSV file from Udisc Top Courses
date: 2024-03-09
---
# Goal

I wanted to take the data in the HTML table on [Udisc's blog post](https://udisc.com/blog/post/worlds-best-disc-golf-courses-2024) and load it into my `places` table so I can make a goal on visiting all the courses. I then could keep track of how many I have visited.

# Downloads

I've already created these [JSON](https://github.com/lanekatris/monorepo/blob/main/data/udisc-worlds-best-disc-golf-courses-2024.json) and [CSV](https://github.com/lanekatris/monorepo/blob/main/data/udisc-worlds-best-disc-golf-courses-2024.csv) files on GitHub.

# Steps

#### Create JSON File

Go to the [post](https://udisc.com/blog/post/worlds-best-disc-golf-courses-2024)

Run this in Chrome DevTools:
```javascript
var rows = document.querySelectorAll('tbody')[7].querySelectorAll('tr')
var a = []; 
for (var i = 0; i < rows.length; i++) {  
  if (i > 1) {  
    if (!rows[i].children[1]) continue; // There are empty <tr> rows  
    a.push({
        rank: +rows[i].children[0].textContent,
      name: rows[i].children[1].children[0].text,  
      url: rows[i].children[1].children[0].href,  
      udisc_id: rows[i].children[1].children[0].href.replace('https://udisc.com/courses/', ''),  
      source: 'https://udisc.com/blog/post/worlds-best-disc-golf-courses-2024'  
    });  
  }  
}
copy(a)
```

You know have the data on your clipboard to paste wherever.

#### Create a CSV File

I cheat and use `json2csv` to create the CSV:
```bash
npm i -g json2csv

json2csv -i udisc-worlds-best-disc-golf-courses-2024.json -o udisc-worlds-best-disc-golf-courses-2024.csv
```

> [!NOTE]
> Yes, I know I'm using `var`, this lets you rerun the whole block of code over and over with no `const` errors. Yes, it could be refactored by using a variable, it could also be de-structured to be cleaner. No need to spend a lot of effort on one-offs 😉

#### Loading into SQL

#todo Need to define how I got the CSV into Postgres, I'm using the DataGrip GUI for now.

Once it was in Postgres I ran:
```sql
insert into neondb.noco.place (name, source, udisc_id, url)  
select t.name, t.source, t.udisc_id, t.url  
from neondb.random.udisc_worlds_best_disc_golf_courses_2024_2 t  
         left join neondb.noco.place p on t.udisc_id = p.udisc_id  
where p.id is null
```

Now I have places loaded in SQL 🎉