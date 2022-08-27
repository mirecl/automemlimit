# automemlimit

[![Go Reference](https://pkg.go.dev/badge/github.com/KimMachineGun/automemlimit.svg)](https://pkg.go.dev/github.com/KimMachineGun/automemlimit)

Automatically set `GOMEMLIMIT` to match Linux [cgroups(7)](https://man7.org/linux/man-pages/man7/cgroups.7.html) memory limit.

See more details about `GOMEMLIMIT` [here](https://tip.golang.org/doc/gc-guide#Memory_limit).

## Installation

```shell
go get -u github.com/KimMachineGun/automemlimit
```

## Usage

```go
package main

// By default, it sets `GOMEMLIMIT` to 90% of cgroup's memory limit.
// You can find more details of its behavior from the doc comment of memlimit.SetGoMemLimitWithEnv.
import _ "github.com/KimMachineGun/automemlimit"
```

or

```go
package main

import "github.com/KimMachineGun/automemlimit/memlimit"

func init() {
	memlimit.SetGoMemLimitWithEnv()
	memlimit.SetGoMemLimit(0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.Limit(1024*1024), 0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.FromCgroup, 0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.FromCgroupV1, 0.9)
	memlimit.SetGoMemLimitWithProvider(memlimit.FromCgroupV2, 0.9)
}
```