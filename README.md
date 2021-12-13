# go fmt in the browser via WebAssembly

**DEMO: [go-fmt-wasm.netlify.app](https://go-fmt-wasm.netlify.app)**

This example uses the `go/format` package instead of compiling the `go fmt` command line tool because we don't have access to a file-system replacement out of the box in the browser which `go fmt` would need.

## Creating the wasm file
- Compile the Go code with `GOOS=js GOARCH=wasm go build -o format-go-code.wasm`
- To execute the wasm file from JS you also need some glue code. This code can also be found in your local go installation under `{path to your go installation}/misc/wasm/wasm_exec.js`. This script needs to be imported as a script in your index.html. (On Linux, the Go directory is usually `/usr/local/go`.)

## Using the wasm file
- The glue code needs to be imported via `<script src="wasm_exec.js"></script>`.
- The WASM file needs to be loaded, see index.html.
- Afterwards, the "exported" function (`formatGoCode`) is available in JavaScript.

## Error handling
- If the formatting did not succeed, an empty string is returned. In that case, the result should not be used to replace the non-formatted code the user wrote.

## Sources
- https://golangbot.com/webassembly-using-go/
