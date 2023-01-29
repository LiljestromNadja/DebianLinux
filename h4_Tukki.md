# h4_Tukki  



### Tehtävä: x)

Lue ja tiivistä [YCombinator Hacker News -sivustolta, vapaavalintainen artikkeli kommentteineen Linuxin komentokehotteesta](https://hn.algolia.com/?dateEnd=1643270199&dateRange=custom&dateStart=1547942400&page=0&prefix=false&query=command%20line&sort=byPopularity&type=story)  

Luin tehtävää varten artikkelin [“Multitasking from the Linux Command Line + Process Prioritization”]https://www.forbes.com/sites/jasonevangelho/2020/12/22/heres-the-true-reason-linux-users-love-the-command-line/

Artikkelissa käsiteltiin prosessien pysäyttämistä, käynnissä olevien prosessien siirtämistä taustalle, prosessien lopettamista sekä prosessien priorisointia. 

Jutussa esitellyistä toimenpiteistä omalle komentorivilleni pääsi heti kokeiluun prosessien pysäyttäminen ja jatkaminen.Tämä on kätevää, jos esimerkiksi tekstieditorin ollessa auki täytyy tarkastaa vaikkapa muistiinpanoja toisesta tiedostosta. “CTRL+Z” komennolla saa tehtävän, kuten tämän tekstieditorin, “stop-tilaan” siksi aikaa kun selaa toista tiedostoa. Tehtävän pysäytys toimii samankaltaisesti kuin vaihtaisi graafisessa käyttöliittymässä ikkunasta toiseen. 
Prosesseja saa toki useampia pysäytettyä ja ne saavat oman “työnumeronsa”, eli kun kyseiseen keskeytettyyn prosessiin haluaa takaisin, se hoituu komentoriviltä komennolla “fg %tehtavanNumero”. Mikäli tehtäviä on “jäähyllä useampi”, listauksen pysäytetyistä tehtävistä saa kirjoittamalla komentoriville “jobs”. 

Listasin tähän jutussa mainittuja komentoja: 

CTRL + Z = stop

fg %tehtavanNumero = jatka

jobs - listaa stop-tilassa olevat 

bg %tehtavanNumero = siirtää prosessin taustalle

nano teeusitiedosto.md & = aloittaa prosessin taustalla, eli ei tässä tapauksessa edes avaa tekstieditoria käyttäjän nähtäväksi

sudo kill %tehtavanNumero = lopettaa tehtävän 


prosessin lopettaminen(“terminoiminen”)

sudo kill %tehtavaNro 

prosessin lopettaminen “painokkaammin”
sudo kill -9 %tehtavaNro

prosessin lopettaminen prosessi ID:llä (Id näkyy kun uusi prosessi luodaan taustalle)
sudo kill 12345




