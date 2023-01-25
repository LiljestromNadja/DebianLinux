# Lisenssit, Grep ja säännölliset lausekkeet, Pipe

Free Software Definition (FSF), Rise of Open Source, Grep and regular exprenssions, Pipe

## h3_Vapaus [(Kurssi: Linux-palvelimet 2023 alkukevät)](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

### Harjoitukset: 

*Lue ja tiivistä:*  
*FSF: FSF Free Software Definition. https://www.gnu.org/philosophy/free-sw.html.*

*Välimäki 2005: Rise of Open Source: 5 Open Source Licenses as Alternative Governance Mechanisms: 5.1.1 - 5.1.4 (sivu 113 - 121). http://lib.tkk.fi/Diss/2005/isbn9529187793/isbn9529187793.pdf.*    
<!--<br></br>-->

#### Vapaan ohjelmiston/ohjelmakoodin määritelmä:  
"Free software" -käsitteessä ei ole kyse ilmaisesta hinnasta, vaan yksittäisen käyttäjän vapaudesta sekä yhteisöllisyydestä. 
Käyttäjillä on vapaus tutkia ja käyttää, muuttaa ja parannella, kopioida ja jakaa näitä ohjelmistoja ja ohjelmistojen koodeja.  
Myöskään rahan tienaaminen ei ole kiellettyä.

##### Free Software Definition - 4 tekijää, jotka määrittelevät "Vapaan": 
0. Suorita. Vapaus käyttää ohjelmistoa ilman rajoitteita. 
1. Tutki. Vapaus tutkia ohjelmistoa ja muovata sitä toimimaan haluamallaan tavalla.
2. Levitä. Vapaus levittää ohjelmistoa muille ilman rajoituksia. 
3. Kehitä. Vapaus jakaa muokattua versiota eteepäin. Antaa myös muille mahdollisuuden kehittää muovaamaasi ja jakamaasi ohjelmistoa.
Pääsy lähdekoodiin on tämän edellytys. 

Lähde: https://www.gnu.org/philosophy/free-sw.html.


*a) Kolmen ohjelman lisenssit. Tarkastele kolmen edellisessä harjoituksessa asentamasi ohjelman lisenssejä. Selvitä kustakin ohjelmasta:  
-Mitä lisenssiä kyseinen ohjelma käyttää?  
-Mistä päättelit lisenssin?  
-Onko kyseessä vapaa lisenssi?  
-Mitkä ovat tämän lisenssin tärkeimmät oikeusvaikutukset?  
-Jääkö tämän ohjelman lisenssoinnista jotain avoimia kysymyksiä tai epäselvyyttä?*    

**Asentamani ohjelmat olivat Asciijump, Micro ja Cowsay.**   

**Asciijump:** v 1.0.2beta. Gnu general public license v2. Vapaa lisenssi.  

Selvitin ohjelman version komennolla $ ohjelmanNimi --version:  

    $ asciijump --version
  
Versiotiedoissa näkyivät myös lisenssitiedot  

**Micro:** Version 2.0.8. En löytänyt lisenssistä tietoa.

**Cowsay:** Version unknown. 	Artistic License / GNU General Public License, löytyi Googlailemalla. Vapaa lisenssi.

**Gnu General Public License tärkeimmät oikeusvaikutukset:**  

Gnu General Public License on vapaa copyleft-lisenssi ohjelmistoille ja muille teoksille.  
Lisenssi antaa "vapaat kädet" käyttää ohjelmistoja ja ohjelmakoodia, noudattaen "Free Software" -periaatteita. Käyttäjällä on siis vapaus käyttää, tutkia, muokata ja levittää ohjelmistoa ja ohjelmistokoodia. Tämä vapaus siirtyy myös ohjelmiston mukana, eli kun ohjelmistoa tai ohjelmakoodia muokataan, lähdekoodin täytyy pysyä avoimena. Ohjelmistoa tai ohjelmakoodia saa käyttää myös kaupallisesti.  

Lähde: https://www.gnu.org/licenses/gpl-3.0.html  



*b) Säännöllistä. Poimi tekstitiedostosta tietoa grep-komennolla käyttäen säännöllisiä lausekkeita (regexp, regular expressions).*  

Etsitään "newfile.md" -tiedostosta merkkijonoa "linux" merkkien koosta välittämättä ja tulostetaan rivit joilla kyseinen merkkijono on:  

        $ cat newfile.md | grep -i linux
        
![Näyttökuva (135)](https://user-images.githubusercontent.com/118609353/214702315-947f3ada-4c9b-4667-b5b3-fdbad49bd0e4.png)  

![Näyttökuva (136)](https://user-images.githubusercontent.com/118609353/214702769-dc656355-98c9-4509-b79b-7f6da6a4a0eb.png)  

Etsitään "newfile" -tiedostosta sanat jotka alkavat merkillä "t", välissä kaksi merkkiä ja päättyvät merkkiin "t":  

        $ cat newfile.md | grep -P 't..t'  
        
![Näyttökuva (138)](https://user-images.githubusercontent.com/118609353/214705560-e09a3fb8-cbe4-4589-b1b8-899d037ae6f3.png)
![Näyttökuva (137)](https://user-images.githubusercontent.com/118609353/214705731-ebca87bf-f0ea-4a40-9aa0-e41c417b6617.png)

        $ cat newfile.md | grep -P '...dow-' --color
        

![Näyttökuva (139)](https://user-images.githubusercontent.com/118609353/214706870-8810c638-107f-48f7-9a8d-92b895445cb3.png)


*c) Pipe. Näytä esimerkki putkista (pipes).*  

Laitetaan lehmä sanomaan "putkeen meni" tiedostossa kotitehtava.md:  

        $ cowsay putkeen meni > kotitehtava.md
        
![Näyttökuva (131)](https://user-images.githubusercontent.com/118609353/214697389-29762f73-1018-4d9a-8e94-b623047e73ed.png)  

Laitetaan lehmä sanomaan, mitä tiedostossa "jotainsanottavaalehmalle" on:  

        $ cowsay < jotainsanottavaalehmalle
        
![Näyttökuva (132)](https://user-images.githubusercontent.com/118609353/214698435-a4cf0eae-52c8-40e1-83ed-03c0b4defd3b.png)  

Sama toisella komennolla, nyt lehmä kertoo mitä "newfile.md" pitää sisällään:  

        $ cat newfile.md | cowsay
 
![Näyttökuva (133)](https://user-images.githubusercontent.com/118609353/214699583-fd17b64a-aa53-437b-9195-3a2128ebcd11.png)  




#### Lähteet ja materiaalit:  
FSF: FSF Free Software Definition.https://www.gnu.org/philosophy/free-sw.html.  

Välimäki 2005: Rise of Open Source: 5 Open Source Licenses as Alternative Governance Mechanisms: 5.1.1 - 5.1.4 (sivu 113 - 121).http://lib.tkk.fi/Diss/2005/isbn9529187793/isbn9529187793.pdf.  

Karvinen, Tero. Linux Palvelimet 2023 alkukevät.https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
