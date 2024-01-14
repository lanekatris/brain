# Goal

Explore Spotify data. I'd like to:

- View stats about my listening history
- View my listening history
	- Would be nice to be able to search
- List the podcasts I listen to
	- Ideally I'd like an RSS feed of updates to my Podcast feed. Things like "followed new podcast xxx on x date"

# Design

1. Put the exported files into PostgreSQL so it's easy to query and slice and dice to display

# Issues

My beloved #datagrip wasn't working importing a CSV to #neonpostgres with the error:
![[Pasted image 20240113121202.png]]

I'm not sure why... so I had to go the `psql` CLI route 🤷‍♂️

# TODO cat4egforize the below

Get list of podcasts from spotify and migrate to other app (kicked off export 2024-01-06 2:52pm) ([dataframed](https://open.spotify.com/show/02yJXEJAJiQ0Vm2AO9Xj6X) addition) (downloaded spotify data on 1-9-24)


I only exported a years worth of data.

I'd like to be able to search my listen history.

**Primary Goal**
Get a list of all the podcasts I follow, curate, add to AntennaPod app. Expose a OPML download. Expose a markdown list.


**To Do**



# Generate Podcast List

The file we want is `YourLibrary.json`

Install dependencies:

[Install `psql`](https://www.linuxtechi.com/how-to-install-postgresql-on-ubuntu/)

```
npm install -g @json2csv/cli
```

Get it in a CSV format to load:

```
cat YourLibrary.json | jq -r '.shows' > your-library-just-shows-v1.json

json2csv -i your-library-just-shows-v1.json -o your-library-just-shows-v1.csv
```

Load it:

```
psql YOUR_CONNECTION_STRING

create table spotify_podcasts (  
    name text,  
    publisher text,  
    uri text  
);

\copy spotify_podcasts FROM '/home/lane/Desktop/Spotify Account Data/your-library-just-shows-v1.csv' DELIMITER ',' CSV HEADER
```

# Random

```
# Run a random inline sql script
psql -c "select * from spotify_streaming_history" YOUR_CONNECTION_STRING

# Run a random sql script
psql -f ./test-script.sql YOUR_CONNECTION_STRING
```

# To Dos

- [x] Create stats and show in nextjs ✅ 2024-01-13
- [ ] Create opml page manually or with [library](http://scripting.com/code/opmlpackage/examples/browser/)
- [x] Generate URL to spotify like so: `https://open.spotify.com/show/2GFqbdH3xEtu0ZKUP6tr13` ✅ 2024-01-13
- [ ] export from the open podcast app to see the format for opml
- [ ] need flyway or something for this schema

# Brain Dump

* [Import | DataGrip Documentation](https://www.jetbrains.com/help/datagrip/import-data.html#import_csv)
* [Import | DataGrip Documentation](https://www.jetbrains.com/help/datagrip/import-data.html#import_dialogs)
* [Neon data import guides - Neon Docs](https://neon.tech/docs/import/import-intro)
* [Import data from CSV - Neon Docs](https://neon.tech/docs/import/import-from-csv)
* [milliseconds to hours - Google Search](https://www.google.com/search?q=milliseconds+to+hours&oq=milliseconds+to+hou&gs_lcrp=EgZjaHJvbWUqDQgAEAAYgwEYsQMYgAQyDQgAEAAYgwEYsQMYgAQyBggBEEUYOTIHCAIQABiABDIHCAMQABiABDIHCAQQABiABDIHCAUQABiABDIHCAYQABiABDIHCAcQABiABDIHCAgQABiABDIHCAkQABiABKgCALACAA&sourceid=chrome&ie=UTF-8)
* [expand nested array into rows? · Issue #139 · zemirco/json2csv](https://github.com/zemirco/json2csv/issues/139)
* [@json2csv/cli - npm](https://www.npmjs.com/package/@json2csv/cli)
* [How to Convert from JSON to CSV at The Command Line - Earthly Blog](https://earthly.dev/blog/convert-to-from-json/)