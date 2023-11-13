## using wasm runtime 

1. install wasmedge

```bash
sealos run docker.io/labring/containerd-shim-wasmtime:v0.3.0
```

2. build wasi image

使用rust 写一个wasm的程序
```rust
use std::thread::sleep;

fn main() {
    loop {
        sleep(std::time::Duration::from_secs(5));
        println!("{}", "This is from a main function from a wasm module");
    }
}
```

这里我已经编译好了wasm文件 [quick-start.wasm](./quick-start.wasm)

构建wasi镜像
```bash
sealos build --platform "wasi/wasm" -t sealos.hub:5000/quick-start:latest .
sealos push sealos.hub:5000/quick-start:latest
```

3. create pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-with-wasm-workload
spec:
  runtimeClassName: runwasi-wasmtime #修改成对应的runtime名字
  containers:
  - name: wasm-container
    image: sealos.hub:5000/quick-start:latest
```

