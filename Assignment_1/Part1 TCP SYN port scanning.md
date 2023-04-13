# TCP SYN port scanning

### 1 TCP SYN host virtual interface 10.0.2.2

![image-20230412202741756](images/image-20230412202741756.png)

### 2 TCP SYN host physical interface 192.168.0.137

![image-20230412202950828](images/image-20230412202950828.png)

### 3 TCP SYN scanning-target without firewall

![image-20230413205732742](images/image-20230413205732742.png)

****![image-20230413210643945](images/image-20230413210643945.png)

### request

![image-20230413211238936](images/image-20230413211238936.png)

### Response(1)

![image-20230413211944664](images/image-20230413211944664.png)

This is very simply that **the port you are trying to connect to is not being listened to on the remote host**. Either your service is not running on the host, or possibly it has been firewalled.

### Response(2)

![image-20230413213302217](images/image-20230413213302217.png)

some response with [SYN,ACK], which means the port is open.

### 4 TCP SYN scanning-target with firewall

![image-20230413205909155](images/image-20230413205909155.png)

![image-20230413210611658](images/image-20230413210611658.png)

