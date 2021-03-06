A simple and focused javascript library which supports basic URL parsing
and 'url prefix' testing.

The first feature of urlmatch is its ability to parse a url into components:

    console.log(URLParse("http://google.com/"));
    {
        "directory": "/",
        "path": "/",
        "relative": "/",
        "host": "google.com",
        "authority": "google.com",
        "scheme": "http",
        "source": "http://google.com/"
    }

urlmatch can also validate urls:

    $ URLParse("httpe://www.google.com/").validate();
    Error: invalid url: unsupported scheme: httpe

can also normalize urls:

    $ URLParse("http://www.google.com:80/foo/../bar/").normalize();
    http://www.google.com/bar/

can reliably extract the origin of a url:

    $ URLParse("http://www.google.com:80/foo/../bar/").normalize().originOnly().toString();
    http://www.google.com

And finally, urlmatch can combine all of these features to support
robust url prefix matching:

    $ URLParse("http://doma.in/appscope/").contains("http://doma.in/appscope/somepath/../../attack.html");
    false
    $ URLParse("http://doma.in/appscope/").contains("http://doma.in/appscope/somepath/../not_attack.html");
    true

## In Browser Usage

    <script src="urlparse.js"></script>
    <script>
      console.log(window.URLParse("https://github.com/lloyd/urlparse.js"));
    <script>

## NodeJS Usage

Install it:

    $ npm install urlparse

Use it:

    #!/usr/bin/env node

    const urlparse = require('urlparse');

    console.log(urlparse("https://github.com/lloyd/urlparse.js"));

