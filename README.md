# sample-app-mongoid-cache
This is a sample repo for checking if Fragment Cache would work with Mongoid instance itself as cache key.

Please see the PR for the detail. https://github.com/FumiyaShibusawa/sample-app-mongoid-cache/pull/2

## How to reproduce

```
$ git clone git@github.com:FumiyaShibusawa/sample-app-mongoid-cache.git
$ cd sample-app-mongoid-cache
$ bundle install
$ rails c
  > User.create(email: "hoge@example.com", name: "hoge")
$ rails s
```

After following the above those steps, go to 0.0.0.0:3333, then it will crash.
