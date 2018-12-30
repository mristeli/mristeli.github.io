---
layout: default
---

## Komentorivikurssi

Tällä sivulla esittelen, mikä on Komentorivikurssi ([Commandline-course](https://courses.helsinki.fi/en/kik-lg218/126710126)), ja kerron, mitä opin kurssin aikana, jaoteltuna viikkokohtaisesiin osioihin. Lopuksi kerron kurssin loppytyöprojektista.

Komentorivikurssi on Helsingin yliopiston kurssi, jossa tutustutaan Unix-järjestelmään ja erityisesti sen tarjoamiin "standardityökaluihin". Kysemyksessä ei ole ihan puhtaasti standardista, koska usein käskyjen täsmällinen toiminta saattaa erota ympäristöjen välillä. Yhtä kaikki nämä työkalut tarjoavat kielentutkijoille valmiiksi monia keinoja hakea ja kostaa sekä analysoida tekstiaineistoja. Komentorivi on myös hyvin tehokas ympäristö automatisoida monenlaisia toimia.

### Viikko 1: Unixin peruskomentoja

Tämän viikon tehtävät unohdin palauttaa ajoissa, vaikka ne lopulta teinkin. Tämän viikon tehtävissä tutustuttiin muutamiin peruskomentoihin, jotka löytyy lähes aina Unix-ympäristöstä. Näitä ovat esimerkiksi

1. 'cat' --- tekstitiedoston sisällön tulostamiseen käytettävä ohjelma. Tarvitaan usein osana laajempia peräkkäisistä käskyistä koostuvia komentoja ajaessa, kun esimerkiksi halutaan analysoida tiedoston sisältöä vaiheittain.
2. 'mv', 'cp' --- tiedostojen uudelleen nimeämiseen ja kopiointiin käytettäviä komentoja.
3. 'wget' --- komento, jolla voi hakea tiedoston hakeminen webosoitteesta, toinen yleinen ohjelma tähän on 'curl'.
4. 'man' --- komento, jolla voi hakea avata käskyn käyttöohjeeen.
5. 'nano' --- tekstieditorilla, jolla voi siis muokata oikeata tekstitiedostoa. 

Lisäksi tehtävissä tutustuttiin siihen, mitä tiedostot ovat.

### Viikko 2: Prosessit ja tiedostojärjestelmä

Toisen viikon tehtävissä jatkettiin tutustumista Unix-järjestelmään. Erityisesti tutkittiin tiedostojen käyttöoikeuksia ja tiedostojärjestelmää, sekä komentotulkki-istunnon toimintaa paikallisesti tai secure shell -yhteyden yli. Olennaisia komentoja oli

1. 'ln' --- tällä käskyllä luodaan linkkejä, symbolisia tai kovia, tiedostojärjestelmään. Yhdelle tiedostolle voi siten antaa monta nimeä.
2. 'chmod' --- tiedoston omistaja tai 'root'-käyttäjä voi muokata tällä käskyllä tiedostokäyttöoikeuksia, jotka kertovat miten ko. tiedosto on muiden käyttäjien käytettävissä. 
3. 'sudo' --- komennolla käyttäjä voi suorittaa käskyjä 'root'-käyttäjänä, mikäli hänellä on tähän oikeus.
4. 'kill' --- komennolla käyttäjä voi lopettaa oman prosessinsa, jos tietää sen prosessi-id:n.

Lisäksi tällä viikolla opittiin Unixin prosessihierarkiasta. Kaikki Unix-prosessit paitsi 'init' -- järjestelmän käynnistyessä ensimmäisenä syntyvä prosessi -- ovat jonkun toisen prosessin lapsiprosesseja.

### Viikko 3: Korpustutkimusta perustyökaluilla

Kolmannen viikon tehtävissä sovellettiin Unix-työkaluja yksinkertaisen korpustutkimuksen tekemiseen. Komentorivityökalulla voi helposti analysoida tekstitiedostoon talletettua teosta. Kohteena oli Maurice Maeterlinckin romaani "Life of a bee". Romaani tuli hakea Project Gutenberg -sivustolta, jossa on vapaasti haettavissa teoksia, joiden tekijänoikeudet ovat jo vanhentuneet.  Ensivaiheessa tekstistä tuotettiin frekvenssilista, lista, jossa on lueteltuna kaikki tekstissä esiintyvät eri sanamuodot ja kuinka monta kertaa mikäkin sana muoto esiintyy. Frekvenssilistan luominen konentorivillä on näinkin yksinkertaista, kun lähde teksti on tiedostossa life_of_bee.txt:


```
cat life_of_bee.txt | tr -s '\n\t\r ' '\n' | tr -dc "A-Za-z0-9'\n" | sort | uniq -c | sort -nr > life_of_bee.freq
```

Lisäksi luotiin tiedosto, jossa tekstin jokainen lause on erotettu omalle rivilleen.

### Viikko 4: komentoriviskriptaus

Neljännen viikon tehtävissä opeteltiin komentoriviskriptien tekemistä. Skriptit ovat tekstitiedostoja, jotka sisältävät kutsuja ohjelmiin sekä skriptiä suorittavan komentotulkin toimintaa ohjaamia käskyjä, joiden avulla voidaan automatisoida toimia ja kohdistaa käskyjä esimerkiksi kaikkiin hakemiston tiedostoihin. Olennaisia opittuja asioita olivat 'bash'-skriptien kontrollikäskyt. Esimerkiksi 'loopdir.sh':ssa luetaan 'ls -a'-käskyn tuloste ja tehdään jokaiselle tulosteriville jotain. Tämä iterointi skriptataan seuraavasti.
```
files=`ls -a`
for name in $files
do
	# tee jotain
done
```

### Viikko 5: ohjelmistojen asennus- ja kääntämisympäristöt

Viidennen viikon tehtävissä tutustuttiin yleiskäyttöiseen make-komentoon, pakettien hallintaan ja python-ympäristön pip-hallintatyökaluun. Taulukossa on kuvattu näiden käyttöympäristöt.

|Työkalu|Ympäristö|Käyttö|
|:------|--------:|------:|
|'make' |Yleinen  |Tiedostojen luonti toisten tiedostojen perusteella
|'brew' |Mac OS X |Avoimen lähdekoodien ohjelmistojen asentamiseen käytetty sovellus
|'yum'	|Linux 	  |Yksi yleisimmistä pakettienhallintaohjelmistoista Linux-maailmassa
|'pip'	|Python	  |Python-laajennuksien asennukseen käytettävä ohjelmisto

Mielenkiintoisin näistä oli tässä yhdeydessä 'make'. [M]ake-työkalulla voidaan luota tiedostoja toisista tiedostoista määrittämällä tiedostojen väliset riippuvuudet ja niiden luontiin käytettävät käskyt Makefile-tiedostoon. Makefile-tiedostoon voidaan myös määrittää erilaisia kohdesettejä; kaikkia tulostiedostoja ei ole pakko luoda kerralla. Osana kotitehtävää piti muokata Makefileä luomaan uusi tilasto kaikista kirjoista ja lisätä lähdelistaan yksi kirja.  

### Viikko 6: Java ja versionhallinta

Viimeisenä kohtitehtävänä tutustuttiin muutamaan java-kääntäjän virheilmoitukseen ja git-versionhallintajärjestelmään. Git on ns. hajautettu versionhallintajärjestelmä, mikä tarkoittaa sitä, että git-projektin jokainen työkopio on itse asiassa itsenäinen versionhallintatietokanta. 

Versionhallintaharjoituksena luotiin git-repositorio, johon tuotiin edellisen viikon make-harjoituksen tiedostot. Tähän haluttiin tehdä pieni muutos, joten gitin käyttöharjoituksena luotiin sitä varten oma kehityshaara, sitten tehtiin pieni muutos yhteen skriptiin ja Makefileen. Samalla opeteltiin myös peruuttamaan jo talletettu muutos.

Samalla poistettiin kehityshaara, johon muutokset oli alunperin tehty. Ja luotiin siis tunnukset Github-sivustolle, jossa kuka tahansa voi ylläpitää omien projektiensa versionhallintarepositorioita ja tehtävän myötä syntyi Github-projekti [cmdline-course](https://github.com/mristeli/cmdline-course).


### Lopputyö: Github Pages -julkaisualusta ja raportti

Tämä lopputyö on kirjoitettu Github Pages -julkaisualustalle. Github Pages -on Jekyll-ohjelmistoa hyödyntävä sivusto, jolla julkaistaan automaattisesti Github-käyttäjien repositoriot, joiden nimi on muotoa KÄYTTÄJÄNIMI.github.io. Sivusto tulee vastaavasti tarjolle osoitteeseen __https://KÄYTTÄJÄNIMI.github.io__. 

Jekyll on Ruby-ohjelmointikielellä tehdy ohjelmisto, jolla voi helposti julkaista staattisista sivuista koostuvia websivustoja. Sivuston lähdekoodina voi käyttää [Markdown-kuvauskieltä](https://daringfireball.net/projects/markdown/), jota käytetään myös esimerkiksi Githubin README-tiedostoissa. 
Kun Githubiin on luotu Github Pages -sivustoa varten repositorio, ja se on kloonattu omalle kehityskoneelle, on omalle koneelle syytä asentaa Jekyll paikallisesti. Tämä tosin oli omassa Mac OS X -ympäristössäni hieman monimutkaista. Kun Jekyll on asennettu, pystyy omaa sivustoa testaamaan helposti. Ajamalla ```bundle exec jekyll serve``` tulee seuraava viesti:
 
![Jekyll-output](/assets/img/sshot.png "Jekyll output")

Omaa sivustoa pääsee siis kokeilemaan avaamalla selaimessa osoitteen **http://127.0.0.1:4000/**. Jekyll reagoi myös sivuston sisältöön tehtyihin muutoksiin automaattisesti, joten aina tekstiä muokatessa riittää, että lataa selainikkunan uudestaan. 

