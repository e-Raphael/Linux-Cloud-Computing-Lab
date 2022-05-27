az
az group create --name schullio --location australiaeast
az vm create \
  --resource-group schullio \
  --name mondayweb \
  --image UbuntuLTS \
  --size Standard_DS2_v2 \
  --admin-username webadmin \
  --generate-ssh-keys \
  --data-disk-sizes-gb 128 128
az vm disk attach \
    --resource-group schullio \
    --vm-name mondayweb \
    --name myDataDisk \
    --size-gb 128 \
    --sku Premium_LRS \
    --new
ssh webadmin@20.211.126.57
sudo parted /dev/sdc --script mklabel gpt mkpart xfspart xfs 0% 100%
sudo mkfs.xfs /dev/sdc1
sudo partprobe /dev/sdc1
sudo mkdir /datadrive && sudo mount /dev/sdc1 /datadrive
df -h | grep -i "sd"
sudo -i blkid
sudo nano /etc/fstab
UUID=e7d87e36-12c3-4089-b9e3-30cad80fc791  /datadrive  xfs    defaults,nofail   1  2
exit
osdiskid=$(az vm show \
   -g schullio \
   -n mondayweb \
   --query "storageProfile.osDisk.managedDisk.id" \
   -o tsv)
az snapshot create \
    --resource-group schullio \
    --source "$osdiskid" \
    --name osDisk-backup
az disk create \
   --resource-group schullio \
   --name mySnapshotDisk \
   --source osDisk-backup
az vm delete \
--resource-group schullio \
--name mondayweb
az vm create \
    --resource-group schullio \
    --name mondayweb \
    --attach-os-disk mySnapshotDisk \
    --os-type linux
datadisk=$(az disk list \
   -g schullio \
   --query "[?contains(name,'mondayweb')].[id]" \
   -o tsv)
az vm disk attach \
   --g schullio \
   --vm-name mondayweb \
   --name $datadisk
