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





## b) Hello Vagrant




## c) Mun verkko




## d) Master-slave



## e) As code
