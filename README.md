# Generating a task list for a CA tool

## Uses the following repo to scrape the list: 
https://github.com/osrs-reldo/task-scraper

## How to scrape CA json using task scraper:
### Set up node
```bash 
    nvm install 22.4.0
    nvm use 22.4.0
    npm install
```
### Download the local Cache:
```bash
    npm run cli -- cache update
```

### Local code changes I had to make:
#### After running the cache update 
```bash
    cd osrs-cache
    pwd
```
#### export the result of this `pwd` command to an env variable:
```bash 
    export CACHE_DIR=<pwd result>
```
#### update two files to look for your exported variable:

`src/app.service.ts` line 25 & `src/core/cache-provider.module.ts` line 28

```typescript
    new NodeFSFileProvider(process.env.CACHE_DIR || path.resolve(__dirname, '../../osrs-cache'))
```

### Generate the JSON file:
```bash
    mkdir out
    npm run build
    npm run cli -- cache update
    npm run cli -- tasks combat --json --legacy
```

