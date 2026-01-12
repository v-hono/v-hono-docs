# hono.docs

API documentation tools (OpenAPI, Swagger) for v-hono-core framework.

## Features

- OpenAPI 3.0/3.1 specification support
- Swagger UI integration
- Interactive API documentation
- Fluent API for building specs

## Installation

```bash
v install hono
v install hono.docs
```

## Usage

```v
import hono
import hono.docs

fn main() {
    mut app := hono.Hono.new()

    // Build OpenAPI specification
    spec := docs.OpenAPIBuilder.new()
        .openapi('3.0.0')
        .title('My API')
        .version('1.0.0')
        .path('/users')
            .get(docs.OpenAPIOperation{
                summary: 'List users'
                responses: {
                    '200': docs.OpenAPIResponse{
                        description: 'Success'
                    }
                }
            })
            .done()
        .build()!

    // Register OpenAPI endpoint
    app.doc('/doc', spec)

    // Serve Swagger UI
    app.get('/ui', docs.swagger_ui(docs.SwaggerUIOptions{
        url: '/doc'
        title: 'API Documentation'
    }))

    app.listen(':3000')
}
```

## Dependencies

- `hono` - Core framework

## License

MIT
