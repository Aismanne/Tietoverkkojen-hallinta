<h1> Windows </h1>

<h2> Tehtävä A </h2>

Tehtävässä oli tarkoituksena kokeilla Salttia Windowsilla. Päätin koettaa hallita Windows konetta Debian laitteelta. 

Aluksi asensin Saltin Windows koneelle lataamalla sen Saltin omilta sivuilta. Asennusvaiheessa Saltille piti antaa herran IP osoite sekä nimetä Windows orja. Asennuksen jälkeen kokeilin herra koneella komentoa **``sudo salt-key``**. Siellä näkyi nyt Windows kone **Unaccepted keys** kohdassa. Hyväksyin Windows laitteen avainmen ja kokeilin sen jälkeen komentoa **``sudo salt 'Windows' cmd.run 'echo hello'``**. Komento toimi ja Windows kone tulosti hello!. Yllättävän helppoa!

![Screenshot_200](https://user-images.githubusercontent.com/82207948/119275009-633ccd00-bc1b-11eb-97f6-1ddea30079ac.png)

Seuraavaksi päätin kokeilla asentaa jonkin ohjelman Windows koneelle, sillä se olisi muutos jonka voisin nähdä helposti!

Aluksi aloin asentamaan repositoriota herra koneelle, josta se osaisi etsiä ohjelmat. Tämä tapahtui komennolla **``salt-run winrepo.update_git_repos``**. Tämä ei kuitenkaan onnistunut suoraan, sillä vastaukseksi sain että kansioon **``srv/salt/win/repo``** ei ollut oikeuksia. Päättelin että salt ei saa kirjoittaa kansioon, joten jouduin antamaan sille lisäoikeuksia. Tämä tapahtui niin että aluksi lisäsin root.salt:n **``srv/salt/win``** omistajaksi komennolla **``sudo chowm root.salt /srv/salt/win``** Siten annoin kansiolle kirjoitus ja lukuoikeudet kansion omistajalle komennolla **``sudo ug+rwx /srv/salt/win``** 

![Screenshot_201](https://user-images.githubusercontent.com/82207948/119275205-5cfb2080-bc1c-11eb-8721-b6c03792dd01.png)

Tämän jälkeen **``salt-run winrepo.update_git_repos``** komento toimi ja nyt pystyin asentamaan ohjelmia windows orjalle. Kokeilin asentaa firefoxin Windows orjalle komennolla **``sudo salt 'Windows' pkg.install firefox_64``**. Komento toimi ja nyt Windows orjalla oli Firefox ilmestynyt työpöydälle! 

![Screenshot_202](https://user-images.githubusercontent.com/82207948/119275313-f6c2cd80-bc1c-11eb-91b6-7489d3ec4764.png)


<h2> Tehtävä B </h2>

Tehtävässä oli tarkoituksen kertoa omasta moduulista. Itse tein tämän kyseisen tehtävän vasta sen jälkeen kun moduulini oli tehty ja esitetty jo luokalle joten en kokenut että tässä tehtävässä oli enää järkeä.
