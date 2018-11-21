# alpine stress container
A [stress](https://people.seas.harvard.edu/~apw/stress/) workload app on alpine linux.

It is not a benchmark. It is a tool used by system administrators to evaluate how well their systems will scale, 
by kernel programmers to evaluate perceived performance characteristics, and by systems programmers 
to expose the classes of bugs which only or more frequently manifest themselves when the system is under heavy load.


# with interactive shell in container
```
docker run -it --rm stress /bin/ash
```
### ram stress test
2GB with two workers
```
stress --vm 2 --vm-bytes 2G --timeout 10s
```
90% ram load test with one worker
```
stress --vm 1 --vm-bytes $(awk '/MemAvailable/{printf "%d\n", $2 * 0.9;}' < /proc/meminfo)k --timeout 20
```

### cpu stress test
```
stress --cpu 2 --timeout 10s
```


# you can start stress test directly with docker run command
docker run --rm -it stress --cpu 2 --io 1 --vm 2 --vm-bytes 128M --timeout 10s

# options
```
 -?, --help         show this help statement  
     --version      show version statement  
 -v, --verbose      be verbose  
 -q, --quiet        be quiet  
 -n, --dry-run      show what would have been done  
 -t, --timeout N    timeout after N seconds  
     --backoff N    wait factor of N microseconds before work starts  
 -c, --cpu N        spawn N workers spinning on sqrt()  
 -i, --io N         spawn N workers spinning on sync()  
 -m, --vm N         spawn N workers spinning on malloc()/free()  
     --vm-bytes B   malloc B bytes per vm worker (default is 256MB)  
     --vm-stride B  touch a byte every B bytes (default is 4096)  
     --vm-hang N    sleep N secs before free (default is none, 0 is inf)  
     --vm-keep      redirty memory instead of freeing and reallocating  
 -d, --hdd N        spawn N workers spinning on write()/unlink()  
     --hdd-bytes B  write B bytes per hdd worker (default is 1GB)  
     --hdd-noclean  do not unlink files created by hdd workers  
```


