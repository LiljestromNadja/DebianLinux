
# h8_Say_my_name

**Tehtävänanto**  
a) Vuokraa domainnimi ja aseta se osoittamaan virtuaalipalvelimeesi.  
b) Tutki oman nimesi tietoja 'host' ja 'dig' -komennoilla. Analysoi tulokset.  


<!--**Vinkit:**  
Julkisia nimiä vuokrataan:
NameCheap
Gandi.
Harjoittelua varten voit kokeilla myös http://www.dot.tk/ tai vastaavaa kokonaan ilmaista palvelua (ei tärkeille nimille).
Jos et jostain syystä halua vuokrata oikeaa nimeä, voit vaihtoehtotehtävänä kokeilla nimipalvelua tai sen simulointia hosts-tiedoston avulla. Tällöin voit tehdä nimipalvelutietojen analysoinnin mistä vain julkisessa käytössä olevasta nimestä. Suosittelen kuitenkin oikean nimen vuokraamista ja asettamista.-->



[Lähde](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)   

---
## Domain  

Tehtävää varten vuokrasin [nadjaliljestrom.website](http://www.nadjaliljestrom.website/) -nimen [Gandilta](https://www.gandi.net/en-US).  Käytin harjoituksessa aikaisemmin luomani [virtuaalipalvelimen](https://github.com/LiljestromNadja/DebianLinux/blob/main/h7_Based-Real_Internet.md#a-vuokraa-oma-virtuaalipalvelin-haluamaltasi-palveluntarjoajalta-vaihtoehtona-voit-k%C3%A4ytt%C3%A4%C3%A4-ilmaista-kokeilujaksoa-github-education-krediittej%C3%A4-tai-jos-mik%C3%A4%C3%A4n-muu-ei-onnistu-voit-kokeilla-vagrantia-paikallisesti) IP-osoitetta.  

---
## Tehtävät  


---

### a) Vuokraa domainnimi ja aseta se osoittamaan virtuaalipalvelimeesi.    

**Palveluntarjoaja:** [Gandi](https://www.gandi.net/en-US)  
**Domain:** [nadjaliljestrom.website](http://www.nadjaliljestrom.website/)  

Aluksi etsin itselleni sopivan domainin palveluntarjoajan hakutoiminnolla, maksoin sen ja loin käyttäjätunnuksen palveluun.  
<br></br>
![Näyttökuva (226)](https://user-images.githubusercontent.com/118609353/218337909-4548ad25-effc-433a-b92a-633859aa1f4d.png)


**Domainin asetusten muokkaaminen:**  

Domain -> (Advanced Wiew) -> Manage -> DNS Records  
<br></br>

![Näyttökuva (217)](https://user-images.githubusercontent.com/118609353/218333955-a1e2b82a-8b28-4174-8c00-7f145aebe025.png)

![Näyttökuva (218) alku](https://user-images.githubusercontent.com/118609353/218334788-416747ad-d4e1-42fe-8765-0f4c80d372c3.png)

Otin kaikki alkuperäiset määritykset pois ja lisäsin omat: 


    @ 10800 IN A 46.101.234.74 (nadjaliljestrom.website)
    kokeilu 10800 IN A 46.101.234.74 (kokeilu.nadjaliljestrom.website)
    toinenip 10800 IN A 104.248.253.250 (toinenip.nadjaliljestrom.website)
    www 10800 IN A 46.101.234.74 (www.nadjaliljestrom.website)

Lisäksi tallentaessa ilmestyi automaattisesti vielä tämä:  

    @ 86400 IN SOA ns1.gandi.net. hostmaster.gandi.net. 1676074586 10800 3600 604800 10800
    

![Näyttökuva (220)](https://user-images.githubusercontent.com/118609353/218335099-5a6eca25-b9e1-4f43-8cd9-43c2ef3852c6.png)  
<br></br>
Melko nopeasti sivut näkyivät selaimella:  



![Näyttökuva (222)](https://user-images.githubusercontent.com/118609353/218335537-8b9e09f8-1d25-4241-a168-ebbbc40f25a2.png)




---

### b) Tutki oman nimesi tietoja 'host' ja 'dig' -komennoilla. Analysoi tulokset.   

#### Dig
Lähdin kokeilemaan dig-nimipalvelintyökalua:  

    nadja@debbiedebian:~$ dig NS nadjaliljestrom.website
    bash: dig: command not found

Eli siis asennushommiin: 

    nadja@debbiedebian:~$ sudo apt-get install -y dnsutils  
    
![Näyttökuva (224)](https://user-images.githubusercontent.com/118609353/218336591-07c34d25-8033-4a8c-89e7-05c8e6f817e8.png)


Sitten uudestaan:  

    nadja@debbiedebian:~$ dig NS nadjaliljestrom.website

![Näyttökuva (225)](https://user-images.githubusercontent.com/118609353/218336988-ba1716fc-6aa4-431b-929a-eb57ba46546c.png)

**'dig NS'** vastaa kysymykseen mikä nimipalvelin osoitteella on. Tuloksena näkyy vastaus, jossa esimerkiksi ANSWER SECTION:sta näkyy nimipalvelin. Lisäksi tuloksessa näkyy mm. kauan vastauksen saamiseen meni (Query time: 28 msec), milloin kysely tehtiin (WHEN: Sun Feb 12 23:02:24 EET 2023), vastaanotetun viestin(?) koko(MSG SIZE  rcvd: 129).

<!-- 
dig A - Mihin IPv4-osoitteeseen url-osoite osoittaa?
fig AAAA - Mihin IPv6-osoitteeseen url-osoite osoittaa?
dig -x 82.118.208.5 - Mikä on IP-osoitteen 82.118.208.5 reverse-osoite eli hostname?

-->


---

#### Host

Kokeilin host -komentoa:  

    nadja@debbiedebian:~$ host nadjaliljestrom.website

![Näyttökuva (223) host komento](https://user-images.githubusercontent.com/118609353/218337805-09f416a3-06bf-4570-a6a9-3b302cbe48a5.png)



Komentoa käyttämällä sain IPv4-osoitteen johon kyseinen URL-osoite on yhdistetty. 

---





#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

[Gandi.net](https://www.gandi.net/en-US)  

[Linux.fi/wiki/Dig](https://www.linux.fi/wiki/Dig)

---











