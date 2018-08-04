# sample-app-mongoid-cache
This is a sample repo for checking if Fragment Cache would work with Mongoid instance itself as cache key.

Please see the PR for the detail. https://github.com/FumiyaShibusawa/sample-app-mongoid-cache/pull/2

## How to reproduce

First, you need to have mongodb installed in your machine.

```
$ git clone git@github.com:FumiyaShibusawa/sample-app-mongoid-cache.git
$ cd sample-app-mongoid-cache
$ bundle install
$ rails c
  > User.create(email: "hoge@example.com", name: "hoge")
$ rails s
```

After following the above those steps, go to 0.0.0.0:3333, then it will crash.

## stacktrace
```
Started GET "/" for 127.0.0.1 at 2018-08-01 23:59:06 +0900
Processing by UsersController#index as HTML
  Rendering users/index.html.erb within layouts/application
MONGODB | EVENT: #<Mongo::Monitoring::Event::TopologyOpening topology=Unknown>
MONGODB | Topology type 'unknown' initializing.
MONGODB | EVENT: #<Mongo::Monitoring::Event::ServerOpening address=localhost:27017 topology=Unknown>
MONGODB | Server localhost:27017 initializing.
MONGODB | EVENT: #<Mongo::Monitoring::Event::TopologyChanged prev=Unknown new=Single>
MONGODB | Topology type 'unknown' changed to type 'single'.
MONGODB | EVENT: #<Mongo::Monitoring::Event::ServerDescriptionChanged>
MONGODB | Server description for localhost:27017 changed from 'unknown' to 'standalone'.
MONGODB | EVENT: #<Mongo::Monitoring::Event::TopologyChanged prev=Single new=Single>
MONGODB | There was a change in the members of the 'single' topology.
MONGODB | localhost:27017 | sample_app_mongoid_cache_development.find | STARTED | {"find"=>"users", "filter"=>{}}
MONGODB | localhost:27017 | sample_app_mongoid_cache_development.find | SUCCEEDED | 0.007s
Read fragment views/users/index:5bb9c14e255656db576fb60bfc3138ac/users/5b61c8b34cfad12270b6689a (15.8ms)
  Rendered users/index.html.erb within layouts/application (41.1ms)
Completed 500 Internal Server Error in 84ms



SystemStackError (stack level too deep):

app/views/users/index.html.erb:10:in `block in _app_views_users_index_html_erb___4253829445550396588_70166155779880'
app/views/users/index.html.erb:9:in `_app_views_users_index_html_erb___4253829445550396588_70166155779880'
^C/Users/basicinc/.rbenv/versions/2.3.3/lib/ruby/gems/2.3.0/gems/web-console-3.6.2/lib/web_console/middleware.rb:20: [BUG] vm_call_cfunc - cfp consistency error
ruby 2.3.3p222 (2016-11-21 revision 56859) [x86_64-darwin15]
```
