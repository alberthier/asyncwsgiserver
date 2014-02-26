# Asyncore based WSGI server

The asyncwsgiserver module integrates a WSGI web server with asyncore.
Using this module allows you to integrate any WSGI application in an asyncore event loop.

Basic example:

```python
#!/usr/bin/env python

import asyncore
import asyncwsgiserver


def hello_app(environ, start_response):
    """ Simple WSGI application """
    status = '200 OK'
    response_headers = [('Content-type', 'text/plain')]
    start_response(status, response_headers)
    return [b'Hello world!\n']


if __name__ == "__main__":
    # Create the web server on port 8000
    port = 8000
    print("Open http://localhost:" + str(port))
    asyncwsgiserver.WsgiServer("", port, hello_app)
    try:
        # Start asyncore's event loop
        asyncore.loop()
    except KeyboardInterrupt:
        pass
```

