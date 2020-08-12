# wallarm-go

[![build](https://github.com/416e64726579/wallarm-go/workflows/Go/badge.svg)](https://github.com/416e64726579/wallarm-go/actions?query=workflow%3AGo)
[![GoDoc](https://img.shields.io/badge/godoc-reference-5673AF.svg?style=flat-square)](https://godoc.org/github.com/416e64726579/wallarm-go)
[![Go Report Card](https://goreportcard.com/badge/github.com/416e64726579/wallarm-go?style=flat-square)](https://goreportcard.com/report/github.com/416e64726579/wallarm-go)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://github.com/416e64726579/wallarm-go/blob/master/LICENSE)

## Table of Contents
- [Install](#install)
- [Getting Started](#getting-started)
- [License](#license)

> **Note**: This library is in active development and highly suggested to use carefully.

A Go library for interacting with
[Wallarm API](https://apiconsole.eu1.wallarm.com). This library allows you to:

* Manage applications
* Manage nodes
* Manage integrations
* Manage triggers
* Manage users
* Manage the blacklist
* Change the global WAF mode
* List vulnerabilities

## Install

You need a working Go environment

```sh
go get github.com/416e64726579/wallarm-go
```

## Getting Started

```go
package main

import (
	"fmt"
	"log"
	"os"

	wallarm "github.com/416e64726579/wallarm-go"
)

func main() {
	// Construct a new API object
	api, err := wallarm.New(os.Getenv("WALLARM_API_UUID"), os.Getenv("WALLARM_API_SECRET"))
	if err != nil {
		log.Fatal(err)
	}

	// Fetch user details
	u, err := api.UserDetails()
	if err != nil {
		log.Fatal(err)
	}
	// Print user specific data
	fmt.Println(u)

	// Change global WAF mode to monitoring
	mode := ClientUpdate{
		Filter: &ClientFilter{
			ID: 1,
		},
		Fields: &ClientFields{
			Mode: "monitoring",
		},
	}
	c, err := api.ClientUpdate(&mode)
	if err != nil {
		log.Fatal(err)
	}
	// Print client data
	fmt.Println(c)
}
```

The reference to the godoc API description of the package
[API documentation](https://godoc.org/github.com/416e64726579/wallarm-go)

# License

[MIT](LICENSE) licensed
