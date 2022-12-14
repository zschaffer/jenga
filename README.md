<img align="right" width="250px" src="https://github.com/zschaffer/jenga/blob/a8cbfd372c352d78b7ac91d7b6e439d379d995cb/jenga.png">

# Jenga

[![Go Reference](https://pkg.go.dev/badge/github.com/zschaffer/jenga.svg)](https://pkg.go.dev/github.com/zschaffer/jenga)
![build](https://github.com/zschaffer/jenga/actions/workflows/go.yml/badge.svg)
[![Go Report Card](https://goreportcard.com/badge/github.com/zschaffer/jenga)](https://goreportcard.com/report/github.com/zschaffer/jenga)

A tool for building static single page blogs in [Go](https://golang.org/).

## Details

Jenga is a no frills, fast-enough static site builder written in [Go](https://golang.org/). It is optimized for single-page infinite scrolling blogs.
Jenga takes a source directory of markdown files and an HTML template and spits outs a full HTML blog.

### Supported Platforms

In the releases tab you will find pre-built binaries for Linux, Windows and macOS (Intel and Apple Silicon). Otherwise, Jenga can compile and run anywhere Go can!

## Build and Install from Source

### Prerequisities

- [Git](https://git-scm.com/)
- [Go](https://golang.org/)

Clone the source from GitHub and install:

```bash
git clone https://github.com/zschaffer/jenga.git
cd jenga
go install
```

## Usage

Jenga has some basic setting up in order to get going; sort of like the real game!

### Set up your own `jenga.tmpl` or copy it from the releases tab

Jenga uses Go's [`html/template`](https://pkg.go.dev/html/template) library for template construction. Read their [doc's](https://pkg.go.dev/html/template) for more information on how to manipulate your data. The basic thing required in your `jenga.tmpl` is a `{{.}}` block to render the data converted from your `.md` files.

The included `jenga.tmpl` file looks something like this:

```tmpl
<body>
  <!-- Wrap everything in a div -->
  <div>
    <!-- Map over all your input .md files -->
    {{range .}}

    <!-- Wrap each input file in a div tag -->
    <div>{{.}}</div>

    <!-- End the map -->
    {{end}}
  </div>
</body>
```

### Set up your config `jenga.toml` file or copy it from the releases tab

Jenga uses [TOML]() as a configuration language (for now). [TOML]() is structured with `keys` and `values` like `mykey = myvalue`.

Jenga has three keys it looks for in order to run:

```toml
 InputFileDir = "/path/to/your/markdown/files"
 OutputDir = "/path/to/your/output/folder"
 TemplatePath = "/path/to/your/template.html"
```

> Note: TOML is case-sensitive so make sure you get those keys right!

### Run Jenga

Jenga only takes one flag, `-config`, that indicates to Jenga where your `jenga.toml` file is.

```bash
jenga    #If you don't pass any flags - default is "./jenga.toml"

# OR

jenga -config="$HOME/.config/jenga.toml"
```

Running Jenga will read through your source files, convert them to markdown, punch them into your template, and output them your your output directory - once you see the `build is finished!` you're good to go!

From here you can use Cloudflare Page's or GitHub Pages to host your new site. Just point them at your new build folder and bam!

## Dependencies

Jenga takes advantage of Go's super handy standard library for most things.

Other than that, Jenga currently relies on:

- [Burnt Sushi's toml](https://github.com/BurntSushi/toml.git)
- [gomarkdown's markdown](https://github.com/gomarkdown/markdown.git)

Shoutout to them because otherwise this would've been a lot trickier.

## Credits

Jenga Logo by [Xinrui Chen](https://github.com/xynree)

Original Go gopher eyes were. designed by [Renee French](https://reneefrench.blogspot.com/)
