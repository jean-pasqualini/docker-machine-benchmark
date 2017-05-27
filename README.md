Benchmark
---------

#### Docker for mac
1. Start docker for mac

2. Open the terminal

3. Launch benchmark 
```
docker run --rm -v $PWD:/data -it ubuntu:latest dd if=/dev/zero of=/data/test.data bs=1M count=1024 conv=fdatasync
```

4. Results
```
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 3.8278 s, 281 MB/s
```

#### Docker machine (avec virtualbox share)
0. Open the terminal 

1. Create the machine
```
docker-machine create terminator --virtualbox-cpu-count=2 --virtualbox-memory=2048 --driver=virtualbox
```

2. Connect docker client to machine
```
eval $(docker-machine env terminator)
```

3. Launch benchark
```
docker run --rm -v $PWD:/data -it ubuntu:latest dd if=/dev/zero of=/data/test.data bs=1M count=1024 conv=fdatasync
```

4. Results
```
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 4.44023 s, 242 MB/s
```

#### Docker machine (sans virtualbox share)
0. Open the terminal 

1. Create the machine
```
docker-machine create terminator --virtualbox-cpu-count=2 --virtualbox-memory=2048 --virtualbox-no-share --driver=virtualbox
```

2. Connect docker client to machine
```
eval $(docker-machine env terminator)
```

3. Launch benchark
```
docker run --rm -v $PWD:/data -it ubuntu:latest dd if=/dev/zero of=/data/test.data bs=1M count=1024 conv=fdatasync
```

4. Results
```
1024+0 records in
1024+0 records out
1073741824 bytes (1.1 GB, 1.0 GiB) copied, 0.260314 s, 4.1 GB/s
```



#### Astuce

Volume is speed when share from vm to host<br>
Volume is slow when share from host to vm<br>
<br>
Use sshfs for access from host to volumes stored in vm<br>
docker run -v /host/share:/home/terminator/share -p 2222:22 -d atmoz/sftp 'terminator:terminator:1000'
