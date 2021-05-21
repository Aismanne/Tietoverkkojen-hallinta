<h1> Oma moduuli </h1>

<h2> Tehtävä A </h2>

Tehtävä h1: https://github.com/Aismanne/Tietoverkkojen-hallinta/blob/1main/Hei%20maailma%2C%20verkon%20yli%20ja%20idempotenssi.md

Tehtävä h2: https://github.com/Aismanne/Tietoverkkojen-hallinta/blob/1main/Package%20File%20Service.md

Tehtävä h3: https://github.com/Aismanne/Tietoverkkojen-hallinta/blob/1main/Versionhallinta.md

Tehtävä h4: https://github.com/Aismanne/Tietoverkkojen-hallinta/blob/1main/Uusi%20komento.md

Tehtävä h5: https://github.com/Aismanne/Tietoverkkojen-hallinta/blob/1main/Aikajana.md

Tehtävä h6: ~Tulossa~

<h2> Tehtävä B </h2>

Tehätävässä tavoitteena oli luoda jokin oma moduuli, jolla olisi jokin oikean maailman käyttötarkoitus. Idean keksiminen oli mielestäni melko hankalaa, sillä kaikki ideat tuntuivat liian simppeleiltä tai typeriltä. Päädyin lopulta luomaan moduulin, jota voidaan käyttää uuden Debian asennuksen käyttöönotossa. Päädyin tähän, sillä olin juuri ottanut käyttöön Debian pohjaisen koneen, jota käytän palvelimena omille projekteilleni. Tilaa olisi siis tarkoitus käyttää VirtualBoxin sisällä pyörivästä Debianista, joka toimii herrana, erillisellä PC:llä pyörivään Debianiin joka toimii orjana. Molemmat laitteet toimivat samassa lähiverkossa. 

Moduulin halusin asentavan LAMP paketin ohjelmia, sillä olen halunnut ylläpitää omia verkkosivuja ja opetella LAMP ohjelmistojen käyttöä. Tein myös moduuliin tilan, joka asentaa LAMP paketin lisäksi itselleni hyödyllisä ohjelmia, kuten OpenSSH-serverin, Treen, Curlin ja Nanon.

Ensimmäiseksi asensin kaikki LAMP paketin ohjelmat ja OpenSSH-server ohjelman herra koneelle käsin, jotta saisin niiden asetustiedostot ja voisin muokata niitä ja sen jälkeen käyttää niitä orjalle asennuksessa. Apachen ja OpenSSH:n asetustiedostot olivat jo tuttuja, sillä olen käyttänyt niitä aikaisemminkin. LAMP paketista muut ohjelmat eivät olleet tuttuja eikä minulla ollut niistä valmiiksi asetustiedostoja. Hetken taustatutkimuksen jälkeen päätin jättää näiden asetukset sikseen, sillä kaikkien ohjelmien käyttöön tutustumisessa olisi mennyt melko kauan enkä halunnut säätää vain satunnaisia asetuksia. 

Käsin asentamisen jälkeen loin **``srv/salt``** kansioon kaksi uutta kansiota **``Lamp_stack``** ja **``Useful_programs``**. Tämän jälkeen loin näihin uusiin kansioihin molempiin **``Config_files``** kansiot, joihin laitoin asennettavien ohjelmien asetustiedostot, jotka haluaisin siirtyvän orjalle. **``/Lamp_stack/Config_files``** kansion sisälle laitoin Apachen asetustiedostot **``apache2.conf``** ja **``ports.conf``**. **``apache2.conf``** tiedostoon olin tehnyt muutoksia, jotka estävät virhe sivua kertomasta Apachen versiotietoja yms. Estin myös Apachea listamaasta kansioita, jos index tiedostoa ei ole olemassa. Tämän jälkeen lisäsin **``/Useful_programs/Config_files``** kansioon OpenSSH:n **``sshd_config``** asetustiedoston, johon olin muuttanut käytettävän portin, salasana yritysten määrän ja root kirjautumisen eston salasanalla.

Kansioiden luomisen ja asetustiedostojen lisäämisen jälkeen siirryin **``/srv/salt/Lamp_stack``** kansioon ja loin sinne **``init.sls``** tiedoston, johon tein tilan joka asentaa LAMP paketin ja sen ohjelmien asennustiedostot. Tila myös käynnistaa Apachen uudelleen jos **``apache2.conf``** tai **``ports.conf``** tiedostoja muutetaan. Tilaa luodasse pala palalta ilmeni testivaiheissa muutamia kirjoitusvirheitä, mutta muuten tila toimi hyvin.  Alla on kuva **``/srv/salt/Lamp_stack/init.sls``** tiedoston sisällöstä.

