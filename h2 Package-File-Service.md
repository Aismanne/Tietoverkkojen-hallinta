<h1> Package-File-Service tehtävät </h1>

<h2> Tehtävä A </h2>

Tehtävän tavoitteena oli asentaa linuxille jokin uusi demoni aluksi käsin ja sen jälkeen automatisoidusti saltilla. Valitsin Apachen asennettavaksi demoniksi, sillä olen halunnut käyttää sitä mahdolliseen verkkosivun hostaamiseen. 

Ensimmäiseksi päivitetään linuxin repositorit komennolla **``sudo apt-get update``**. Sen jälkeen voidaan asentaa Apache komennolla **``sudo apt-get install apache2``**. Apachen asentamisen jälkeen voidaan käynnistää Apache ja varmistaa että se toimii komennoilla **``sudo systemctl start apache2.service``** ja **``sudo systemctl status apache2.service``**. Jos status komento näyttää että apache on aktiivinen pitäisi sen nyt toimia. (ks. kuva alla)

![Screenshot_120](https://user-images.githubusercontent.com/82207948/114685617-b79a8600-9d1a-11eb-97df-0c3e2d12b290.png)

Apachen asentamisen jälkeen muutetaan apachen porttiasetuksista portti, jota apache kuuntelee. Apachen asetustiedostot löytyvät kansiosta /etc/apache2. Tänne kansioon päästään komennolla **``cd /etc/apache2``**. Komennolla **``sudoedit ports.conf``** voidaan muokata Apachen porttiasetuksia. Muutetaan portiksi, jota apache kuuntelee 999. Muutoksien tallennuksen jälkeen tehdään port.config tiedostosta kopio, jota voidaan käyttää Saltilla asennuksen ja asetusten automatisoinnissa. Kopio tehdään komennolla **``sudo cp ports.conf /srv/salt``**.

Nyt Apache on asennettuna ja porttiasetuksia on muutettu haluamalla tavalla. Seuraavaksi voimme poistaa Apachen ja yrittää sen automatisointia Saltilla. Apachen voi poistaa komennolla **``sudo apt-get purge apache2``**. Tämä komento poistaa Apachen ja myös kaikki sen asetus tiedostot. 

Seuraavaksi automatisoidaan asennus Saltilla. Komennolla **``cd /srv/salt``** siirrytään Saltin kansioon ja sinne luodaan komennolla **``sudo mkdir apache``** apache kansio, josta Salt tila ajetaan. Siirretään /srv/salt kansiossa oleva ports.conf tiedosto, joka kopioitiin aikaisemmin Apachen asetustiedostoista nyt luotuun apache kansioon komennolla **``sudo mv ports.conf apache``**. Tämän jälkeen luodaan Saltille tila, jonka se ajaa. Aluksi siirrytään luotuun apache kansioon **``cd apache``** komennolla. Tämän jälkeen luodaan tila komennolla **``sudoedit init.sls``**.

Init.sls sisään kirjoitetaan tilan komennot. Kaikkia komentoja testataan omassa pienessä osassa, jotta voidaan helposti todentaa tilan toimivuus. Testasin kaikki tilan komennot erikseen ennen niiden lyömistä yhteen. 

**``
apache2:
  pkg.installed
 /etc/apache2/ports.conf:
  file.managed:
    - source: salt://apache/ports.conf
``**
Nyt voimme testata apache tilan ajamista komennolla **``sudo salt '*' state.apply apache``**. Komennon tulisi näyttää onnistumisia olleen 2 ja muutoksia 2. Voimme myös testata vahtiiko tila **ports.cof** tiedostoa, jos muutamme sen sisältä kuunneltavan portin. Tilaa ajettaessa tulisi onnistumisia olla 2 ja muutoksia 1. 

<h2> Tehtävä B </h2>

Tehtävässä B oli tavoitteena asentaa joku täysin uusi ohjelma, jota ei ole käyty tunnilla läpi. Päätin asentaa VLC mediaohjleman. Yritin käyttää **``find``** komentoa löytämään tiedostoja, joita VLC:n asentaminen olisi muuttanut tai lisännyt. Kokeilin **``find -mtime 10, find -print ja find -amin 999``** komentoja, mutta ne eivät palauttaneet mitään VLC:en liittyvää. Osa palautti Permission denied. (Ks. kuvat alla)

![Screenshot_130](https://user-images.githubusercontent.com/82207948/115070747-05bbaf00-9efe-11eb-9a85-f4e0261702a2.png)


![Screenshot_129](https://user-images.githubusercontent.com/82207948/115070749-06544580-9efe-11eb-9245-61ad05d8f88b.png)

<h2> Tehtävä C </h2>

Tehtävässä C tarkoituksena oli ajaa jokin tila paikallisesti, ilman master-slave arkkitehtuuria. Ajoin komennolla **``sudo salt-call --local state.apply hello``**. hello tilan, jonka tulisi luoda /tmp kansioon hellomaailma.txt tiedoston. Tila toimi aivan normaalisit, sillä olen käyttänyt yhtä virtuaalikonetta herrana ja orjana, joten tiedostopoluissa ei ole ongelmia. Kokeilin myös ajaa tilat komennoilla **``sudo salt-call --local state.apply ssh``** ja **``sudo salt-call --local state.apply curl``**. Molemmat tilat toimivat normaalisti. Missään ajamassani tilassa ei ole tiedostopolkuja, joita ei ole olemassa, joten kaikki toimivat normaalisti. Jos tilojen koodi olisi tehty koneille, joilla olisi toinen käyttäjänimi, tai tiedostot olisivat tietyn nimisissä kansioissa, joita ei paikallisella koneella ole, tilat eivät toimisi.

En saanut -debug komentoa lisättyä **``sudo salt-call --local state.apply``** komentojen perään. Etsin ratkaisua jonkin aikaa eri materiaaleista, mutta en saanut sitä toimimaan. Asiaan pitää perehtyä lisää, tai kysyä opettajalta. (Alhaalla kuva paikallisesti ajetusta tilasta.)!

[Screenshot_131](https://user-images.githubusercontent.com/82207948/115072981-92676c80-9f00-11eb-820e-0b9020e64629.png)


<h2> Lähteet </h2>

https://www.tecmint.com/35-practical-examples-of-linux-find-command/ (Yksi hyödyllisimmistä lähteistä find komennon käyttämiseen, jonka löysin)

https://www.tecmint.com/change-apache-port-in-linux/

https://phoenixnap.com/kb/how-to-install-apache-web-server-on-ubuntu-18-04

http://terokarvinen.com/2018/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/ (Käytin tilojen tekemisen muistutuksena)
