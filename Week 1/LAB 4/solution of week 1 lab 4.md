az
az group create --name schullio --location australiaeast
az vm create --name demoweb --resource-group schullio --image UbuntuLTS --generate-ssh-keys
az sshkey create --name "demo_key" --resource-group "schullio"