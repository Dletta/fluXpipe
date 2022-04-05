<img src="https://user-images.githubusercontent.com/1423657/161867564-4b3fc400-95e5-424c-9210-604d5671a85e.png" width=100 />

# FluxPipe
Experimental [flux](https://github.com/influxdata/flux) pipeline for embedded or external datasources

### Instructions
Download a [binary release](https://github.com/lmangani/fluxpipe/releases/) or build from source


#### 📦 Download Binary
```
curl -fsSL github.com/lmangani/fluxpipe/releases/latest/download/fluxpipe -O && chmod +x fluxpipe
```

### 📖 Build
``` 
go build -o fluxpipe -ldflags="-s -w" fluxpipe.go
```

### 🐛 Test
```
cat script.flux | fluxpipe
```
