# commit-analyzer-wildcard
Wildcard commit analyzer for [semantic-release](https://github.com/semantic-release/semantic-release) to find substrings in each commit message.

## Installation
* Using NPM
```bash
> npm install -D @khala/commit-analyzer-wildcard
```
* Using yarn
```
> yarn add -D @khala/commit-analyzer-wildcard
```

Then add it to your `release` options

* `package.json`
```JSON
{
  "release": {
    "analyzeCommits": "@khala/commit-analyzer-wildcard/analyzer"
  }
}
```
* `.releaserc`
```JSON
{
  "analyzeCommits": "@khala/commit-analyzer-wildcard/analyzer"  
}
```

## Default usage
Simply add some special characters to any of your commit messages and new release will be triggered
* Major - `<x.x.x>` or `<x.x.?>` or `<x.?.x>` or `<x.?.?>`
* Minor - `<?.x.x>` or `<?.x.?>`
* Bug - `<?.?.x>`
* No release - `<no>`

To trigger automatic release add this to `package.json` and install [semantic-release](https://www.npmjs.com/package/semantic-release)
```JSON
{
  "scripts": {
    "release": "semantic-release"
  }
}
```

Settings for travis is
```YML
after_success:
- npm run release
```

## Options

To change default patterns you can pass your own in your release option.
```JSON
{
  "release": {
    "analyzeCommits": [
      {
        "path": "@khala/commit-analyzer-wildcard/analyzer",
        "patterns": {
          "major": "<x.[x|?].[x|?]>",
          "minor": "<?.x.[x|?]>",
          "patch": "<?.?.x>",
          "noRelease": "<no>"
        } 
      }
    ]
  }
}
```

Each pattern is transfered into Regular Expression and searched in each commit message.
