---
title: "Functional Options Pattern In Go"
date: 2024-03-21
draft: false
---

# Functional Options Pattern In Go
I became increasingly frustrated with how I deal with optional configurations in my Go apps. Imagine that we are making a server constructor, `NewServer,` and want to allow clients to provide optional configuration values or otherwise use defaults. Usually, I pass a configuration struct on autopilot without too much thinking and looks something like this

```go
type Config struct {
	Port int
}

func NewServer(addr string, cfg Config) { ... }
```

This approach is flexible enough to support new configuration attributes being added but suffers from several issues

* There is no easy way to perform validation of the attributes and return an error to the client if needed.
* There is no way to enforce default behaviour. Default values will be used if not provided when initialising the Config struct.
* Distinguishing between a value purposefully set to the default value and the value missing becomes complicated. Using pointers to denote `nil` is not handy for the clients and forces them to pass an empty configuration instead.
```go
func NewServer(addr string, Config{}) { ... }
```
---
The first solution that comes to mind is [Bulder pattern](https://refactoring.guru/design-patterns/builder). I've extensively used it when programming in Java; it is a clean and flexible pattern I find very useful. Builder in Golang might look something like this

```go
type Config struct {
	Port int
}

type ConfigBuilder struct {
	port *int
}

func (b *ConfigBuilder) SetPort(port int) *ConfigBuilder {
	b.port = &port
	return b
}

func (b *ConfigBuilder) Build() (Config, error) {
	cfg := Config{}

	if b.port == nil {
		cfg.Port = 8080 // default port
	} else if *b.port <= 0 {
		return Config{}, errors.New("port can't be <= 0")
	} else {
		cfg.Port = *b.port
	}
	return cfg, nil
}
```
This much cleaner approach allows clients to chain calls, leaving defaults as they are. However, it still has an issue - error management becomes more challenging as we cannot return errors in builder setters and have to defer them to the `build()` stage. It's clunky and adds extra complexity.

---

This is where the Functional Options Pattern comes to the rescue. It utilises Golangs [variadic functions](https://gobyexample.com/variadic-functions), variable capturing, and higher-order functions. In short

* Internal `options` struct denotes the config template
* A functional type `Option` which, when applied, mutates `options`
* An associated `Option` generator function. For example, we will have a function called `func WithPort(port int) Option {}` that returns an `Option` to modify the port with the provided value
* Function that iterates over the `Option` arguments and applies them one by one to generate a final set of config options
* Apply options to an internal `options`

Code is better than a hundred words

```go
// options is a configuration struct
type options struct {
	port *int
}

// Option represents a functional option for configuring the server.
type Option func(options *options) error

// WithPort is a functional option to set the port for the server.
func WithPort(port int) Option {
	return func(options *options) error {
		if port <= 0 {
			return errors.New("port can't be less than 0")
		}
		options.port = &port
		return nil
	}
}

// NewServer creates a new server with the given options.
func NewServer(addr string, optFuncs ...Option) (*http.Server, error) {
	var opts options
	for _, optFunc := range optFuncs {
		err := optFunc(&opts)
		if err != nil {
			return nil, err
		}
	}

	var port int
	if opts.port == nil {
		port = 8080
	} else if *opts.port <= 0 {
		return nil, errors.New("port can't be <= 0")
	} else {
		port = *opts.port
	}
	// ...
}
```

Client will call this function like so

```go
server, err := mylib.NewServer("localhost", mylib.WithPort(1111), mylib.WithTimeout(10*time.Second))

// or if wants default args
server, err := mylib.NewServer("localhost")
```

This pattern covers all of the pain-points mentioned before
* Clean and easy-to-understand API
* Clear default behaviour
* Simple error handling during config initialisation