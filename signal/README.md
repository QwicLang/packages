# 📡 Signal

`signal` is a robust, high-performance web framework for the Qwic language. It combines the simplicity of Flask with the type safety and robustness of FastAPI.

## 🚀 Quick Start

```qwic
import signal

func getUser(req) {
    const id = req.params.id
    return signal.Response.new(200, { 
        userId: id, 
        name: "Qwic User " + id.to_string() 
    })
}

func createItem(req) {
    const data = req.body.validate({ 
        title: "string", 
        priority: "int" 
    })
    return signal.Response.new(201, { status: "created", item: data })
}

public func main() {
    const app = signal.App.new()

    app.routes([
        { path: "/user/{id:int}", method: "GET", handler: getUser },
        { path: "/item",          method: "POST", handler: createItem },
    ])

    app.run(port: 8080)
}
```

## ✨ Features

- **Function-Based Routing**: Clean separation of route configuration and business logic.
- **Type-Safe Parameters**: Automatic casting of path parameters (e.g., `{id:int}`).
- **Robust Validation**: Built-in request body validation to ensure data integrity.
- **High Performance**: Asynchronous core designed for micro-services and APIs.

## 🛠️ Installation

(Installation instructions will be added once the build system is finalized)
