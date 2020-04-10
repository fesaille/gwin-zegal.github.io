# Helpers

**Displaying IP address on eth0 interface**
```
ifconfig eth0 | grep "inet ad" | cut -d ':' -f 2 | cut -d ' ' -f 1
```
