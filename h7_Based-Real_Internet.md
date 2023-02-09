# h7_Based-Real_Internet(tm)

**Tehtävänanto**  
x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli.  
(Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)  
[Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)    
a) Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta.  
(Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla vagran:tia paikallisesti).  
b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.  
c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. (Muista tehdä reikä tulimuuriin).  
d) Etsi merkkejä murtautumisyrityksistä.  

**Vinkit:**  

Aina hyvät salasanat  
sudo ufw allow 22/tcp; sudo ufw allow 80/tcp  
Wannabe-murtautujia voit löytää lokeista, /var/log/auth.log, joskus myös /var/log/apache2/access.log  
Nykyisin demonin uudelleenkäynnistys 'sudo systemctl restart apache2' (ei enää service)  
[Lähde](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)   

---
## Virtuaalipalvelin palveluntarjoajalta  

Tehtävää varten rekisteröidyin [GitHub Education](https://education.github.com/) -käyttäjäksi. Valitsin palveluntarjoajaksi [Digital Oceanin](https://cloud.digitalocean.com).  

---
## Tehtävät  

### x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. [Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)  

First steps on a new Virtual Private server: 

0. "Always use good passwords. Only good passwords. Good passwords every moment."  
1. Create a new virtual server on the service provider's site.
2. Log in for the first time: '$ ssh root@exampleIPv4'
3. Firewall. Before enabling, remember to make a hole for SSH.
4. Add different type of users with different type of privileges.
5. Close root account. '$ Usermod --lock root' just locks the password, not every way to use the user.
6. Upgrade software. 
7. Start using it. Remember ‘$ sudo ufw allow 80/tcp’ when you install a public server such as Apache.
8. Get Public DNS Name.



---

### a) Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. (Vaihtoehtona voit käyttää ilmaista kokeilujaksoa, GitHub Education krediittejä; tai jos mikään muu ei onnistu, voit kokeilla vagran:tia paikallisesti).  

**Palveluntarjoaja:** Digital Ocean  
**Droplet:**  

Create -> Droplets(Create cloud servers)  

Choose Region -> Frankfurt  

Choose an image -> Debian

Version -> 11 x64  

Droplet Type -> SHARED CPU, Basic

CPU options -> Regular(Disk type:SSD)  

$6/mo
1GB/ 1CPU
25 GB SSD Disk
1000GB transfer

Choose Authentication Method -> Password(SSH recommended)  

Create Droplet ->  

![Näyttökuva (205) dropleetin luominen](https://user-images.githubusercontent.com/118609353/217606297-bee6a400-84ec-4c41-9bab-b21dad04b790.png)  


---

### b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.  

Komentoriville mars:  

    nadja@debbiedebian:~$ ssh root@PIv4osoite eli ->  

    nadja@debbiedebian:~$ ssh root@165.227.131.128  

Ja tietenkin, kurssilla muutamaan otteeseen kuultu lausahdus "Kun tietokoneet ei koskaan toimi", 
toteutui. 

![Näyttökuva (198) ssh command not found](https://user-images.githubusercontent.com/118609353/217606364-9207a014-01ae-4666-8991-7539bde33dbb.png)  

Ihan ensimmäiseksi kokeilin asentaa päivitykset. Ei vaikutusta.  


    nadja@debbiedebian:~$ sudo apt-get update  

    nadja@debbiedebian:~$ sudo apt-get -y dist-upgrade  


Hyvän tovin pyöriskelin netissä etsimässä ratkaisua, muun muassa [täältä.](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server)  


Youtubesta löytyi ratkaisu:  
[Failed to start ssh service Unit ssh.service could not be found Ubuntu](https://www.youtube.com/watch?v=95ssd2a2Re0)  

Ei kun kokeilemaan:   

    nadja@debbiedebian:~$ sudo apt-get install openssh-server  

    nadja@debbiedebian:~$ sudo systemctl start ssh  
    nadja@debbiedebian:~$ sudo systemctl status ssh  

![Näyttökuva (199) ssh status toimii jee](https://user-images.githubusercontent.com/118609353/217606613-15300262-5da5-4cf4-947b-703244fb8d7c.png)  

Käynnissä on. Eli jatkoin siitä mihin jäätiin:   

    nadja@debbiedebian:~$ ssh root@165.227.131.128  

Are you sure you want to continue connecting?  

    nadja@debbiedebian:~$ yes  

Seuraavaksi salasana, jonka määrittelin luodessani dropletia.   

![Näyttökuva (201) debianin rootissa](https://user-images.githubusercontent.com/118609353/217606721-47986bc3-957a-42e0-9fe0-36629fc4ef99.png)  

Sitten päivitykset ja "tulimuuri":  

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo apt-get update 
    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo apt-get -y dist-upgrade

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo apt-get install ufw  

"Rei'itetään" ennen palomuurin päällekytkemistä:  

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo ufw allow 22/tcp  

Laitetaan muuri päälle:   

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo ufw enable  

Proceed with operation?  

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# y  

![Näyttökuva (202) palomuuri päivitetty](https://user-images.githubusercontent.com/118609353/217606963-acab489d-1d38-43d2-b2f2-01122a333063.png)  

---

### c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. (Muista tehdä reikä tulimuuriin).  


    root@debian-s-1vcpu-1gb-amd-fra1-01:~# hostname -I   

Sitten Apache2:  

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo apt-get install apache2  

Käynnistetään:  

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo systemctl start apache2  
    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo service apache2 status  

Muokataan "etusivu":  

    root@debian-s-1vcpu-1gb-amd-fra1-01:~# echo moi | sudo tee /var/www/html/index.html  
    root@debian-s-1vcpu-1gb-amd-fra1-01:~# echo helloWeb | sudo tee /var/www/html/index.html  


![Näyttökuva (203) uusi curl localhost](https://user-images.githubusercontent.com/118609353/217607192-b06f8135-cf25-4716-9b2e-c058bef5d843.png)  


    root@debian-s-1vcpu-1gb-amd-fra1-01:~# sudo ufw allow 80/tcp  
    
    root@debian-s-1vcpu-1gb-amd-fra1-01:~#sudo systemctl restart apache2  

Netissä ollaan!  

![Näyttökuva (204) netissä ollaan](https://user-images.githubusercontent.com/118609353/217607293-e5839a16-533a-41e6-a5ce-d2c8d4aab236.png)  


Tämän jälkeen "tuhosin" äskeisen Dropletin, jolloin terminaalissa
siirryin "omalle koneelle" (nadja@debbiedebian).  

---

#### SSH-avain (omalla virtuaalikoneella)  

        nadja@debbiedebian:~$ ssh-key ja tabia perään

        nadja@debbiedebian:~$ ssh-keygen

Enterillä eteenpäin. En luonut tällä kertaa passphrasea, joten jatkoin enterillä.  

        nadja@debbiedebian:~$ cd .ssh
        nadja@debbiedebian:~/.ssh$ ls
        
        nadja@debbiedebian:~$ micro id_rsa.pub

Kopioin koko pitkä pätkän (microssa CTRL+C) ja liitin se SSH Public Key -kenttään luodessani uuden Dropletin.  

Sitten taas omaan terminaaliin:  

        nadja@debbiedebian:~/.ssh$ ssh root@164.92.170.157  

Are you sure you want to continue connecting?  

        nadja@debbiedebian:~/.ssh$ yes

Nyt ei tarvitse siis kirjoittaa salasanaa, koska sellaista ei luotu. Jos salasanan käytön haluaa lukita ssh-avainta käytettäessä (ole tässä tapauksessa varma, että käytät ssh-avainta, sillä jos käytössä on vain salasana, lukitset itsesi ulos):

        root@debian-s-1vcpu-1gb-fra1-01:~# usermod --lock root
        root@debian-s-1vcpu-1gb-fra1-01:~# exit  

Testaillaan vielä:  

        nadja@debbiedebian:~/.ssh$ ssh root@164.92.170.157

![Näyttökuva (207) sshkeytoimiirootlukittu](https://user-images.githubusercontent.com/118609353/217667745-e6654d35-1c0b-4ae9-8139-a6c2df196914.png)

Koska kaikki meni niin kuin pitikin, muistin virkistämiseksi päivitykset ja tulimuurit kohdilleen: 

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo apt-get update  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo apt-get -y dist-upgrade  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo apt-get install ufw   

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo ufw allow 22/tcp  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo ufw enable  

        Proceed with operation? 

        root@debian-s-1vcpu-1gb-fra1-01:~# y  

        root@debian-s-1vcpu-1gb-fra1-01:~# hostname -I (voi tarkistaa että on oikea)  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo apt-get install apache2  

        Do you want to continue?

        root@debian-s-1vcpu-1gb-fra1-01:~# y  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo systemctl start apache2  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo service apache2 status  

        root@debian-s-1vcpu-1gb-fra1-01:~# echo moi | sudo tee /var/www/html/index.html  

        root@debian-s-1vcpu-1gb-fra1-01:~# curl localhost  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo ufw allow 80/tcp  

        root@debian-s-1vcpu-1gb-fra1-01:~# sudo systemctl restart apache2

![Näyttökuva (208) helloThere](https://user-images.githubusercontent.com/118609353/217668104-94ec91b5-dc63-427f-9392-b9a4091b53cc.png)

---
#### Root kiinni  

    root@debian-s-1vcpu-1gb-fra1-01:~#  sudoedit /etc/ssh/sshd_config
    
Etsin tiedostosta kohdan (nano, CTRL+W) 'PermitRootLogin yes' ja vaihdoin siihen 'PermitRootLogin no'.  

    root@debian-s-1vcpu-1gb-fra1-01:~#  sudo service ssh restart
    
![Näyttökuva (209) rootLoginNo](https://user-images.githubusercontent.com/118609353/217683021-b324c22c-1b79-4184-ad9d-773aba584bf2.png)


---
### d) Etsi merkkejä murtautumisyrityksistä.   
Testailin itse virheellisiä kirjautumisyrityksiä, yrittämällä kirjautua lukittuun rootiin, kirjautumista väärällä salasanalla sekä olemattomalla käyttäjätunnuksella:   

![Näyttökuva (211) väärät kirjautumiset ja auth log](https://user-images.githubusercontent.com/118609353/217877814-d64acb82-1392-4704-ad05-13ad9fb389d8.png)

Lukittuun rootiin oli toki muitakin pyrkijöitä:  


![Näyttökuva (213) osaa ne muutkit](https://user-images.githubusercontent.com/118609353/217878026-e755ec84-0768-4cbd-9756-8f42ee2bee99.png)

![Näyttökuva (213) ihmeip pieni](https://user-images.githubusercontent.com/118609353/217879226-30f99634-5923-4617-b86e-312ef210c0cc.png)  



<!---
d-osio oli vähän myöhässä palautettu

-->



#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

[Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS](https://terokarvinen.com/2017/first-steps-on-a-new-virtual-private-server-an-example-on-digitalocean/)  
[Digital Ocean tutorial](https://www.digitalocean.com/community/tutorials/how-to-use-ssh-to-connect-to-a-remote-server)  
[Failed to start ssh service Unit ssh.service could not be found Ubuntu. Youtube.](https://www.youtube.com/watch?v=95ssd2a2Re0)  

---
I also changed my password with  

        $ passwd
        
:sweat_smile:










