I wanted to play with charts with Kibana.

```bash
docker run -d --name=grafana -p 3000:3000 grafana/grafana
```

The table I wanted to go against was in a different schema than `dbo`.

I found that I needed to create a different "role" (not sure the difference between "role" and a "user") in Neon and then [change the default schema](https://www.commandprompt.com/education/how-do-i-setchange-the-default-schema-in-postgresql/) for that user.

`ALTER DATABASE db_name SET search_path TO schema_name;`

I then set up the data connection in Kibana with this different user and they can see the table I wanted.
