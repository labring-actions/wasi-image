## using wasm runtime 

1. install wasmedge

```bash
sealos run docker.io/labring/runwasi-wasmedge:wasi_nn-ggml
```

2. create pod
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-with-wasm-workload
spec:
  runtimeClassName: wasmedge
  containers:
  - name: wasm-container
    image: sealos.hub:5000/quick-start:latest
```
