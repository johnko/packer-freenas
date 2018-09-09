Packer templates for FreeNAS
============================

Delete existing box (optional):
```
rm ./FreeNAS-11.1-U6-x64-vbox.box
vagrant box remove freenas/11.1u6x64
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
