## Hei maailma, verkon yli ja idempotenssi tehtävät.

<h2> Tehtävä A </h2>

<p> Tehtävässä tavoitteena oli asentaa Salt ja sille yksi orja. Valitsin alustakseni Oraclen VirtualBoxin ja sille asennetun Debian käyttöjärjestelmän. </p>

Saltin asentamiseksi on ensimmäisenä avattava käyttöjärjestelmän terminaali. Sieltä voimme asentaa tarvittavan Salt ohjelman ja myös antaa sille tarvittavia komentoja. Salt master ohjelman asentamiseksi tulee terminaaliin antaa komennot ``sudo apt-get install salt-master``. Tämä asentaa Salt herra ohjelman, jolla orjia ohjataan. Tämän jälkeen asennetaan orja ohjelma toiselle koneelle, joka tässä tapauksessa on sama virtuaalikone. Orjalle ohjelma saadaan käyttämällä terminaalissa komentoa ``sudo apt-get install salt-minion``

Asennuksen jälkeen tulee muokata orjan asetus tiedostoa, jotta se tietää missä osoitteessa herra on. Tämä voidaan toteuttaa komennolla ``sudoedit /etc/salt/minion``
Tämä avaa minion nimisen asennustiedoston muokattavaksi. Asetustiedostosta poistetaan # merkki master: rivin edestä ja kirjoitetaan sen perään herra koneen osoite.
Tämän jälkeen poistetaan # merkki kohdasta id ja lisätään siihe haluttu nimi orjalle. Tässä tapauksessa nimeämme sen minioniksi
Herra koneen osoite voidaan selvittää käyttämällä herra koneella komentoa ``hostname -I``.

Jotta orja saadaan yhdistämään herraan ja asetuksiin tehdyt muutokset ajettua tulee salt-minion ohjelmaa käynnistää uudelleen. Uudelleenkäynnistys tapahtuu komennolla ``sudo systemctl restart salt-minion.service``. Nyt käyttämällä komentoa ``sudo systemctl status salt-minion`` voimme nähdä että ohjelman status on Aktiivinen ja se on ollut päällä vain hetken, sillä käynnistimme sen uudelleen. 

Seuraavaksi meidän tulee hyväksyä herra koneella orjien avaimet, jotta voimme alkaa ohjaamaan niitä. Avaimet hyväksytään komennolla ``sudo salt-key -A``. Komennolla ``sudo salt-key`` näemmä kaikki hyväksytyt ja hylätyt avaimet. Hyväksytyt avaimet kohdassa tulisi nyt luke minion. 

Nyt voimme testata toimiiko yhteys orjaan komennolla ``sudo salt '*' cmd.run 'whoami'``. Vastauksen tulisi palauttaa minion: root. Jos vastauksena tuli tämä on yhteys toiminnassa.

<h2> Tehtävä B </h2>


Tehtävässä oli tarkoitus luoda tiedosto, joka luo orjalle Hei maailma tiedoston, jota muokataan vain, jos siihen on tehty muutoksia

sda
