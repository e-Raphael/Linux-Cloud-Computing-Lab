az
az group create --name schullio --location australiaeast
az vm create \
    --resource-group schullio \
    --name binaweb \
    --image UbuntuLTS \
    --admin-username webadmin \
    --generate-ssh-keys
ssh webadmin@20.211.27.92
exit
az vm image list --output table
az vm image list --offer CentOS --all --output table
az vm create --resource-group schullio --name binaweb2 --image OpenLogic:CentOS:6.5:latest --generate-ssh-keys
az vm list-sizes --location australiaeast --output table
az vm create \
    --resource-group schullio \
    --name abimbolaweb \
    --image UbuntuLTS \
    --size Standard_F4s \
    --generate-ssh-keys
az vm show --resource-group schullio --name abimbolaweb --query hardwareProfile.vmSize
az vm list-vm-resize-options --resource-group schullio --name abimbolaweb --query [].name
az vm resize --resource-group schullio --name abimbolaweb --size Standard_DS4_v2
az vm deallocate --resource-group myResourceGroupVM --name myVM
az vm resize --resource-group schullio --name abimbolaweb --size Standard_GS1
az vm start --resource-group schullio --name abimbolaweb
az vm get-instance-view \
    --name abimbolaweb \
    --resource-group schullio \
    --query instanceView.statuses[1] --output table
az vm list-ip-addresses --resource-group schullio --name abimbolaweb --output table
az vm stop --resource-group schullio --name abimbolaweb
az vm start --resource-group schullio --name abimbolaweb
az group delete --name schullio --no-wait --yes
