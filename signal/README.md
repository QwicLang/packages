# Signal

Signal is the HTTP routing package for Qwic. It provides function-based routes,
typed path parameters, JSON request validation, and structured responses on top
of Qwic's native HTTP/1.1 runtime.

## Install

```bash
qwic install signal
```

Packages are installed once in the shared Qwic package directory and can then
be imported by any project.

## Example

```qwic
import signal

public func getUser(req: signal.Request): any {
    const id = req.params["id"]
    return signal.Response.new(200, {
        "userId": id,
        "name": "Qwic User " + id.to_string(),
    })
}

public func main() {
    const app = signal.App.new()
    app.routes([
        {"path": "/user/{id:int}", "method": "GET", "handler": getUser},
    ])
    app.run(8080)
}
```

## Request Validation

```qwic
public func createItem(req: signal.Request): any {
    try {
        const data = req.body.validate({"title": "string", "priority": "int"})
        return signal.Response.new(201, {"status": "created", "item": data})
    } catch (error) {
        return signal.Response.new(400, {"error": error})
    }
}
```

## Current Runtime Limits

Signal currently uses Qwic's synchronous HTTP/1.1 listener. TLS, streaming,
keep-alive, chunked request bodies, concurrent request handling, middleware,
and graceful shutdown are not implemented yet.
