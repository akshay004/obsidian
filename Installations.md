Give sudo permission to user
```shell
ubuntu ALL=(ALL) NOPASSWD: ALL
```

DOCKER
```shell
sudo apt update -y
sudo apt  install docker.io -y
mkdir -p ~/.docker/cli-plugins/
curl -SL https://github.com/docker/compose/releases/download/v2.3.3/docker-compose-linux-x86_64 -o ~/.docker/cli-plugins/docker-compose
chmod +x ~/.docker/cli-plugins/docker-compose
sudo usermod -aG docker ubuntu
sudo systemctl start docker.service
sudo chmod 666 /var/run/docker.sock

```

SWAP
```shell
sudo dd if=/dev/zero of=/swapfile bs=20M count=200
sudo chmod 600 /swapfile
sudo mkswap /swapfile
sudo swapon /swapfile
echo "/swapfile swap swap defaults 0 0" | sudo tee -a /etc/fstab
```

```shell
export PS1="awsdev1-inno \@[\w] \$ "
```

## For wildcard certificate
https://www.youtube.com/watch?v=VJPfdXN-dSc&t=534s
sudo certbot certonly --manual --preferred-challenges dns <naked_domain> *.<naked_domain>

To create SSL 
https://ongkhaiwei.medium.com/generate-lets-encrypt-certificate-with-dns-challenge-and-namecheap-e5999a040708

sudo apt install certbot -y
sudo certbot certonly --manual --preferred-challenges dns -d hostinglive.co.in

To check certificate 
```shell
sudo certbot certificates
```

## Add Logging 

```shell
logging:
      driver: "json-file"
      options:
        max-file: "5"
        max-size: "5m"
```

Login from one container to another container 

https://medium.com/@mfahad1667/ssh-connection-between-two-docker-container-7c9dced1aa43 

Repeat the below steps in both containers to install ssh-keygen 

apt-get update
apt-get install openssh-server
apt-get install vim
vim /etc/ssh/sshd_config
service --status-all
service ssh start
service --status-all
