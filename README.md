[![Go Package](https://img.shields.io/badge/Go%20Package-Reference-green?style=flat&logo=Go&link=https://pkg.go.dev/github.com/jpengineer/logger)](https://pkg.go.dev/github.com/jpengineer/logger)

# logger v1.6.1
**Go Logger module**

This logger is a simple module to write a log file, and it allows multiple instances, 
concurrency write, rotation by file size (MB), backup files and log level (debug, informative, warning, error and critical)

You can load module with:
```go
go get "github.com/jpengineer/logger"
```

The default implementation way is: 

```go
package main

import (
	"github.com/jpengineer/logger"
)

func main() {
	logName := "MyLogName.log"
	path := "/my/log/path"
	level := logger.Level.DEBUG

	_log, _ := logger.Start(logName, path, level)
	_log.TimestampFormat(logger.TS.Special)

	_log.Critical("This is a Critical message")
	_log.Info("This is a Informational message %d", 12345)
	_log.Warn("This is a Warning message")
	_log.Error("This is a Error message")
	_log.Debug("This is a Debug message")
	_log.Close()
}
```

If you don't specify the rotation settings, by default it will be set to 40 MB maximum size per file
and 4 backup files. To change default rotation you should be considerate the next:

```go
    maxSizeMB := 80
    maxBackup := 5
    
    _log.Rotation(maxSizeMB, maxBackup)
```

The output format is:
```log
Logger Version: 1.6.0 SourceFile: main.go Hash: XDNRdfeWUJa4BJ4gaiDWTIQJxxgW1NhxfXaK0qDnKBU=
Aug 3, 2020 12:41:25.946521 -04 [CRITICAL] This is a Critical message
Aug 3, 2020 12:41:25.946526 -04 [INFO] This is an Informational message 12345
Aug 3, 2020 12:41:25.946557 -04 [WARN] This is a Warning message
Aug 3, 2020 12:41:25.946562 -04 [ERROR] This is an Error message
Aug 3, 2020 12:41:25.946575 -04 [DEBUG] This is a Debug message
```
