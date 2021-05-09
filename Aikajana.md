<h1> Aikajana </h1>

<h2> Tehtävä A </h2>

Tehtävässä A oli tarkoituksena asentaa 10 ohjelmaa saltilla orjille. Tein tilalle oman kansion ja sen sisälle **init.sls** tiedoston, johon laitoin ohjelmat, joita halusin asentaa. Ohjelmat asensin **``pkg.installed``** komennolla.

Alla näkyy ohjelmat, joita salt tila asensi.

![Screenshot_177](https://user-images.githubusercontent.com/82207948/117585372-c8bc9400-b11a-11eb-8dd9-8566cb1f3c79.png)

Kaikki ohjelmat asentuivat hyvin ja ne toimivat oikein kun tila ajettiin.

<h2> Tehtävä B </h2>

Tehtävässä B oli tarkoituksen oli asentaa Microsoftin pakettivarasto ja sieltä Visual Studio Code. Minulla ei ollut aikaisempaa kokemusta tällaisesta tehtävästä, joten etsin netistä ohjeet, joiden perusteella tehtävän tein.

Linkki ohjeeseen: https://linuxize.com/post/how-to-install-visual-studio-code-on-debian-10/

Aluksi tuli asentaa riippuvuus alla oleville komennoilla, jotta Microsoftin repositorio toimisi.  

**``sudo apt update``**

**``sudo apt install software-properties-common apt-transport-https curl``**

Seuraavaksi tuli lisätä Microsoftin GPG avain, jotta luottosuhde voidaan muodostaa. Avain lisättiin alla olevalla komennolla. 

**``curl -sSL https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -``**

Tämän jälkeen täytyy lisätä repositorio Visual Studio Codelle alla olevalla komennolla.

**``sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"``**

Sen jälkeen voidaan päivittää repositoriot komennolla **``sudo apt update``** ja asentaa Visual Studio Code komennolla **``sudo apt install code``**

Asennuksen valmistuttua testasin että ohjelma toimii oikein komennolla **``code``**. Tämä käynnistää Visual Studio Code ohjelman, jos se asentui oikein. Minulla ohjelma käynnistyi, joten asennus onnistui. Virtuaalikone ei kuitenkaan jaksanut ohjelmaa pyörittää, kun yritin ohjelmaa hieman käyttää. Koko asennus jäätyi ja jouduin käynnistämään sen uudelleen. 

<h2> Tehtävä C </h2>

Tehtävässä C oli tarkoituksena käyttää komentoa **``cd /etc/; sudo find -printf '%T+ %p\n'|sort|tail``** ja tutkia sitä. Alla on tuloste, kun kokeilin komentoa polkuun /usr/local/bin. Olin tehnyt sinne muutoksia aikaisemmissa tehtävissä.

![Screenshot_178](https://user-images.githubusercontent.com/82207948/117586204-54382400-b11f-11eb-8de4-e1c0bb3d04a7.png)

Komennossa **``cd /usr/local/bin; sudo find -printf '%T+ %p\n'|sort|tail``** **-printf** tulostaa tuloksen terminaaliin, **%T+** kertoo komennolle miltä ajalta muutosta etsitään, **%p** antaa muutetun tiedoston nimen, \n laittaa listan kohdat uusille riveille, sort lajittelee rivit ja tail antaa vain 10 viimeisintä tulosta. 

Viimeiseen kohtaan en keksinyt komentoa, joka olisi muuttanut yhteisiä asetustiedostoja. Koetin poistaa muutamia eri ohjelmia, mutta en saanut **/etc** polussa näkymäään muutoksia. 



<h1> Lähteet </h1>

https://linuxize.com/post/how-to-install-visual-studio-code-on-debian-10/

https://docs.microsoft.com/en-us/windows-server/administration/linux-package-repository-for-microsoft-software
