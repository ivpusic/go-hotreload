go-hotreload
============

Recompiling and rerunning go apps when source changes

## Features
- specify list of files/directories to watch
- specify list of files/directories to ignore
- provide command which will be run on start/restart
- configuration using cli-flags and/or json file

### How to install?
```shell
go get github.com/ivpusic/go-hotreload/hr
```

## Usage
```
hr --help
usage: hr [<flags>]

Flags:
  --help               Show help.
  -v, --verbose        Verbose mode. Default: false
  -c, --cmd=CMD        Command to execute on each reload. Default: 'go run main.go'
  -w, --watch=WATCH    Comma separated list of directories to watch. Default: ['.']
  -i, --ignore=IGNORE  Comma separated list of directories to ignore. Default: []
  -p, --port=PORT      Port on which app is running. Default: 3000
  --conf=CONF          Path to json config. Default: ''
  --version            Show application version.

To run with default settings just run
```
hr
```

### Examples
Let we say you have your app running on port 3000, you want to run your program with `go run main.go`, you want to listen `.go` files under `/some/path` and `/some/other/path` directories, and you want to ignore files on `/some/ignored/path` directory.

You can provide configuration using command line flags, using ``json`` config, or combined, where command line args has bigger priority.

#### - using cli flags
```
hr --port 3000 --cmd "go run main.go" --watch /some/path,/some/other/path --ignore /some/ignored/path
```

Note that you can also use short version of cli flags. So we could write commans as:
```
hr --port 3000 -c "go run main.go" -w /some/path,/some/other/path -i /some/ignored/path
```

You have troubles? Use verbose mode! You will see a lot of usefull information about go-hotreload internals.
```
hr -v --port 3000 -c "go run main.go" -w /some/path,/some/other/path -i /some/ignored/path
```

#### - using json config
Create json file with content, with name for example conf.json
```
{
	"port": 3000,
	"cmd": "go run main.go",
	"watch": ["/some/path", "/some/other/path"],
	"ignore": ["/some/ignored/path"]
}
```
and then
```
hr --conf conf.json
```

#### - combined
If the same option is provided by cli flag and json config, one from cli will survive.

Example of json config:
```
{
	"cmd": "go run main.go",
	"watch": ["/some/path", "/some/other/path"],
	"ignore": ["/some/ignored/path"]
}
```
and then
```
hr --conf conf.json --port 3000
```

# TODO
- **tests**

# License
MIT
