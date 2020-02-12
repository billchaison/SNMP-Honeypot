# SNMP-Honeypot
SNMP community string intercepter

Useful for intercepting SNMP v1 and v2 credentials from vulnerability scanners or monitoring applications.

Example python script "snmp-honeyd.py"<br />
```python
#!/usr/bin/python

import socket
from datetime import datetime
import string

while True:
    data = ""
    server_socket = socket.socket(socket.AF_INET, socket.SOCK_DGRAM)
    server_socket.bind(('0.0.0.0', 161))
    message, address = server_socket.recvfrom(1300)
    now = datetime.now()
    dtn = now.strftime("%m/%d/%Y %H:%M:%S")
    print "Received at " + dtn + " from " + address[0]
    for i in message:
        if ord(i) >= 32 and ord(i) <= 126:
            data += i
        else:
            data += " "
    print "   [" + data + "]\n"
```
