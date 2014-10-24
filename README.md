godirsync
=========

A tool to replicate a directory containing bunch of sub directories and files to another machine over http.

build:
```
$ go get ./...
$ go build
```


flags:

```
$ go run main.go
Must be a server or a client. Use -server or -from.
Usage of /tmp/go-build324068723/command-line-arguments/_obj/exe/main:
  -alsologtostderr=false: log to standard error as well as files
  -from="": run as client pulling data from server at URI
  -log_backtrace_at=:0: when logging hits line file:N, emit a stack trace
  -log_dir="": If non-empty, write log files in this directory
  -logtostderr=false: log to standard error instead of files
  -server="": run as server listening at ip:port
  -stderrthreshold=0: logs at or above this threshold go to stderr
  -v=0: log level for V logs
  -vmodule=: comma-separated list of pattern=N settings for file-filtered logging
exit status 1
```


example:
```
$ godirsync -server localhost:9999
```

This will serve files located in "." where the program runs

on the client machine:
```
$ godirsync -from http://somemachine:9999 
```

Each time you run godirsync on client machine it will get files that have been added or changed since the last time godirsync ran. All files will be fetched from the server via http.  Godirsync running in client mode will ask the server, over http, for a list of files that have been added or changed. Then it will do GET for each machine and write to "." where the client is running.
