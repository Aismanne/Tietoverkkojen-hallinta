<h1> Package-File-Service tehtävät </h1>

<h2> Tehtävä A </h2>

Tehtävän tavoitteena oli asentaa linuxille jokin uusi demoni aluksi käsin ja sen jälkeen automatisoidusti saltilla. Valitsin Apachen asennettavaksi demoniksi, sillä olen halunnut käyttää sitä mahdolliseen verkkosivun hostaamiseen. 

Ensimmäiseksi päivitetään linuxin repositorit komennolla ``sudo apt-get update``. Sen jälkeen voidaan asentaa Apache komennolla ``sudo apt-get install apache2``. Apachen asentamisen jälkeen voidaan käynnistää Apache ja varmistaa että se toimii komennoilla ``sudo systemctl start apache2.service`` ja ``sudo systemctl status apache2.service``. Jos status komento näyttää että apache on aktiivinen pitäisi sen nyt toimia. (ks. kuva alla)

![Screenshot_120](https://user-images.githubusercontent.com/82207948/114685617-b79a8600-9d1a-11eb-97df-0c3e2d12b290.png)

Apachen asentamisen jälkeen muutetaan apachen porttiasetuksista portti, jota apache kuuntelee. Apachen asetustiedostot löytyvät kansiosta /etc/apache2. Tänne kansioon päästään komennolla ``cd /etc/apache2``. Komennolla ``sudoedit ports.conf`` voidaan muokata Apachen porttiasetuksia. Muutetaan portiksi, jota apache kuuntelee 999. Muutoksien tallennuksen jälkeen tehdään port.config tiedostosta kopio, jota voidaan käyttää Saltilla asennuksen ja asetusten automatisoinnissa. Kopio tehdään komennolla ``sudo cp ports.conf /srv/salt``.

Nyt Apache on asennettuna ja porttiasetuksia on muutettu haluamalla tavalla. Seuraavaksi voimme poistaa Apachen ja yrittää sen automatisointia Saltilla. Apachen voi poistaa komennolla **``sudo apt-get purge apache2``**. Tämä komento poistaa Apachen ja myös kaikki sen asetus tiedostot. 

Seuraavaksi automatisoidaan asennus Saltilla. Komennolla ``cd /srv/salt`` siirrytään Saltin kansioon ja sinne luodaan komennolla ``sudo mkdir apache`` apache kansio, josta Salt tila ajetaan. Siirretään /srv/salt kansiossa oleva ports.conf tiedosto, joka kopioitiin aikaisemmin Apachen asetustiedostoista nyt luotuun apache kansioon komennolla ``sudo mv ports.conf apache``. Tämän jälkeen luodaan Saltille tila, jonka se ajaa. Aluksi siirrytään luotuun apache kansioon ``cd apache`` komennolla. Tämän jälkeen luodaan tila komennolla ``sudoedit init.sls``.

Init.sls sisään kirjoitetaan tilan komennot. Kaikkia komentoja testataan omassa pienessä osassa, jotta voidaan helposti todentaa tilan toimivuus. Testasin kaikki tilan komennot erikseen ennen niiden lyömistä yhteen. 

``
apache2:
  pkg.installed
 /etc/apache2/ports.conf:
  file.managed:
    - source: salt://apache/ports.conf
``
dads
