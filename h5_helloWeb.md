# h5_helloWeb  

**Tehtävänanto**

x) Kuuntele ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)
Indie Hackers -podcast, vapaavalintainen jakso, jossa hyödynnetään weppiä kaupallisesti.  
a) Vaihda Apachen esimerkkisivu johonkin lyheen sivuun niin, että vanha esimerkkisivu ei näy. (Tämä lienee ainoa kohta, jossa ikinä muokkaat weppisivua pääkäyttäjän oikeuksin. /var/www/html/index.html)  
b) Laita käyttäjien kotisivut (http://example.com/~tero) toimimaan. Testaa esimerkkikotisivulla.  
c) Tee uusi käyttäjä. Kirjaudu ulos omastasi ja sisään uutena käyttäjänä. Tee uudellekin käyttäjälle kotisivu.  
d) Tee validi HTML5 sivu.



## Tehtävät  


### x) Kuuntele ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)Indie Hackers -podcast, vapaavalintainen jakso, jossa hyödynnetään weppiä kaupallisesti.  

Kuunneltu podcast: **Indie Hackers | #266 – Lessons Learned Building a $37k/mo Business in 2.5 Years with Mat De Sousa of WideBundle.**  

Jakson kuvaus: Mat De Sousa (@DsMatie) talks having million-dollar ambitions as a child, learning from numerous failed startups, why Shopify apps are great for indie hackers, the proper way to find a business idea, and growing from $0 to $37k/mo in 2.5 years with Courtland (@csallen) and Channing (@ChanningAllen). [Lähde](https://share.transistor.fm/s/940ae75e)  

**Mistä lähteä liikkeelle:**  
- Usko omaan ideaan  
- Periksiantamattomuus  
- Virheiden tekeminen ja niistä oppiminen  
- Yrittäminen, kerta toisensa jälkeen  

**Keinoja saada oma palvelu/tuote menestymään:**  
- Luo positiivisia kokemuksia   
- Kerää ja kuuntele käyttäjän palautetta   
- Seuraa käytönaikaista dataa. Tässä tapauksessa oltiin seurattu sitä käyttöä joka johti tilaukseen maksuttoman kokeilujakson jälkeen. Selvitettiin mitä nämä käyttäjät olivat tehneet ja hyödynnettiin sitä tuotteen (ohjelmiston) kehittämisessä.  
- Näkyvyys: sosiaalisen median ryhmät, youtube.  
- Kehitä pienin askelin.  
- Sen sijaan että keskitytään vain vahvuuksiin, on myös huomattava heikkoudet.  


**Shopify:**  
- Shopify on verkkokauppa-alusta.  
- Kaikki mitä verkkokaupan pyörittämiseen on samalla alustalla, eli käyttäjä saa tukea esimerkiksi markkinointiin ja maksuliikenteeseen.  
- Tekee verkkokauppatoiminnan aloittamisen kenelle tahansa helpoksi.  

### a) Vaihda Apachen esimerkkisivu johonkin lyheen sivuun niin, että vanha esimerkkisivu ei näy. (Tämä lienee ainoa kohta, jossa ikinä muokkaat weppisivua pääkäyttäjän oikeuksin. /var/www/html/index.html)  

index.html sivun sisällön vaihtaminen:  

    echo Hello|sudo tee /var/www/html/index.html
tai  

    sudoedit /var/www/html/index.html  
    

![Näyttökuva (164)](https://user-images.githubusercontent.com/118609353/216155623-5262be4a-122e-4ff8-a4da-5967c436fb92.png)  

Käynnistetään Apache2 uudelleen:  

    sudo systemctl restart Apache2  
    
Ja katsotaan Mozilla Firefox -selaimessa (http://localhost):  

![Näyttökuva (165) rootstestpage selain](https://user-images.githubusercontent.com/118609353/216156458-00ac14e2-0a50-46c8-94ef-d54699e28765.png)


### b) Laita käyttäjien kotisivut (http://example.com/~tero) toimimaan. Testaa esimerkkikotisivulla.   

### c) Tee uusi käyttäjä. Kirjaudu ulos omastasi ja sisään uutena käyttäjänä. Tee uudellekin käyttäjälle kotisivu.  

Uuden käyttäjän lisääminen:  
    
        sudo adduser debbie02  
        
![Näyttökuva (161) kayttajanlisaaminen](https://user-images.githubusercontent.com/118609353/216150860-792dfa84-652f-439e-9643-f5dbeba47b26.png)  

Käyttäjän poistaminen:  

      sudo deluser debbie01  
         
![Näyttökuva (158) kayttajanpoistaminen](https://user-images.githubusercontent.com/118609353/216151354-8d5414e5-7dfb-404a-8ae7-52f1f8e3cd33.png)  

Käyttäjän vaihtaminen:  

![Näyttökuva (162) kayttajan vaihtaminen](https://user-images.githubusercontent.com/118609353/216156876-bd6e0b44-57a2-4903-b4a5-95c2ee9d7f69.png)  

Uusi käyttäjä:  

![Näyttökuva (163) testuser debbie](https://user-images.githubusercontent.com/118609353/216157104-02b75b5a-575d-4adf-8758-89221ba206b9.png)  

Tehdään käyttäjälle debbie02 oma kotisivu:  

![Näyttökuva (166) debbien oma etusivu](https://user-images.githubusercontent.com/118609353/216161127-094be1c3-db4a-4e5a-b388-cefec3f5d56c.png)



### d) Tee validi HTML5 sivu

Syötin index.html -sivun [Validate by Direct Input](https://validator.w3.org/#validate_by_input)-kohdassa:  

![Näyttökuva (167)](https://user-images.githubusercontent.com/118609353/216164530-cbbe27c8-7c44-4d30-8347-d3cdeec5dc81.png)

 


<br></br> 



#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

[Karvinen, Tero. Short HTML-page.](https://terokarvinen.com/2012/short-html5-page/)  

[Indie Hackers | #266 – Lessons Learned Building a $37k/mo Business in 2.5 Years with Mat De Sousa of WideBundle](https://share.transistor.fm/s/940ae75e)  

[Tunnilla 31.01.2023.](https://github.com/LiljestromNadja/DebianLinux/blob/main/InstallingApache2.md#k%C3%A4ytt%C3%B6%C3%B6notto)








