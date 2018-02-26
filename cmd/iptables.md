iptables限制特定端口的出口带宽
===============================

```
iptables -A OUTPUT -p tcp --source-port 10000 -m limit --limit 1/s -j ACCEPT
iptables -A OUTPUT -p tcp --source-port 10000 -j DROP
```

上述指令组合可以对端口10000的出口带宽限制在一个MTU(外网网卡的MTU一般为1500，即1500bytes),为直观起见，此处单位用字节。
limit的数值对应的是MTU的个数。
limit的数值与带宽限制值关系如下所示：

|limit的数值 | 带宽限制值 |
| --- | --- |
| 1/s | 1500Bytes |
| 2/s | 1500Bytes * 2 |
| 3/s | 1500Bytes * 3 |
| 4/s | 1500Bytes * 4 |
| ... | ... |
| n/s | MTU * n Bytes|
