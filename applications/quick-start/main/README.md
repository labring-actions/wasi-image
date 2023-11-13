## using wasm runtime 

1. install wasmedge

```bash
sealos run docker.io/labring/containerd-shim-wasmtime:v0.3.0
```

2. build wasi image

```
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
  runtimeClassName: wasmedge #修改成对应的runtime名字
  containers:
  - name: wasm-container
    image: sealos.hub:5000/quick-start:latest
```
