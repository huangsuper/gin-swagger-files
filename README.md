# gin-swagger-files

[![Go](https://github.com/huangsuper/gin-swagger-files/actions/workflows/go.yml/badge.svg)](https://github.com/huangsuper/gin-swagger-files/actions/workflows/go.yml) [![Go Report Card](https://goreportcard.com/badge/github.com/huangsuper/gin-swagger-files)](https://goreportcard.com/report/github.com/huangsuper/gin-swagger-files)

Alternative to [github.com/swaggo/files](https://github.com/swaggo/files) that provides support for `//go:embed`, and multiple swagger UI versions.

## Example usage

This package is a drop-in replacement for [github.com/swaggo/files](https://github.com/swaggo/files) and will work with
Go1.16+ projects. To use it, replace the `github.com/swaggo/files` with `github.com/huangsuper/gin-swagger-files` like this:

```go
package main

import (
    "github.com/gin-gonic/gin"
    swaggerFiles "github.com/huangsuper/gin-swagger-files"
    ginSwagger "github.com/swaggo/gin-swagger"

    _ "github.com/swaggo/gin-swagger/example/basic/docs" // docs is generated by Swag CLI, you have to import it.
)

// @title Swagger Example API
// @version 1.0
// @description This is a sample server Petstore server.
// @termsOfService http://swagger.io/terms/

// @contact.name API Support
// @contact.url http://www.swagger.io/support
// @contact.email support@swagger.io

// @license.name Apache 2.0
// @license.url http://www.apache.org/licenses/LICENSE-2.0.html

// @host petstore.swagger.io
// @BasePath /v2
func main() {
    r := gin.New()

    url := ginSwagger.URL("http://localhost:8080/swagger/doc.json") // The url pointing to API definition
    r.GET("/swagger/*any", ginSwagger.WrapHandler(swaggerFiles.Handler, url))

    r.Run()
}
```

## Updating the version

To update the Swagger UI version, copy the contents of the
[swagger-api/swagger-ui](https://github.com/swagger-api/swagger-ui)
[dist folder](https://github.com/swagger-api/swagger-ui/tree/master/dist) into the dist folder here. This will
automatically be bundled into the library at build time.

The version should be tagged appropriately like `3.51.1`.
