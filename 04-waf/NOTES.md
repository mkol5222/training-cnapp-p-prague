# CloudGuard WAF

CloudGuard WAF is managed from dedicated Infinity Portal [section](https://portal.checkpoint.com/dashboard/appsec/cloudguardwaf#/waf-policy/getting-started). Open it for tenant `training-cnapp+p-prague`



```shell
# install dig
sudo apt update; sudo apt install dnsutils -y

# app to protect
curl https://ifconfig.me; echo
# try https://ifconfig.me also in browser

# find your alias-color in training dashboard

# verify DNS pointing to WAF platform
dig notpink.lab.klaud.online
# CNAME for wafservice-prg-training.westeurope.cloudapp.azure.com.

# once configured, WAF will behive as your app
curl -vvv -k https://notpink.lab.klaud.online
# but before configured - it is not handled by proxy
curl -vvv  http://red.lab.klaud.online


# incident
curl -vvv -k 'https://notpink.lab.klaud.online/?z=cat+/etc/passed' 

curl -vvv -k 'https://notpink.lab.klaud.online/?z=cat+/etc/passed' | grep 'Incident Id.*</p'
```