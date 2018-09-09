Packer templates for FreeNAS
============================

Delete existing box (optional):
```
rm ./FreeNAS-11.1-U6-x64-vbox.box
vagrant box remove --force freenas/11.1u6x64
```

Build new box:
```
packer build ./FreeNAS-11.1-U6-x64.json
```

Add box to vagrant:
```
vagrant box add --name freenas/11.1u6x64 ./FreeNAS-11.1-U6-x64-vbox.box
```

Bring up a vagrant machine:
```
vagrant up
```

Use API to create zpool named tank with disk ada1 (optional):
```
bash
curl --verbose --silent http://localhost/account/login/ 2>&1 | tee csrfoutput.txt
COOKIE=$(grep -o 'Cookie:[^;]*' csrfoutput.txt)
TOKEN=$(grep -o 'csrfmiddlewaretoken[^/]*/' csrfoutput.txt | awk -F"'" '{print $3}' | head -n1 )
curl -X PUT -u root:freenas -H "${COOKIE}" -H 'Content-Type: application/json' -d "{\"csrfmiddlewaretoken\": \"${TOKEN}\", \"objects\": [{\"volume_name\": \"tank\", \"layout\": [ { \"vdevtype\": \"stripe\", \"disks\": [ \"ada1\" ]}]}]}" http://localhost/api/v1.0/storage/volume/
rm csrfoutput.txt
```
