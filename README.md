# ESCFLARE

## Script for appending/updating DNS records on CloudFlare

![](https://github.com/alive-corpse/escflare/raw/master/screen.png)

### Features:
* updating of existing records, creating new records in case of notexisting
* should working on OpenWRT based devices and similar firmwares based devices, required ca-bundle and curl
* using parameters from cli or saving them inside script
* bulk updating of few records for one run
* using IP address for updating as well as network interface name

##### Notice: at the moment script working only with A-type records.

### Setup:
```bash
wget https://raw.githubusercontent.com/alive-corpse/escflare/master/escflare
chmod +xw escflare
```

### Using:

You should get api key in your CloudFlare's profile. In "API Keys" section
find "View" button near the "Global API Key label".

##### Simple way to use
```
./escflare <add|create|update> <subdomain>.<domain.name> <iface|ip> [ttl]
```
Examples:
```bash
# vailiy.pupkin.ru - domain name with subdomain(s)
# wan0 - network interface name (you can also use IP address instead)
./escflare update vasiliy.pupkin.ru wan0
```
```bash
# Subdomains can be divided by comma. You can use * for wildcard and @ for root record. If some record is not exists, it will be created. 
./escflare 'vasiliy,*,@,ivan,sergey.pupkin.ru' 123.234.123.234 14400
```

##### Notices
* At first run script will ask you for all needed variables such as email, key, default tty and will save them inside itself.

* It will not update record again with the same content and ttl. You can force updating with the same data by setting variable forcedupdate with sone nonempty value.


### Getting all of current parameters
You can get all parameters and values by running:
```bash
./escflare <list|ls|show>
```

### Setting/updating parameters

Updating credentials:
```bash
./escflare set cred
```

Updating default ttl value:
```bash
./escflare set ttl
```

Updating default iface value:
```bash
./escflare set iface
```

Updating forcedupdate value (you can just set it to 1 or clean to turn off forced updating):
```bash
./escflare set forcedupdate
```

### Cleaning/resetting parameters

Cleaning parameter by it's name:
```bash
./escflare <clean|clear> <variable name>
```

Cleaning all of main parameters:
```bash
./escflare <clean|clear> all
```

### Logging

There are three main logging levels: debug/info/warning, info is setted by default. For permanent changing set value for llevel parameter:
```bash
./escflare set llevel
```
Also you can change it temporary by setting ll environment value:
```bash
ll=debug ./escflare update vasiliy.pupkin.ru wan0
```