![Screenshot_191](https://user-images.githubusercontent.com/82207948/119114563-f238c200-ba2e-11eb-8a62-2ca0897fa2d6.png)

LAMP paketin tilan luomisen jälkeen sirryin **``/srv/salt/Useful_programs``** kansioon ja loin sinne taas **``init.sls``** tiedoston, johon tein tilan joka asentaa cURL:in, Treen, Nanon ja OpenSSH-Serverin, sekä antaa OpenSSH:lle asetustiedoston ja uudelleenkäynnistää OpenSSH: jos asetustiedosto muuttuu. Näin asetukset saadaan heti käyttöön. Alla on kuva **``/srv/salt/Useful_programs/init.sls``** tiedoston sisällöst.

![Screenshot_192](https://user-images.githubusercontent.com/82207948/119120247-be609b00-ba34-11eb-8897-1a582544f527.png)

Tilojen luomisen jälkeen loin **``/srv/salt``** kansioon **``top.sls``** tiedoston, jolla molemmat tilat saadaan ajettua **``sudo salt '*' state.apply``** komennolla. Alla on kuva **``top.sls``** tiedoston sisällöstä.

![Screenshot_193](https://user-images.githubusercontent.com/82207948/119120695-3c24a680-ba35-11eb-9b17-614dcc86044a.png)

Tässä vielä Tree:llä näytetty kuva moduulin kansiorakenteesta. 

![Screenshot_194](https://user-images.githubusercontent.com/82207948/119120899-78f09d80-ba35-11eb-83ac-a29277491649.png)

Tilaa ajettaessa komennolla **``sudo salt '*' state.apply``** se toimii! Tila muuttaa asetustiedostot ja asentaa tarvittavat ohjelmat kuten pitää. Tila toimii myös idempotenssisti, eikä tee muutoksia ellei niille ole tarvetta. Alla kuvia muutamasta eri kerrasta, kun tila on ajettu

![Screenshot_197](https://user-images.githubusercontent.com/82207948/119121944-ab4eca80-ba36-11eb-8114-f7fd169bd4c8.png)

![Screenshot_196](https://user-images.githubusercontent.com/82207948/119121921-a558e980-ba36-11eb-918a-32f9ecb182bb.png)

Tila antaa kuitenkin varoituksen **``/Lamp_stack/init.sls``** tiedostosta löytyvästä "virtuaali paketista", jota ei enää tueta? Se ei tällä hetkellä vaikuta tilan toimivuuteen, mutta jatkossa saattaa aiheuttaa ongelmia. En kerennyt tutustua ongelmaan tarkemmin, mutta uskon että etsimällä paketin oikea nimi ja käyttämälllä sitä ongelma saataisiin ratkaistua. Täytyy tutustua aiheeseen lisää. Alla kuva varoituksesta, jonka tila antaa

![Screenshot_195](https://user-images.githubusercontent.com/82207948/119121795-82c6d080-ba36-11eb-9d52-234e3f1ecd92.png)
 
Tilan ajamisen jälkeen voidaan testata toimivatko ohjelmat, joita asennettiin oikein. Apachea voidaan testata menemällä orjan IP osoitteeseen verkkoselaimella. Siellä näkyy Apachen default verkkosivu! Apache siis toimii. Myös ajamamme asetukset toimivat, sillä virheilmoitus ei anna tietoa Apache versiosta tai käyttöjärjestelmästä, jossa se pyörii. Muita LAMP paketin ohjelmia en kerenny testaamaan. Myös SSH yhteys toiseen koneeseen toimii määrittelemälläni portilla ja orjan konellaa kaikki asentamamme hyötyohjelmat toimivat halutusti. Alla kuvia Apachen toimivuudesta.

![Screenshot_198](https://user-images.githubusercontent.com/82207948/119122495-3d56d300-ba37-11eb-9b07-90216531913b.png)

![Screenshot_199](https://user-images.githubusercontent.com/82207948/119123975-d4705a80-ba38-11eb-83ed-bf7fd35f9b2a.png)
