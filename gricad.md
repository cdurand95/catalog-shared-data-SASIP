# How to access data from GRICAD

 - If you don't have an account, create it [here](https://perseus.univ-grenoble-alpes.fr/create-account/portal) (select chercheur in contract type if you have a permanent position or are a post-doc, doctorant if you are PhD) and ask to join the pr-sasip project.
 - Read carefully the [computation center documentation](https://gricad-doc.univ-grenoble-alpes.fr/en/)
 - Once logged to dahu (CPU) or bigfoot (GPU), you have access to the storage at : ```/summer/sasip```


### Configuration of your access to gricad

You can set up a direct access to dahu via [this procedure](https://gricad-doc.univ-grenoble-alpes.fr/en/hpc/connexion/#connecting-to-the-gateways-without-a-password) so that ssh and scp takes only one line of command, a simplified version is reported below :

  - Check that you should be able to connect to the bastions : ```ssh <your-login>@rotule.u-ga.fr``` and ```ssh <your-login>@trinity.u-ga.fr``` (replace <your-login> with your perseus account)
  - Once connected on one of the bastions, check that you can connect to dahu (for CPU) : ```ssh dahu``` or bigfoot (for GPU) ```ssh bigfoot```
  - To connect directly to dahu or bigfoot, add the following lines to your ```.ssh/config``` :

```bash
Host *
  ServerAliveInterval 30
  AddKeysToAgent yes
  IdentityFile ~/.ssh/id_rsa
  ForwardX11 yes
  TCPKeepAlive yes
 
Host *.ciment
  User <your-login>
  ProxyCommand ssh -q <your-login>@access-gricad.univ-grenoble-alpes.fr "nc -w 60 `basename %h .ciment` %p"
```

  - Now you should be able to connect to dahu directly with ```ssh dahu.ciment``` or to bigfoot with ```ssh bigfoot.ciment```
  - To connect without typing your password, you can set up a SSH key :
    - on your local machine create the ssh key : ```ssh-keygen```
    - copy the public key to the bastions : ```ssh-copy-id -i .ssh/id_rsa.pub <your-login>@rotule.u-ga.fr:``` and  ```ssh-copy-id -i .ssh/id_rsa.pub <your-login>@trinity.u-ga.fr:``` and to the clusters : ```ssh-copy-id -i .ssh/id_rsa.pub <your-login>@dahu.ciment:``` or ```ssh-copy-id -i .ssh/id_rsa.pub <your-login>@bigfoot.ciment:```



