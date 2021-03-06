# Caching Layer for Node-GitHub

This is a Node.JS module that transparently adds caching for the [node-github](https://github.com/mikedeboer/node-github) project.

**Note:** Version 1.0.0 is in testing and is the current code in **master**. Many changes were made from 0.3.0 to 1.0.0 in caching behavior. If you upgrade or use the master branch, delete your cache database folder before upgrade to avoid conflicts.

## Installation

Install with Node.JS package manager

```
$ npm install github-cache
```

## Documentation

You use this class just like you would use [node-github](https://github.com/mikedeboer/node-github). 

If you want to not use the cache at any time, add `cache: false` to your API call.

## Settings

1. `cachedb` - this is a value passed to the creation of the API object, it is a path to a location to store the cached data.
2. `cache` - this is a value that can be passed to any API function with a boolean value to disable or enable the cache. `Default: true`
3. `validateCache` - `Default: true` - Check cached etag using `If-None-Match` with GitHub API before using the cached data. Ensures you have the latest data at all times. Setting to `false` allows you to use cached data without making the API call, results in quicker lookups. Especially useful if you are making dozens of API calls or more.

## Example

```javascript
var GitHubApi = require("github-cache");

var github = new GitHubApi({
  version: "3.0.0",
  debug: true,
  cachedb: './cachedb',
  validateCache: true
});

github.user.getFollowingFromUser({
  user: "ekristen",
  cache: false
}, function(err, res) {
  console.log(JSON.stringify(res));
});

github.orgs.getTeams({
  org: 'private',
  validateCache: false
}, function(err, teams) {
  console.log(teams);
});

```
