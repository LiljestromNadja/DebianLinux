# h6_Based

Tehtävänanto:  

x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)  
[Apache Software Foundation 2023: Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)  
[Apache Software Foundation 2023: Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)  
a) Vaihda Apachelle uusi etusivu. Varmista, että voit muokata sivua normaalilla käyttäjällä (ilman sudoa).  
b) Tee Apachen asetustiedostoon kirjoitusvirhe. Etsi se työkalujen avulla. Vertaa 'apache2ctl configtest' ja virhelokin /var/log/apache2/error.log virheilmoituksia.  
n) Vapaaehtoinen: Tee Apachelle kaksi nimipohjaista palvelua (name based virtual host), foo.example.com ja bar.example.com. Voit simuloida nimipalvelun toimintaa hosts-tiedoston avulla.  


### x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)  

Getting Started  

- Netissä URL-osoite sisältää: 
    - protokollan (http)  
    - palvelimen nimen (www.something.com)  
    - URL-polun (/public_sites/index.html)  
    - mahdollisesti  palvelimelle lähetettävää tietoa (?name=Pentti&ika=12)  
- Yhteys esimerkiksi Internet-selaimesta (client) palvelimeen (esim. Apache) muodostetaan pyynnöllä (request). 
- Palvelin vastaa pyyntöön (response) tunnuksella (esim. 404 client error), joka kertoo onko yhteyden muodostaminen onnistunut vai ei.  
- Mikäli yhteyden muodostamisessa on tapahtunut virhe, virheen tyyppi selviää tästä tunnuksesta (status code).  
- Tapahtumat, esimerkiksi virheet kirjataan lokiin.  
 
- Jotta yhteys voidaan muodostaa, palvelimen nimellä täytyy olla IP-osoite, joka on sen "sijainti" Internetissä.  
- Useampi hostname voi osoittaa samaan IP-osoitteeseen.  
- Useampi IP-osoite voi sijaita samalla palvelinlaitteella.  

- Apache on määritelty yksinkertaisilla tekstitiedostoilla.  
- Näiden asetuksia määrittelevien tiedostojen sisältö on jaettu useampaan pieneen tiedostoon hallinnan helpottamiseksi.  

- Nettisivujen sisältö voidaan jakaa karkeasti staattiseen (esim. html-, kuva- ja css-tiedostot) ja dynaamiseen sisältöön (generoidaan pyyntöä vastaanotettaessa).  

- Järjestelmänvalvojan "arvokkainta omaisuutta" ovat lokitiedostot, erityisesti virheloki. Vianetsintää ilman virhelokia verrataan ajamiseen silmät kiinni.  
- Virhelokin merkinnöistä käy ilmi, missä ja milloin virhe on tapahtunut, sekä mahdollisesti toimet virheen korjaamiseksi. 








**Lähteet**  
[Apache Software Foundation 2023: Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)  
[Apache Software Foundation 2023: Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)  
 

### tehtäväotsikko  

### tehtäväotsikko  


**BOLD**  


<br></br> 



#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  


[Apache Software Foundation 2023: Getting Started](https://httpd.apache.org/docs/2.4/getting-started.html)  
[Apache Software Foundation 2023: Name-based Virtual Host Support](https://httpd.apache.org/docs/current/vhosts/name-based.html)  









