# Harjoitus-2


Tehtävät löytyvät [Tero Karvisen sivulta](https://terokarvinen.com/2021/configuration-management-systems-palvelinten-hallinta-ict4tn022-2021-autumn/#h2-master-slave)

## z) Tiivistelmät

[Salt Quickstart](https://terokarvinen.com/2018/salt-quickstart-salt-stack-master-and-slave-on-ubuntu-linux/)
 
 Sivulla opastetaan miten voi asentaa Master ja slaven koneelle.
 * Kuten jos on palomuuri käytössä niin, mitä portteja master käyttää.
 * Miten voi hyväksyä slave avaimen masterilla
 
 Kerrotaan myös pari komentoa joita voi kokeilla testatakseen oliko asennus onnistunut.
 
 ```
 master$ sudo salt '*' grains.items|less
 
 ```
 Tai 
```
 master$ sudo salt '*' pkg.install httpie
```

[Vagrant Revisited](https://terokarvinen.com/2017/04/11/vagrant-revisited-install-boot-new-virtual-machine-in-31-seconds/)

Sivulla kerrotaan miten voi asentaa Vagrantin avulla uuden virtuaali koneen.
Kerrotaan myös millä luotua konetta voi hallita

sisältää mm.
* Komentoja
* SSH


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

## c) Mun verkko




## d) Master-slave



## e) As code
