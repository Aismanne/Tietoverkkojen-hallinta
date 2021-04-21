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

Tehtävässä oli tavoitteena asentaa jokin ohjelma, ja luoda moduuli Saltilla, joka automaattisesti asentaa kyseisen ohjelman ja konfiguroi sen. Päätin asentaa Lynx nimisen verkkoselaimen, joka toimii terminaalissa. Ohjelma vaikutti todella mielenkiintoiselta, sillä en ole edes osannut ajatellä että verkkosivuja voisi selata terminaalista :O. 
