# Deploy OpenShift Origin on Single VM with Cloud Init

```
az group create -n cloud-init-osorigin-disk -l eastus

az vm create \
  --resource-group cloud-init-osorigin-disk \
  --name centos74 \
  --size Standard_D4s_v3 \
  --data-disk-sizes-gb 32 \
  --public-ip-address-dns-name jzosorigindisk \
  --storage-sku Premium_LRS \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud-init-osorigin-master.yml \
  --ssh-key-value /Users/jimzim/.ssh/id_rsa.pub
  
- Need to open the port in order for ansible installer to work
az vm open-port -g cloud-init-osorigin-disk -n centos74 --port 8443 --priority 100

az group delete -n cloud-init-osorigin-disk --no-wait -y

```

```
az group create -n cloud-init-osrhel -l eastus

az vm create \
  --resource-group cloud-init-osrhel \
  --name osrhel \
  --size Standard_D4s_v3 \
  --data-disk-sizes-gb 32 \
  --public-ip-address-dns-name jzosrhel \
  --storage-sku Premium_LRS \
  --image RedHat:RHEL:7-RAW-CI:latest \
  --custom-data cloud-init-osorigin-master.yml \
  --ssh-key-value /Users/jimzim/.ssh/id_rsa.pub

az vm open-port -g cloud-init-osrhel -n osrhel --port 8443 --priority 100

az group delete -n cloud-init-osrhel --no-wait -y

```

