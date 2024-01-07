Fork of https://github.com/webview/webview_go.

## new features

1. You can check whether `webview.New()` returns a successful webview:
```go
func isWebviewSuccessful(w webview.WebView) bool {
	log.Printf("%T", w)

	w2 := reflect.ValueOf(w).Elem()
	ww := w2.FieldByName("w")
	return ww.UnsafePointer() != nil
}
```

2. You can change code to set initial windows size before create, to solve window blink problem.
`webview.h:2217`
```c++
      constexpr const int initial_width = 900;
      constexpr const int initial_height = 650;
      set_size(initial_width, initial_height, WEBVIEW_HINT_NONE);
```

# webview_go

[![GoDoc](https://godoc.org/github.com/webview/webview_go?status.svg)](https://godoc.org/github.com/webview/webview_go)
[![Go Report Card](https://goreportcard.com/badge/github.com/webview/webview_go)](https://goreportcard.com/report/github.com/webview/webview_go)

Go language binding for the [webview library][webview].

> [!NOTE]
> Versions <= 0.1.1 are available in the [old repository][webview].

### Getting Started

See [Go package documentation][go-docs] for the Go API documentation, or simply read the source code.

Start with creating a new directory structure for your project.

```sh
mkdir my-project && cd my-project
```

Create a new Go module.

```sh
go mod init example.com/app
```

Save one of the example programs into your project directory.

```sh
curl -sSLo main.go "https://raw.githubusercontent.com/webview/webview_go/master/examples/basic/main.go"
```

Install dependencies.

```sh
go get github.com/webview/webview_go
```

Build the example. On Windows, add `-ldflags="-H windowsgui"` to the command line.

```sh
go build
```

### Notes

Calling `Eval()` or `Dispatch()` before `Run()` does not work because the webview instance has only been configured and not yet started.

[go-docs]: https://pkg.go.dev/github.com/webview/webview_go
[webview]: https://github.com/webview/webview
