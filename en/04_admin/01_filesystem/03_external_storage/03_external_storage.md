# Integrating external storage

## General

Most digitisation projects involve handling very large volumes of data. In most cases, this makes it necessary to link external storage capacity to the server. This can be done in a number of ways. We recommend that the external storage is linked to the following folder in the directory tree:

```bash
/opt/digiverso/
```

This means that all Goobi data can be found in a central location.

Two solutions for integrating external storage are explained in schematic form below. We do not recommend linking via CIFS as this can affect performance and functionality. Furthermore, CIFS does not allow you to produce symbolic links or read-only rights.

## NFS Share

The following information is required if you wish to integrate external storage via an NFS Share

• exporting server  
• exporting directory

You can then add the storage to the directory tree via NFS. It is a good idea to add an entry into the file /etc/fstab that automatically sets up the link when the system starts up. This entry could be as follows:

```bash
example.net:/path/to/share /opt/digiverso nfs vers=3,rsize=8192,wsize=8192,soft,intr,rw,auto 0 0
```

## Logical volume in the virtual machine

Another way of integrating external storage is to attach it to the virtual machine as an independent device. This can be different iSCSIs or SAN LUNs. They are subsequently combined into a logical volume in the virtual machine using LVM. The result is an aggregated storage unit based on a number of devices.