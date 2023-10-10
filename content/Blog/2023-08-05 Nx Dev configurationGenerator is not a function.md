`nx g @nx/next:app web`

When I was trying to create a new Next.js app in a nx.dev workspace I was getting: 

```

 >  NX   configurationGenerator is not a function


TypeError: configurationGenerator is not a function
    at /home/lane/git/monorepo/software/js/node_modules/@nx/next/src/generators/application/lib/add-jest.js:13:32
    at Generator.next (<anonymous>)
    at /home/lane/git/monorepo/software/js/node_modules/tslib/tslib.js:169:75
    at new Promise (<anonymous>)
    at Object.__awaiter (/home/lane/git/monorepo/software/js/node_modules/tslib/tslib.js:165:16)
    at addJest (/home/lane/git/monorepo/software/js/node_modules/@nx/next/src/generators/application/lib/add-jest.js:8:20)
    at /home/lane/git/monorepo/software/js/node_modules/@nx/next/src/generators/application/application.js:27:55
    at Generator.next (<anonymous>)
    at fulfilled (/home/lane/git/monorepo/software/js/node_modules/tslib/tslib.js:166:62)
    at process.processTicksAndRejections (node:internal/process/task_queues:95:5)
```

Looks like a **jest** issue...

Well, I don't really unit test on persoanl projects unless I really need to so I thought I'd skip test project creation/support with:

```
nx g @nx/next:app web --verbose --e2eTestRunner none --unitTestRunner none
```

And my project was added successfully!