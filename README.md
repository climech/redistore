# redistore

A fork of [redistore](http://www.godoc.org/gopkg.in/boj/redistore.v1), a session store backend for [gorilla/sessions](http://www.gorillatoolkit.org/pkg/sessions). It uses [go-redis](github.com/go-redis/redis/v8) instead of [redigo](https://github.com/gomodule/redigo).

## Requirements

Depends on the [go-redis](github.com/go-redis/redis/v8) library.

## Installation

    go get github.com/toshjk/redistore

## Documentation

See http://www.gorillatoolkit.org/pkg/sessions for full documentation on underlying interface.

### Example
``` go
// Fetch new store.
store, err := NewRediStore(":6379", "", []byte("secret-key"))
if err != nil {
	panic(err)
}
defer store.Close()

// Get a session.
session, err = store.Get(req, "session-name")
if err != nil {
	log.Error(err.Error())
}

// Add a value.
session.Values["foo"] = "bar"

// Save.
if err = sessions.Save(req, rsp); err != nil {
	t.Fatalf("Error saving session: %v", err)
}

// Delete session.
session.Options.MaxAge = -1
if err = sessions.Save(req, rsp); err != nil {
	t.Fatalf("Error saving session: %v", err)
}

// Change session storage configuration for MaxAge = 10 days.
store.SetMaxAge(10 * 24 * 3600)
```
