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

## benchmark
````bash
$ go test -bench .
BenchmarkWorkerPool-8                  1        8170956922 ns/op
BenchmarkNopool-8                      1        8400776011 ns/op
BenchmarkGopool-8                      1        8129090755 ns/op
````
