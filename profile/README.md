go-i2p
======

Tunnels for gophers!

I2P applications, libraries, and tools written in Go.

### Go I2P library users: module path changes!

The module path for the Go SAMv3 libraries is changing from the personal namespace(`eyedeekay`) to the `go-i2p` namespace.
This will affect you when you update your SAMv3 or I2PControl library versions.
To upgrade:

```sh
#1: first, delete the old module paths from your go.mod
grep -v 'eyedeekay' go.mod > go.mod.new && mv go.mod.new go.mod
#2: then regenerate your go.mod file
go mod tidy
```

The new module paths are listed below:

## Official source of I2P SAMv3 application development libraries:

* [onramp high-level development library(stable)](https://github.com/go-i2p/onramp) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/onramp)](https://goreportcard.com/report/github.com/go-i2p/onramp)
  - High-level framework for I2P-native web services
  `import "github.com/go-i2p/onramp"`

* [go-sam-go client development library(unstable)](https://github.com/go-i2p/go-sam-go) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/go-sam-go)](https://goreportcard.com/report/github.com/go-i2p/go-sam-go)
  - Modular, clean SAMv3 protocol client implementation. Work-in-progress, seeking contributors, reviewers, and testers.
  `import "github.com/go-i2p/go-sam-go"`

* [gosam client development library(stable)](https://github.com/go-i2p/gosam) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/gosam)](https://goreportcard.com/report/github.com/go-i2p/gosam)
  - High-level SAM protocol implementation. Maintenance mode, future PR's should go to go-sam-go.
  `import "github.com/go-i2p/gosam"`

* [sam3 client development library(stable)](https://github.com/go-i2p/sam3) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/sam3)](https://goreportcard.com/report/github.com/go-i2p/sam3)
  - Modern, flexible SAMv3 protocol client implementation. Maintenance mode, future PR's should go to go-sam-go.
  `import "github.com/go-i2p/sam3"`

* [i2pkeys key handling library(stable)](https://github.com/go-i2p/i2pkeys) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/i2pkeys)](https://goreportcard.com/report/github.com/go-i2p/i2pkeys)
  - I2P destination and key management
  `import "github.com/go-i2p/i2pkeys"`

## Official source of I2PControl development libraries:

* [go-i2pcontrol I2P Control client(stable)](https://github.com/go-i2p/go-i2pcontrol) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/go-i2pcontrol)](https://goreportcard.com/report/github.com/go-i2p/go-i2pcontrol)
  - Router management and configuration API
  `import "github.com/go-i2p/go-i2pcontrol"`

## Official source of I2P Bittorrent development libraries:

* [go-i2p-bt I2P Bittorrent library(stable)](https://github.com/go-i2p/go-i2p-bt) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/go-i2p-bt)](https://goreportcard.com/report/github.com/go-i2p/go-i2p-bt)
  - Anonymous BitTorrent protocol implementation
  `import "github.com/go-i2p/go-i2p-bt"`

## Official source of I2P Tunnel development libraries:

* [go-i2ptunnel I2P Tunnel library(unstable)](https://github.com/go-i2p/go-i2ptunnel) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/go-i2ptunnel)](https://goreportcard.com/report/github.com/go-i2p/go-i2ptunnel)
  - Anonymous Proxy/Reverse Proxy tunnel implementation. Work-in-progress, seeking contributors, reviewers, and testers.
  `import "github.com/go-i2p/go-i2ptunnel"`

## Official source of I2P SMTP development libraries:

* [go-i2p-smtp I2P Mail library(unstable)](https://github.com/go-i2p/go-i2p-smtp) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/go-i2p-smtp)](https://goreportcard.com/report/github.com/go-i2p/go-i2p-smtp)
  - Anonymous email implementation. Work-in-progress, seeking contributors, reviewers, and testers.
  `import "github.com/go-i2p/go-i2p-smtp"`

### Official source of I2P router development libraries:

go-i2p is under active development. [go-i2p ROADMAP.md](https://github.com/go-i2p/go-i2p/blob/master/ROADMAP.md)

* [go-i2p I2P router implementation(incomplete but usable by experts)](https://github.com/go-i2p/go-i2p) [![Go Report Card](https://goreportcard.com/badge/github.com/go-i2p/go-i2p)](https://goreportcard.com/report/github.com/go-i2p/go-i2p)
  - Native Go I2P router implementation
  `import "github.com/go-i2p/go-i2p"`

[Go Report Card]: https://goreportcard.com/badge/go-i2p
