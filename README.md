# miniature-palm-tree

To reproduce the Sprockets issue, run:

	`bundle exec rake assets:precompile`

Then note both the logfiles for generating the assets and the contents
of the Sprockets manifest:

```
...
match_path_extname: returning .default.html, {:type=>"text/html", :engines=>[], :pipeline=>"default"}
parse_path_extnames: .default.html, {:type=>"text/html", :engines=>[], :pipeline=>"default"}
in find_asset: /Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default.html
Sprockets::Resolve#resolve: path=/Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default.html, options={}
resolve_absolute_path: /Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default.html
match_path_extname: returning .default.html, {:type=>"text/html", :engines=>[], :pipeline=>"default"}
parse_path_extnames: .default.html, {:type=>"text/html", :engines=>[], :pipeline=>"default"}
got URI: file:///Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default.html?type=text/html
Sprockets::Loader#load: file:///Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default.html?type=text/html
I, [2019-06-10T15:50:15.551166 #39707]  INFO -- : Writing /Users/rafal/dev/sprockets-test/public/assets/templates/header-e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.html
I, [2019-06-10T15:50:15.551279 #39707]  INFO -- : Writing /Users/rafal/dev/sprockets-test/public/assets/templates/header-e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.html.gz
```

NOTE the above generates a `.../header-<shadigest>.html`, stripping out the
".default" from the original source filename.

Continuing...

```
match_path_extname: returning .html, {:type=>"text/html", :engines=>[], :pipeline=>nil}
parse_path_extnames: .html, {:type=>"text/html", :engines=>[], :pipeline=>nil}
in find_asset: /Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default_view.html
Sprockets::Resolve#resolve: path=/Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default_view.html, options={}
resolve_absolute_path: /Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default_view.html
match_path_extname: returning .html, {:type=>"text/html", :engines=>[], :pipeline=>nil}
parse_path_extnames: .html, {:type=>"text/html", :engines=>[], :pipeline=>nil}
got URI: file:///Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default_view.html?type=text/html
Sprockets::Loader#load: file:///Users/rafal/dev/sprockets-test/app/assets/javascripts/templates/header.default_view.html?type=text/html
I, [2019-06-10T15:50:15.553671 #39707]  INFO -- : Writing /Users/rafal/dev/sprockets-test/public/assets/templates/header.default_view-e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.html
I, [2019-06-10T15:50:15.554242 #39707]  INFO -- : Writing /Users/rafal/dev/sprockets-test/public/assets/templates/header.default_view-e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855.html.gz
```

whereas in this case, where the file name does not match ".default.html", 
the full base filename is used before the digest is appended.

