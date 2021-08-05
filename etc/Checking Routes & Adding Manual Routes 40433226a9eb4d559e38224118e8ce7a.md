# Checking Routes & Adding Manual Routes

---

### Checking Routes

```
ip route    # Checking defined routes in linux
route       # Checking defined routes in linux
route print     # Checking defined routes in windows
```

### Adding Manual Routes

```
ip route add <subnet> via <gateway or router address>
```

for example,

```
ip route add 192.168.222.0/24 via 10.172.24.1       
```
