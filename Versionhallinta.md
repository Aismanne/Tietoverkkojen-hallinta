<h1> Versionhallinta tehtävät </h2>

<h2> Tehtävä D </h2>

Tehtävässä D tavoitteena oli käyttää komentoja **``git log, git diff ja git blame``**. Testasin komentoja omassa Java projektissani, käyttämällä Gittiä.

Komento **``git log``** antaa vastauksena commit lokit. Lokissa näkyy kuka on tehnyt muutoksia projektiin, milloin ja se myös näyttää commitin mukana annetut kommentit. Loki on konsolissa niin että alimmaisena näkyy vanhin kirjaus ja ylimpänä uusin kirjaus. Omassa Git lokissani näkyy kaverini, ja minun tekemät muutokset, sekä haarojen 
yhdistäminen. Komennolla **``git log --patch-with-stat``** saadaan myös näkyviin tiedostojen sisällä tehdyt muutokset. 


![Screenshot_96](https://user-images.githubusercontent.com/82207948/115474871-185c1e00-a247-11eb-941d-030699eb8e28.png)

Komento **``git diff``** antaa tulokseksi muutokset, joita sinulla on ja joite ei ole vielä lähetetty commitattavaksi. Kuvan tapauksessa README.md tiedostoon on lisätty tekstiä, jota ei vielä ole commitattu. 

![Screenshot_119](https://user-images.githubusercontent.com/82207948/115477869-928fa100-a24d-11eb-9fd1-c7046c262f86.png)

Komento **``git blame``** antaa tuloksen, jossa näkyy kuka on tehnyt tutkittavaan tiedostoon muutoksia ja milloin. Komennolla voidaan myös ilmeisesti saadan näkyviin tiedoston sisäiset muutokset, mutta se on helpompi toteuttaa **``git log --patch-with-stat``** komennolla.

![Screenshot_134](https://user-images.githubusercontent.com/82207948/115478389-b2739480-a24e-11eb-95f3-06f5a8db6766.png)

<h2> Tehtävä E </h2>

Tehtässä oli tavoitteen kokeilla **``git reset --hard``** komentoa. Komento poistaa tehdyt muutokset, jos niitä ei ole vielä commitattu ja palauttaa esim. tekstitiedoston vanhaan tilaan ennen muutoksia. Itse en ole tätä komentoa käyttänyt. Se olisi kyllä ollut tarpeellinen pari päivää aikaisemmin, kun tein vapaa ajan projektiin muutoksia, mutta olisin loppujen lopuksi halunnut palauttaa muutokset. Käyttis kamaa!

<h2> Tehtävä F </h2>

Tehtävässä oli tavoitteena asentaa jokin ohjelma, ja luoda moduuli Saltilla, joka automaattisesti asentaa kyseisen ohjelman ja konfiguroi sen. Päätin asentaa Lynx nimisen verkkoselaimen, joka toimii terminaalissa. Ohjelma vaikutti todella mielenkiintoiselta, sillä en ole edes osannut ajatellä että verkkosivuja voisi selata terminaalista. 

Aluksi asennetaan Lynx manuaalisesti komennoilla **``sudo apt-get update``** ja **``sudo apt-get install Lynx``**. Tämän jälkeen testasin ohjelmaa, ja se toimi hyvin, mutta huomasin että evästeet tuli hyväksyä manuaalisesti, joten päätin asetustiedostoon asettaa säännöt, jotka hyväksyvät ne automaattisesti.

Navigoidaan polkuun **``/etc/lynx``**, jossa oletin Lynxin asetustiedostojen olevan. Kansiosta löytyy **``lynx.cfg``** tiedosto, jota muokkaamme komennolla **``sudoedit lynx.cfg``**. Asetuksiin lisätään seuraavat muutokset. **``FORCE_SSL_COOKIES_SECURE:TRUE``**, **``SET_COOKIES:TRUE``**, **``ACCEPT_ALL_COOKIES:TRUE``**. Nyt Lynx ei kysy käyttäjältä hyväksytäänkö evästeet. Ei ehkä fiksua, mutta helppoa. Tämän jälkeen kopioidaan asetustiedosto talteen komennolla **``sudo cp lynx.cfg /srv/salt/``**. Nyt meillä on asetustiedosto, jota Salt voi käyttää moduulissa. Siirrytään **``/srv/salt``** polkuun. Luodaan sinne uusi kansio moduulille komennolla **``sudo mkdir Lynx``**. Sen jälkeen siirretään asetustiedosto sinne komennolla **``sudo mv lynx.cfg Lynx``**. Nyt voimme siirtyä luomaamme Lynx kansioon ja tehdä sinne tila Saltille komennolla **``sudoedit init.sls``**. Tilaan kirjoitamme komennot, joilla saamme Lynxin asennettua ja asetustiedostot muutettua haluamaamme muotoon. Alla olevassa kuvassa näkyy luomani tilan asetukset.

![Screenshot_137](https://user-images.githubusercontent.com/82207948/115515921-46b11c00-a28e-11eb-80e1-9b16f0158af9.png)


Tilan asetukset kannattaa luoda yksittäin, sillä itselläni tuli virheitä muotoilun ja välien kanssa, kun yritin luoda tilan kerralla. Lopuksi päädyin luomaan ja testaamaan kaikkia tilan osia yksi kerrallaan, jotta löysin virheet. 

Tilan luomisen jälkeen voimme komennolla **``sudo apt-get purge Lynx``** Poistaa asentamamme Lynx ohjelman ja koettaa asentaa sen Saltilla luomallamme moduulilla. Moduulin voimme ajaa komennolla **``sudo salt '*' state.apply Lynx``**. Jos tilan ajaminen onnistui, tulisi Succeeded kohdassa lukea Succeeded 2 (changed=2). 

![Screenshot_138](https://user-images.githubusercontent.com/82207948/115517137-7f9dc080-a28f-11eb-88d9-0abaf3f7fd0c.png)

Komennolla **``lynx wikipedia.org``** voimme testata myös asentuiko Lynx ja onko asetustiedosto oikeasti toiminnassa. Lynxin tulisi avata wikipedian pääsivu ja selaimen ei pitäisi kysyä evästeille lupaa, vaan sivun alhaalla ladatessa lukee Always allowing from domain 'wikipedia.org' 

<h2> Lähteet </h2>

https://git-scm.com/docs

https://www.atlassian.com/git/tutorials

https://pc-freak.net/blog/how-to-permanently-enable-cookies-in-lynx-text-browser-disable-accept-cookies-prompt-in-lynx-console-browser/

http://terokarvinen.com/2018/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/ (Käytin muistutinvirkistyksenä ja apuna tilan luomisessa)

