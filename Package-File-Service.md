<h1> Package-File-Service tehtävät </h1>

<h2> Tehtävä A </h2>

Tehtävässä oli tavoitteena asentaa demoni linux järjestelmälle ensin käsin ja sitten automatisoiden saltilla. Päätin asentaa Apache demonin.  

Asennus aloitetaan päivittämällä lista repositoreista komennolla ``sudo apt-get update``. Tämän jälkeen voidaan asentaa Apache komennolla ``sudo apt-get install apache2``. Apachen asennuksen jälkeen siirrytään apachen porttien konfigurointi tiedostolle komennolla ``cd /etc/apache2``. Tämän jälkeen voidaan käyttää komentoa ``sudoedit ports.conf``, jolla voidaan muuttaa porttiasetuksia. Asetetaan apache kuuntelemaan porttia 999 ja tallenetaan muutokset. Tämän jälkeen
