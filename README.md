# workerpool
## install
````go
go get github.com/ejunjsh/workerpool
````

## usage
````go
import "github.com/ejunjsh/workerpool"

func main(){
    wg := new(sync.WaitGroup)
    //十个goroutine，队列容量100
	wp:=workerpool.NewWorkerPool(10,100)
	wp.Start()
    //提交1000000任务
	for i := 0; i < 1000000; i++ {
		wg.Add(1)
		wp.Execute(func() {
			for j := 0; j < 100000; j++ {
			}
			wg.Done()
		})
	}
	wg.Wait()
	wp.Stop()
}

````

## test
````bash
go test -bench .
BenchmarkNopool-8                      1        7966900091 ns/op
BenchmarkGopool-8                      1        7949844269 ns/op
BenchmarkWorkerPool-8                  1        7997732135 ns/op
````
