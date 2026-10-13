Ez a projekt amiatt jött létre, hogy az órán használt VirtualBox image ARM alapú processzorokon is futhasson!

Az image indítása előtt szükség lesz a következőkre:

***
sudo nano /etc/hosts

127.0.0.1       vm1.test api.vm1.test frontend.vm1.test responsive.vm1.test backend.vm1.test pma.vm1.test docs.vm1.test$
***
sudo nano ~/.ssh/config

Host vm1.test 
	HostName vm1.test 
	Port 10022
***
  