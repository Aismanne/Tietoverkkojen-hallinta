## Hei maailma, verkon yli ja idempotenssi tehtävät.

<h2> Tehtävä A </h2>

Tehtävässä tavoitteena oli asentaa Salt ja sille yksi orja. Valitsin alustakseni Oraclen VirtualBoxin ja sille asennetun Debian käyttöjärjestelmän.

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

Aluksi luodaan kansio, josta herra lukee tarvittavat tiedostot orjan ohjaamiseksi. Tämä kansio luodaan komennolla ``sudo mkdir -p /srv/salt/``. Komennolla ``cd /srv/salt`` voimme siirtyä juuri luomaamme kansioon ja komennolla ``ls`` voimme listata kansion sisällön, joka tulisi olla vielä tyhjä. Komennolla ``sudoedit hellomaailma.sls`` voimme luoda sls tiedoston, jota Salt lukee ja johon voimme kirjoittaa komentoja Saltille. 

Tiedoston sisälle tulee kirjoittaa kommenot, joilla saamme Saltin lisäämään tekstitiedoston orjalle. Saltissa komennot kirjoitetaan YAML:lla. Siinä tärkää on muistaa, että sisennykset ovat aina kahden välilyönnin verran. Jos välilyöntejä on väärä määrä voi ohjelma mennä vikatilaan. 

Alla olevalla koodilla saamme Saltin lisäämään herralla olevan hellomaailma.txt tiedoston orjalle /tmp kansioon. Ohjelma hakee hellomaailma.txt tiedostoa /srv/salt/ kansiosta.

``/tmp/hellomaailma.txt:
    file.managed:
      - source: salt://hellomaailma.txt``

Seuraavaksi tarvitaan hellomaailma.txt, jota ohjelma yrittää siirtää orjalle. Se luodaan komennolla ``sudoedit hellomaailma.txt``. Tätä komentoa voidaan käyttää, jos tällä hetkellä olemme /srv/salt kansiossa sisällä. Jos olemme muussa kansiossa tulee komentoa muuttaa muotoon ``suodedit /srv/salt/hellomaailma.txt``. Tässä tapauksessa tekstitiedosto luodaan määrittelemäämme polkuun eikä sinne kansioon, jossa olemme tällä hetkellä. Hellomaailma.txt tiedoston sisälle voimme kirjoittaa teksiä esim. Hei maailma!. 

Tekstitiedoston tallentamisen jälkeen voidaan Saltilla ajaa luomamme hellomaailma.sls ohjelma. Ohjelma voidaan ajaa komennolla ``sudo salt '*' state.apply hellomaailma``. Komennossa ``'*'`` merkitsee orjia, joille komento ajetaan. Tässä tapauksessa ajetaan komento kaikille orjille, mutta kohtaan voidaan myös kirjoittaa orjien ID:t, joille komento halutaan menevän. ``state.apply hello`` merkitsee mikä tila ajetaan. 

Tilan ajamisen jälkeen Salt ilmoittaa onnistuiko tilan ajaminen, kuinka monta muutosta tehtiin ja epäonnistuiko jokin muutos. Hellomaailma tilaa ajettaessa tulisi onnnistua 1 ja muutoksia tulisi olla 1. Epäonnistumisia tulisi olla 0. Jos tila ajetaan uudelleen tulisi tuloksena olle onnistuneina 1, mutta muutoksia ei pitäisi olla. Voimme tarkistaa tallensiko tila haluamaamme kansionn hellomaailma.txt tiedoston siirtymällä /tmp kansioon komennolla ``cd /tmp``. Tämän jälkeen voimme katsoa kansion sisältöä ``ls`` komennolla ja tarkistaa hellomaailma.txt tiedoston sisällön ``cat hellomaailma.txt`` komennolla. Sisällön tulisi olla Hei maailma!. Jos tiedoston sisältö muuttuu ja hellomaailma tila ajetaan uudelleen palauuttaa Salt tiedoston sisällön takaisin määriteltyyn muotoon. 
