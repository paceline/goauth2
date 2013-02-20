# goauth2

Fork of the [goauth2](http://code.google.com/p/goauth2) project, allowing the library to be used in Google App Engine hosted projects (as I do for [autosite-go](http://github.com/paceline/autosite-go))

# Install
Just check out or download the source code from its GitHub repository and copy it to your project's root directory. Import in your GO code like you would any other library:
```Go
import (
    "appengine"
    "appengine/urlfetch"
    "github.com/paceline/goauth2/oauth"
    ...
)
```

# Usage
For the most part things work just like shown it the examples [here](http://code.google.com/p/goauth2/source/browse/oauth/example/oauthreq.go) or [here](https://gist.github.com/border/3579615). However you need to supply urlfetch.Transport manually, e.g.:
```Go
func(w http.ResponseWriter, r *http.Request) {
    c = appengine.NewContext(r)
    config := &oauth.Config{
        ClientId:     *clientId,
        ClientSecret: *clientSecret,
        Scope:        *apiURL,
        AuthURL:      "https://accounts.google.com/o/oauth2/auth",
        TokenURL:     "https://accounts.google.com/o/oauth2/token",
        TokenCache:   oauth.CacheFile(*cachefile),
	}
	transport := &oauth.Transport{Config: config, Transport: &urlfetch.Transport{Context: c}}
	...
}
```
