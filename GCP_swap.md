# GCP Swap

- create a swap file

```bash
sudo fallocate -l 1G /swapfile
```

- add permission

```bash
sudo chmod 600 /swapfile
```

- make the file as swap space

```bash
sudo mkswap /swapfile
```

- enable the swap space

```bash
sudo swapon /swapfile
```

- check the status

```bash
sudo swapon --show
```

- modify to permanent

```bash
sudo vim /etc/fstab

# edit the file: add to the tail
/swapfile swap swap defaults 0 0
```

- configure swappiness value (how often your system swaps data out of RAM to the swap space)

```bash
cat /proc/sys/vm/swappiness

# method 1
sudo sysctl vm.swappiness=10

# method 2, modify sysctl.conf
sudo vim /etc/sysctl.conf
vm.swappiness=10
```

- increase swap space

```bash
# turn off 
sudo swapoff -v /swapfile
# delete /swapfile
# sudo rm /swapfile
# resize the swap (from 512 MB to 8GB)
sudo dd if=/dev/zero of=/swapfile bs=1G count=8
# make the file usable as swap
sudo mkswap /swapfile
# activate the swap file
sudo swapon /swapfile
```
