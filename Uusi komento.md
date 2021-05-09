<h1> Uusi komento </h1>

<h2> Tehtävä A </h2>

Tehtävässä tein testi nimisen bash komennon, joka tulostaa Hello tulosteen. Tein myös init.sls tiedoston erillisen kansion sisään, joka asentaa komennon orjille, antaa komennolle oikeudet, joilla kaikki voivat lukea ja käyttää sitä, mutta eivät kirjoittaa siihen. Salt ohjelma ajaa myös komennon tilaa ajettaessa.

![Screenshot_166](https://user-images.githubusercontent.com/82207948/117572702-bcb1e180-b0dc-11eb-9ab0-d74144c324ea.png)

Komennon ajaminen onnistui normaalisti ja testi tiedosto asentui /usr/local/bin sijaintiin.

![Screenshot_167](https://user-images.githubusercontent.com/82207948/117572747-ebc85300-b0dc-11eb-869b-2b6fb543e39f.png)

Alla näkyy tuloste komennolla **``ls -l /usr/local/bin/testi``**

![Screenshot_168](https://user-images.githubusercontent.com/82207948/117572854-85900000-b0dd-11eb-8207-59b95e223ec4.png)

<h2> Tehtävä B </h2>

Tehtävässä oli tarkoituksena luoda uusi komento, joka antaa tietoja koneesta tai muuttaa asetuksia. Tein whatsup.sh nimisen komennon, joka kertoo ajettaessa järjestelmän arkkitehtuurin, näytönohjain adapterin tiedot, järjestelmän nimen ja päivämäärän, sekä kellonajan. Saltilla ohjelman asentamiseen käytin edellisen tehtävän tilaa, josta muutin tiedostonimet ja poistin testin, joka ajaa komennon Saltilla tilan ajettaessa (En osaa sanoa onko sillä mitään käytännön etua, että näkee pystyykö orja sen ajamaan suoraan?)

![Screenshot_169](https://user-images.githubusercontent.com/82207948/117575528-ebcf4f80-b0ea-11eb-880b-3a25b69e67d0.png)

Komento antaa alla olevan näköisen tulosteen sitä ajettaessa.

![Screenshot_170](https://user-images.githubusercontent.com/82207948/117575607-410b6100-b0eb-11eb-96df-39f45639647f.png)

<h2> Tehtävä C </h2>

Tehtävässä piti luoda python scripti ja asentaa se orjille. Loin hello.py scriptin ja laitoin sen tulostamaan Hei kaikki konsoliin. Käytin tässäkin tehtävässä A tehtävän init.sls tiedostoa scriptin Saltilla asentamiseksi. 

![Screenshot_172](https://user-images.githubusercontent.com/82207948/117576010-d824e880-b0ec-11eb-9d99-6a24eaacc828.png)

<h2> Tehtävä D </h2>

Tehtävässä oli tarkoituksena luoda Salt tila, joka asentaa kansiollisen scriptejä orjakoneelle. Loin tilan moni, jonka sisään loin **init.sls** tiedoston ja **bin** kansion. Bin kansioon laitoin 3 scriptiä: **bashtesti** **pierut** ja **testi.py**. **init.sls** tiedoston sisällä käytin file.recurse komentoa, joka asentaa kaiken bin kansion sisällä orjalle.

![Screenshot_174](https://user-images.githubusercontent.com/82207948/117576431-a745b300-b0ee-11eb-9044-36308f2c27c0.png)

Salt tilan ajamisen jälkeen kaikki komennot toimivat orjalla. 

<h2> Tehtävä E </h2>

Tehtävässä oli tarkoituksen tutkia toisten opiskelijoiden loppuprojekteja ja tiivistää niistä kuvaus.

Ensimmäiseksi projektiksi valitsin Silja Guptan projekti, joka asentaa blenderin valmiiksi käyttäjälle, ja ottaa käyttöön parhaat asetukset. Projekti toimii ilmeisest vain Xubuntu live tikulla tällä hetkellä, mutta vaikuttaa hyödylliseltä, jos se saataisin toimimaan muillakin järjestelmillä.

https://siljagupta.wordpress.com/2018/05/10/palvelinten-hallinta-h6-blender-moduli/

Toiseksi projektiksi valitsin Eetu Pihamäen projekti, jossa moduuli asentaa VirtualBoxin Ubuntulle niin että sitä voi käyttää suoraan selaimessa. Moduuli vaikuttaa todella mielenkiintoiselta, sillä näkisin sille käyttöä itsellänikin. 

https://siljagupta.wordpress.com/2018/05/10/palvelinten-hallinta-h6-blender-moduli/

Kolmanneksi projektiksi valitsin Aatu Alasen moduulin, joka asentaa Teamspeak 3 palvelimen ja antaa sille asetukset, jotta sitä voidaan suoraan käyttää. Moduuli olettaa että sitä käytetään Xubuntu 18.04 käyttöjärjestelmää. 

https://github.com/Suoladgl/Moduuli




