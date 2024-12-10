# CloudGuard WAF

CloudGuard WAF is managed from dedicated Infinity Portal [section](https://portal.checkpoint.com/dashboard/appsec/cloudguardwaf#/waf-policy/getting-started). Open it for tenant `training-cnapp+p-prague`

WAF has multiple deployment options - managed service (SaaS), VM, VMSS/ASG, Docker, Kubernetes container or Ingress, native NGINX embedded and more.

Web applications are defined as `assets` with specific security practices and configuration data to be enforced on specific `profile` used to install one or many WAF agents.

### Lab deployment

[Profiles section](https://portal.checkpoint.com/dashboard/appsec/cloudguardwaf#/waf-policy/profiles/) has preconfigured profile `waf` used to deploy existing VM in Azure running on `wafservice-prg-training.westeurope.cloudapp.azure.com` which can be used as alias(CNAME) for real services e.g. `notpink.lab.klaud.online`.

So you do not need to worry about enforcement part - VM is running for you and was even provided with valid wildcard certificate `*.lab.klaud.online` to make HTTPS setup easy.

![alt text](./img/agent-profile.png)

### Knowing the environment

![alt text](image.png)
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