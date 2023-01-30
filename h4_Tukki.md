# h4_Tukki  



### Tehtävä: x)

Lue ja tiivistä [YCombinator Hacker News -sivustolta vapaavalintainen artikkeli kommentteineen Linuxin komentokehotteesta.](https://hn.algolia.com/?dateEnd=1643270199&dateRange=custom&dateStart=1547942400&page=0&prefix=false&query=command%20line&sort=byPopularity&type=story)  

Luin tehtävää varten artikkelin [“Multitasking from the Linux Command Line + Process Prioritization”.](https://www.forbes.com/sites/jasonevangelho/2020/12/22/heres-the-true-reason-linux-users-love-the-command-line/)  

Artikkelissa käsiteltiin prosessien pysäyttämistä, käynnissä olevien prosessien siirtämistä taustalle, prosessien lopettamista sekä prosessien priorisointia. 

Jutussa esitellyistä toimenpiteistä omalle komentorivilleni pääsi heti kokeiluun prosessien pysäyttäminen ja jatkaminen. Tämä on kätevää, jos esimerkiksi tekstieditorin ollessa auki täytyy tarkastaa vaikkapa muistiinpanoja toisesta tiedostosta. **“CTRL+Z”** -komennolla saa tehtävän, kuten tämän tekstieditorin, “pause-tilaan” siksi aikaa kun selaa toista tiedostoa. Tehtävän pysäytys toimii idealtaan samankaltaisesti kuin vaihtaisi graafisessa käyttöliittymässä ikkunasta toiseen. 
Prosesseja saa toki useampia pysäytettyä ja ne saavat oman “työnumeronsa”, eli kun kyseiseen keskeytettyyn prosessiin haluaa takaisin, se hoituu komentoriviltä komennolla **“fg %tehtavanNumero”**. Mikäli tehtäviä on "jäähyllä" useampi, listauksen pysäytetyistä tehtävistä saa kirjoittamalla komentoriville **"jobs"**.  

Listasin tähän jutussa mainittuja komentoja:  

Tehtävän/prosessin pysäyttäminen:  

    CTRL + Z
    
Tehtävän jatkaminen:  

    $ fg %tehtavanNumero
    
Listaa pysäytetyt: 

    $ jobs
    
Tehtävän siirtäminen taustalle:  

    bg %tehtavanNumero

Tehtävän aloittaminen taustalla (eli tässä tapauksessa tekstieditori ei käynnistyessään avaudu käyttäjän nähtäväksi):  

    nano teeusitiedosto.md &  

Prosessin lopettaminen(“terminoiminen”):  

    sudo kill %tehtavaNro  

Prosessin lopettaminen painokkaammin:  

    sudo kill -9 %tehtavaNro

Prosessin lopettaminen prosessi ID:llä (ID näkyy kun uusi prosessi luodaan taustalle):  

    sudo kill 12345  
    
    
### Tehtävä: a) Tukki. Analysoi yksi esimerkkirivi kustakin näistä lokeista

#### /var/log/syslog - yleisloki, tänne kaikki joilla ei ole omaa lokia  

![Näyttökuva (150)](https://user-images.githubusercontent.com/118609353/215365164-8ed5a4c1-ae17-45d0-aa6a-33b453f7aab8.png)

Tähän on kirjattu Apachen käynnistys. 
#### /var/log/auth.log - kirjatumiset, sudo:n käyttö  

![Näyttökuva (149)](https://user-images.githubusercontent.com/118609353/215364632-6164cef1-1851-4b64-9bdd-1845f43f2197.png)  
Tämä kirjaus tuli kun käytin sudo-komentoa avatakseni /var/log/auth.log -tiedoston. 

#### /var/log/apache2/access.log - onnistunut surffailu 2xx, 3xx; käyttäjän virheet 4xx client error    

![Näyttökuva (148)](https://user-images.githubusercontent.com/118609353/215363557-10dad161-3d2a-4ee1-95d6-8798c31c09ac.png)  

**Onnistunut surffailu:  
127.0.0.1 - - [30/Jan/2023:01:49:11 +0200] "GET / HTTP/1.1" 200 3380 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"**  

Riviltä löytyvät tiedot:   
    -locahostin IP-osoite,   
    -päiväys, kello ja aikavyöhyke (oikeat)  
    -mitä tehdään: "GET"  
    -200 = onnistunut surffailu  
    -selain  
    -käyttöjärjestelmä    

**Error:  
127.0.0.1 - - [30/Jan/2023:01:49:28 +0200] "GET /kukkkkuuuu HTTP/1.1" 404 488 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:102.0) Gecko/20100101 Firefox/102.0"**    

Riviltä löytyvät tiedot:     
    -locahostin IP-osoite,   
    -päiväys, kello ja aikavyöhyke (oikeat)  
    -mitä tehdään: "GET"  
    -400 = client error, tässä tapauksessa sivua ei ole olemassa (localhost/kukkkkuuuu)   
    -selain  
    -käyttöjärjestelmä  



**/var/log/apache2/error.log - apachen omat virheet, 5xx server error**  

### Tehtävä: b) Aiheuta. Aiheuta lokiin kaksi eri tapahtumaa: yksi esimerkki onnistuneesta ja yksi esimerkki epäonnistuneesta tai kielletystä toimenpiteestä. Analysoi rivit yksityiskohtaisesti.  

    
    
    
#### Lähteet ja materiaalit:  

[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

[Jean, Chris. Multitasking from the Linux Command Line + Process Prioritization](https://chrisjean.com/multitasking-from-the-linux-command-line-plus-process-prioritization/)  






