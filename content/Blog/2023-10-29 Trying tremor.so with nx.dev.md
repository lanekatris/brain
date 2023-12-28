This [Vercel template](https://vercel.com/templates/next.js/admin-dashboard-tailwind-postgres-react-nextjs) came across my Google feed and gave me inspiration. So, I wanted to try things out. I really like this abstraction which I consider more like [MUI](https://mui.com/) compared to the raw classes of tailwind.

> [!info] I'm using https://nx.dev/ so the default directions [here](https://www.tremor.so/docs/getting-started/installation) from tremor.so didn't work for me

Add Tailwind via [this](https://nx.dev/recipes/react/using-tailwind-css-in-react):
```
nx g @nx/react:setup-tailwind --project=<your app here>
```

You need to alter your `content` addition to your `tailwind.config.js`:
```
join(__dirname, '../../node_modules/@tremor/**/*.{js,ts,jsx,tsx}')
```

Run the app with the fancy Rust compiler:

> [!danger] This doesn't work for me 
```
node_modules/.bin/nx serve web --turbo 
```


I have to do the usual:
```
node_modules/.bin/nx serve web
```


- [x] update nextjs to v14 ✅ 2023-10-29