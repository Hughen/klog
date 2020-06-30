klog
====

klog is forked from https://github.com/kubernetes/klog. To support the printing of logs with context, for example:

```go
import (
    "klog"
    "context"
    "fmt"
)

type TraceMessage struct {
    ID uint64
}

// TraceMessage must be implementing `Stringer.String` interface
func (t TraceMessage) String() string {
    return fmt.Sprintf("TraceID=%d", t.ID)
}

traceMsg := TraceMessage{ID: 1593498797405}
ctx := context.WithValue(context.Background(), klog.ContextKey, traceMsg)

// log with specified context
klog.Context(ctx).Info("hello, the logger with my context")
// I0630 14:33:17.405003       1 main.go:20] TraceID=1593498797405 hello, the logger with my context
```
