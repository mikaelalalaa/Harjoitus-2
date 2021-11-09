# Harjoitus-2


Tehtävät löytyvät [Tero Karvisen sivulta](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-2021-autumn/#h2-master-slave)

## z) Tiivistelmät

[Salt Quickstart](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/)
 
 
 * opetus Master ja slaven asennuksen koneelle.
 * palomuuri käyttö masterin kanssa, mitä porttia master käyttää.
 * slave avaimen hyväksyminen masterilla
 * komentoa joita voi kokeilla testatakseen oliko asennus onnistunut.
 
 ```
 master$ sudo salt '*' grains.items|less
 
 ```
 Tai 
```
 master$ sudo salt '*' pkg.install httpie
```

[Vagrant Revisited](https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/)

* Vagrantin avulla asentaminen uuden virtuaali koneen.
* miten luotuun koneeseen voi otta yhteyttä 
*   




[Two Machine Virtual Network With Debian 11 Bullseye and Vagrant](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

Sivustolla opetetaan miten voi asentaa Vagrantin ja miten voi kirjautua SSH kautta toiselle luodulle koneelle. 

sisältää mm.
* Komentoja
* Uuden tiedoston luominen
* Poistaa virtuaali koneen

[Salt system architecture](https://docs.saltproject.io/en/latest/topics/salt_system_architecture.html)

 Sivulla kerrotaan yleisestin mikä on Salt ja sen arkkitehtuurista miten se toimii.
 
 Sisältää mm
* Miten salt master ja salt minion toimii
* Kerrotaan joitain esimerkki komentoja ja mitä ne tekee.
    * grains 
    * pkg.



## a) Two-face

Olin aijemmin jo asentanut salt minionin ja masterin komennoilla.
```
sudo apt-get -y install salt-minion
sudo apt-get -y install salt-minion
```
Katsoin ip-osoitteeni komennolla ja otin osoitteen muistiin.
```
sudo hostname -I
```
Sitten ajoin komennon 
```
sudoedit /etc/salt/minion
```
Lisäsin rivin master: (ip osoite) ja tallensin tiedoston.
Tämän jälkeen hyväksyin slave avaimen.
```
sudo salt-key -A
```
Lopuksi testasin että saan orjalta yhteyden, komennoilla.
```
sudo salt '*' grains.item
sudo salt '*' cmd.run 'whoami'
```
![image](https://user-images.githubusercontent.com/93308960/140975770-a082d72c-d6e3-4c94-99b0-23a900753785.png)


## b) Hello Vagrant

Aloitin asennuksen päivittämällä ja sen jälkee asensin itse vagrant.

```
sudo apt-get update
&
sudo apt-get -y install vagrant virtualbox
```
Asennuksien jälkeen aloitin asentamaan debianii bullseye vagrantin avulla, komennolla.
```
sudo vagrant init debian/bullseye64
```
Tämän jälkeen käynnistin koneen komennolla.
```
sudo vagrant up
```
![image](https://user-images.githubusercontent.com/93308960/140977382-effc9f31-cf6e-4184-8d59-8aa110735189.png)

Kun käynnistys onnistui niin testasin yhetyttä SSH kautta
```
sudo vagrant ssh
```
![image](https://user-images.githubusercontent.com/93308960/140977749-661d8c22-c786-4165-bf6e-b59aaaaddfd1.png)
 
 joka onnistui.
 
 Koska kaikki onnistui niin loppujen lopuksi poistin koneen komennolla 
 
 ```
 sudo vagrant destroy
 ```

## c) Mun verkko

Koska aikaisemmassa tehtävässä asennettiin Vagrant jo koneelle, joten aloitin tehtävän luomalla uuden hakemiston nimeltään "twohosts". Luotuun hakemistoon loin uuden tiedoston nimeltään "Vagrantfile"
```
 mkdir twohost
 nano Vagrantfile
```
Vasta luotuun tiedostoon lisäsin alla olevan koodin ja tallensin tiedoston.
```
# -*- mode: ruby -*-
# vi: set ft=ruby :
# Copyright 2019-2021 Tero Karvinen http://TeroKarvinen.com

$tscript = <<TSCRIPT
set -o verbose
apt-get update
apt-get -y install tree
echo "Done - set up test environment - https://terokarvinen.com/search/?q=vagrant"
TSCRIPT

Vagrant.configure("2") do |config|
	config.vm.synced_folder ".", "/vagrant", disabled: true
	config.vm.synced_folder "shared/", "/home/vagrant/shared", create: true
	config.vm.provision "shell", inline: $tscript
	config.vm.box = "debian/bullseye64"

	config.vm.define "sale" do |sale|
		sale.vm.hostname = "sale"
		sale.vm.network "private_network", ip: "192.168.56.4"
	end

	config.vm.define "mastr", primary: true do |mastr|
		mastr.vm.hostname = "mastr"
		mastr.vm.network "private_network", ip: "192.168.56.5"
	end
	
end
```
Lähteet löytyy opettajamme [Tero Karvisen sivulta](https://terokarvinen.com/2021/two-machine-virtual-network-with-debian-11-bullseye-and-vagrant/)

Tämän jälkeen käynnistin koneet komennolla 

```
sudo vargant up
```
![image](https://user-images.githubusercontent.com/93308960/140984686-e6e20e43-c345-43b4-9a72-15e21e689279.png)

Käynnistys oli onnistunut niin otin ensimmäiseksi yhteyden "sale" koneeseen
```
sudo vagrant ssh sale
```

Kun yhetys oli saatu onnistuneestin testasin  yhetyttä toiseen luotuun koneeseen
```
ping 192.168.56.5
```
![image](https://user-images.githubusercontent.com/93308960/140985284-4ee535f6-9362-4286-8cb4-3f9a3d136318.png)

Yhteys saatiin luotua.
Tämän jälkeen postuin "sale" koneesta ```exit``` komennolla ja otin ssh yhteyden "mastr" koneeseen. Josta testasin yhetyttä "sale" koneeseen 
```
sudo vagrant ssh mastr
&
ping 192.168.56.4
```
![image](https://user-images.githubusercontent.com/93308960/140985677-61e02e15-ae4f-458f-9648-b92bf8f8c320.png)

Sitten testasin yhetyttä internettiin ja pingasin googlea
```
ping google.com
```
![image](https://user-images.githubusercontent.com/93308960/140985906-aa357d45-6d68-4f5f-996b-c1a1a6fb6f35.png)

joka myös onnistui.


## d) Master-slave



## e) As code
