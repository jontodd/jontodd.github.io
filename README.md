This is my tech blog.

## Blog Operations

Run blog locally

~~~ bash
# Start server watching _site for chages
jekyll serve --watch 
open http://127.0.0.1:4000
# Edit files, server will auto-refresh
kill -9 $(pgrep jekyll) 
~~~

Deploy

~~~ bash
git push
open http://jontodd.github.io
~~~
