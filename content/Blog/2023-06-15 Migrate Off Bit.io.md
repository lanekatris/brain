I'm planning to move from https://bit.io to https://neon.tech/ as bit.io is shutting down. They were pretty cool, I didn't have any issues. 

# To Do
- [x] Pg export ✅ 2023-06-15
- [x] Pg import into neon ✅ 2023-06-15
**To Do**: [[Aquarium IoT Rewrite]] needs its lambda connection string updated

# Notes
- Being on Windows I couldn't just download `pg_restore`... That is unfortunate
- Docker doesn't do me any good either for the most part, it still takes effort
- Datagrip was wanting a binary to all `pg_restore` with [this article](https://www.jetbrains.com/help/datagrip/import-data.html#restore-a-full-dump-for-mysql-and-postgresql)...
- I decided to just copy tables as desired now
- Since bit.io is going away I can't just live copy tables...
- [This article](https://stackoverflow.com/questions/33854798/how-do-i-install-just-the-client-tools-for-postgresql-on-windows) let me know I can just install CLI tools which is all I needed for Windows

> [!NOTE] UX Note on enterprisedb.com
> I thought there wasn't a download for Windows but it was just there wasn't one for 32 bit... don't be like me

- Added to my path: `C:\Program Files\PostgreSQL\15\bin` - not fully necessary

![[Pasted image 20230615215600.png]]


![[Pasted image 20230615215815.png]]