Go here: https://udisc.com/blog/post/worlds-best-disc-golf-courses-2023

```
var script = document.createElement('script');
script.src = 'https://code.jquery.com/jquery-3.6.3.min.js'; // Check https://jquery.com/ for the current version
document.getElementsByTagName('head')[0].appendChild(script);
```

```
var el = $('tbody')
var a = []
el.last().children('tr').each((i,el)=>{
    if (i==0) return
    const data = {source: 'https://udisc.com/blog/post/worlds-best-disc-golf-courses-2023'}
    $(el).children('td').each((i2,el2) => {
        if (i2 === 1) data.name = $(el2).children('a').text()
        if (i2 === 1 ) data.udiscId = $(el2).children('a').attr('href').replace('https://udisc.com/courses/','')
        if (i2 === 1 ) data.url = $(el2).children('a').attr('href')
        if (i2 === 2) data.city = $(el2).text()
        if (i2 === 3) data.state = $(el2).text()
        if (i2 === 4) data.country = $(el2).text()
    })

    console.log(data)
    a.push(data)
})

a
```

Right click the object and *copy object*

Go here: https://www.convertcsv.com/json-to-csv.htm

Paste your JSON and download result

> [!tip] I uploaded this CSV to Noco DB


I thought about using some web scraping frameworks but it seemed like overkill for this one time thing. A few I looked at:
- https://www.octoparse.com/
- https://apify.com/