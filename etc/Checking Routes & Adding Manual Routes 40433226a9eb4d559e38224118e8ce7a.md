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
ip route add 192.168.222.0/24 via 10.172.24.1       # Here 10.172.24.1 is the address of the gateway for subnet 192.168.222.0/24
```