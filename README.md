# (Linux) Samsung M2020 Series on x64_86 architecture in CUPS

1. Run
```
apt-get update && apt-get install cups -y 
```

2. If you wish to use printer as network printer - configure /etc/cups/cupsd.conf
```
# Only listen for connections from the local machine.
Listen localhost:631
Listen /run/cups/cups.sock
Listen 10.0.0.1:631 # here put your own IP <your_server_private_network_ip>:631
```
```
# Restrict access to the server...
<Location />
  Order allow,deny
  Allow All
</Location>

# Restrict access to the admin pages...
<Location /admin>
  Order allow,deny
  Allow All
</Location>

# Restrict access to configuration files...
<Location /admin/conf>
  AuthType Default
  Require user @SYSTEM
  Order allow,deny
  Allow All
</Location>
```

3. Put PPD files into /etc/cups/ppd with rights 644 on both files
4. Plug printer via USB
5. Make sure it's visible to Linux
```
lpstat -a

output:
root@optiplex:/etc/cups/ppd# lpstat -a
Samsung_M2020_Series accepting requests since mon, 01 jan 2000, 00:00:00
```
6. Install printer via web interface (available from 127.0.0.1:631 or <machine_ip>:631) using drivers from /etc/cups/ppd
7. Run
```
sudo apt install libcupsimage2 -y
systemctl restart cups
```
