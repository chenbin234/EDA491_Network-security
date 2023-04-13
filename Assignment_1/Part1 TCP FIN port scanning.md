# TCP FIN port scanning

### 1.TCP FIN host virtual interface 10.0.2.2

![image-20230413222413132](images/image-20230413222413132.png)

![image-20230413222456218](images/image-20230413222456218.png)

### 2.TCP FIN host physical interface 192.168.0.137

![image-20230413222635618](images/image-20230413222635618.png)

### send 3 ICMP packages in the beginning not ARP

![image-20230413222813321](images/image-20230413222813321.png)

### Response - [RST, ACK]

### 3.TCP FIN scanning-target without firewall

![image-20230413221540481](images/image-20230413221540481.png)

### Response(1) - [RST,ACK]

![image-20230413221854015](images/image-20230413221854015.png)

### Response(2) - no response

### 4.TCP FIN scanning-target with firewall

![image-20230413221022863](images/image-20230413221022863.png)

### Request

![image-20230413221338880](images/image-20230413221338880.png)
