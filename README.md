# Building Rancher Porworx VMware templates 

## The pe of this repo is to provide guidelines on setting up your VMware templates to build Rancher RKE
Clusters you can install Portworx on top of for Data Management inside Rancher.


prerequisites:
At the time of this writing the following environment variables where used.
```
VSphere 7.01 up3
Rancher server 2.6
Centos 7.6 virtual machine template
Linux Kernel 3.10.0-1160.36.2.el7.x86_64
Portworx 2.9
cloud-init
```
###   When building Virtual Machine templates we set the VM template to be the prerequisites as defined by portworx. 

CPU 4vcpu
Ram 4GB
Disk 
	/var = 2GB
        /opt = 3gb

### Storage 
	depends on your cluster storage requirements 
        for demo we just typically start with 20gb additional disk in vmware

### Networking 

10gb is typically adequate

Portworx requires different open ports depending on how it’s installed:
```
Spec-based installations require all Portworx nodes to have open TCP ports at 9001-9022 and an open UDP port at 9002.
Portworx on OpenShift 4+ requires open TCP ports at 17001-17020 and an open UDP port at 17002.
Portworx also requires an open KVDB port. For example, if you’re using etcd externally, open port 2379.
```
If you intend to use Portworx with sharedv4 volumes, you may need to [open your NFS ports](https://docs.portworx.com/portworx-install-with-kubernetes/storage-operations/create-pvcs/open-nfs-ports/).
NOTE: U can tweak these variables in the rancher node templates to suit. However the additional storage should be done manually either before you deploy the cluster as a template if building many of the same cluster. or after inside Vcenter, or via Powercli or automation. 

Before deploying clusters you can read about detailed specs [here](https://docs.portworx.com/start-here-installation/)

### Once you have added all of these specs to your template. you need to clean it and prepare it with cloud-init
```
yum -y install cloud-init

sudo cloud-init start

sudo cloud-init clean
```

shutdown VM

Convert to template 

Template is now ready for use as a Rancher Portworx VMware template

# rancher-portworx-vmware
