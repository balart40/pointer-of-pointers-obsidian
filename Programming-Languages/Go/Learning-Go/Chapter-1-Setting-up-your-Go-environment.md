---
tags:
  - Go
  - Programming-Language
  - Golang
---
## Installing the Go tools

The latest version of tools can be found at the Go website:

[https://go.dev/dl/](https://go.dev/dl/)

For Mac users, this can be done using Homebrew: [https://formulae.brew.sh/formula/go](https://formulae.brew.sh/formula/go)

```
brew install go
```

If install was successful you should be able to to run `go version` as shown below

```
$ go version

go version go1.21.4 darwin/amd64
```
### The go command

You can access many of the Go development tools via the `Go` command such as:
- Compiler
- Code formatter
- Linter
- dependency manager
- test runner
- and more

There's an enhanced version of `go fmt` available called `go imports` that also cleans up your imports statements. It puts them in alphabetical order, removes unused imports, and attempts to guess any unspecified imports.

```
go install golang.org/x/tools/cmd/goimports@latest
```

You can run it as shown below

```
goimports -l -w
```

### The semicolon insertion rule

If the last token before a newline is any of the following, the lexer inserts a semicolon after the token
- An identifier (which includes words like int and float64)
- A basic literal such as a number or string constant
- One of the tokens: "break", "continue", "fallthrough", "return", "++", "--", ")" or "}"

Therefore 

```
func main()
{
    fmt.Println("Hello, world!")
}
```

Turns into

```
func main();
{
    fmt.Println("Hello, world!")
};
```

Which is not valid Go.

### Linting and Vetting

Install `golint` with the following command

```
go install golang.org/x/lint/golint@latest
```
