az
az group create --name schullio --location australiaeast
az vm create \
  --resource-group schullio \
  --name raphaelweb \
  --image UbuntuLTS \
  --admin-username webadmin \
  --generate-ssh-keys
az vm open-port --port 80 --resource-group schullio --name raphaelweb
ssh webadmin@20.248.197.207
sudo apt-get -y update
sudo apt-get -y install nginx
exit
az group delete --name schullio
