[Port Knocking ](https://github.com/pha5matis/Pentesting-Guide/blob/master/port_knocking.md) **<- Check**
[Knock Knockin on Servers Ports (ESP)](https://poesiabinaria.net/2017/08/knock-knock-knockin-on-servers-ports-port-knocking-ejemplos/#coacutemo-hacer-el-golpeo-de-puertos) **<- Check**

## Nmap/bash
```bash
$ for x in 4000 5000 6000; do nmap -Pn --host-timeout 201 --max-retries 0 -p $x server_ip_address; done
```


## knock (apt get install knockd)

```bash
Syntax: knock <ip> <port>
$ knock 192.168.1.21 300 350 400
```

