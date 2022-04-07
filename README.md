<img src="https://user-images.githubusercontent.com/1423657/161867564-4b3fc400-95e5-424c-9210-604d5671a85e.png" width=100 />

# FluxPipe
Experimental [flux](https://github.com/influxdata/flux) API pipeline for embedded datasources

### Instructions
Download a [binary release](https://github.com/lmangani/fluxpipe/releases/) or build from source


#### 📦 Download Binary
```bash
curl -fsSL github.com/lmangani/fluxpipe/releases/latest/download/fluxpipe -O && chmod +x fluxpipe
```

#### 📖 Build CMD
```bash
go build -o fluxpipe -ldflags="-s -w" fluxpipe.go
```

#### 📖 Build Server
```bash
go build -o fluxpipe-server -ldflags="-s -w" fluxpipe-server.go
```

### 🐛 Examples
#### HTTP API
##### Generate CSV
```bash
./fluxpipe-server -port 8086

curl -XPOST localhost:8086/api/v2/query -sS \
  -H 'Accept:application/csv' \
  -H 'Content-type:application/vnd.flux' \
  -d 'import g "generate" g.from(start: 2022-04-01T00:00:00Z, stop: 2022-04-01T00:03:00Z, count: 3, fn: (n) => n)'
```
```flux
#datatype,string,long,dateTime:RFC3339,long
#group,false,false,false,false
#default,_result,,,
,result,table,_time,_value
,,0,2022-04-01T00:00:00Z,1
,,0,2022-04-01T00:00:36Z,2
,,0,2022-04-01T00:01:12Z,3
```

##### Grafana Flux
```
import g "generate" 
g.from(start:  v.timeRangeStart, stop: v.timeRangeStop, count: 10, fn: (n) => n )
```
![image](https://user-images.githubusercontent.com/1423657/162274743-b454d3e6-e678-43aa-8ad6-8d612f2857b5.png)



#### STDIN CMD
##### Generate CSV
```bash
echo 'import g "generate" g.from(start: 2022-04-01T00:00:00Z, stop: 2022-04-01T00:03:00Z, count: 5, fn: (n) => 1)' \
| ./fluxpipe -stdin
```
```csv
#datatype,string,long,dateTime:RFC3339,long
#group,false,false,false,false
#default,_result,,,
,result,table,_time,_value
,,0,2022-04-01T00:00:00Z,1
,,0,2022-04-01T00:00:36Z,1
,,0,2022-04-01T00:01:12Z,1
,,0,2022-04-01T00:01:48Z,1
,,0,2022-04-01T00:02:24Z,1
```
##### Parse CSV
```bash
cat scripts/csv.flux | ./fluxpipe -stdin
```
##### Query SQL
```bash
cat scripts/sql.flux | ./fluxpipe -stdin
```



## Status
- [x] stdin pipeline
- [x] http api
  - [x] plaintext
  - [x] json support
  - [ ] api doc
- [ ] output templates
- [ ] shared secrets
- [ ] bucket emulation


#### Acknowledgements
Project is not affiliated or endorsed by Influxdata or Grafana Labs. All rights belong to their respective owners.
