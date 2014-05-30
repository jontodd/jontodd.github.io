This is my tech blog.

## Blog Operations

Run blog locally

~~~ bash
# Start server in background watching _site for chages
jekyll serve --watch --detach 
open http://127.0.0.1:4000
kill -9 $(pgrep jekyll) 
~~~

Deploy

~~~ bash
git push
open http://jontodd.github.io
~~~
