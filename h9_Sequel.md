
# h9 _Sequel  

**Tehtävänanto**  
x) Yrityssoftaa. Keksi esimerkki palvelusta, jota käytetään wepissä selaimella, koodi ajetaan palvelimella ja taustalla on tietokanta. Mitä etuja tällä toteutustavalla on vaihtoehtoisiin toteutustapoihin verrattuna? (Tässä x-alakohdassa ei tarvitse tehdä testejä koneella tai toteuttaa mitään, pelkkä kuvittelu ja vastauksen kirjoittaminen riittää)  
a) Postgre. Asenna PostgreSQL ja testaa se suorittamalla SQL-komento. (Jos teit jo tunnilla, tee uusi Linux-käyttäjä ja tälle tietokanta ja tietokantakäyttäjä.)  
b) Crud. Kokeile CRUD (create, read, update, delete) kirjoittamalla SQL-käsin. (Artikkeli alla vinkeissä kertoo, kuinka tämä tehdään. Jos SQL on tuttua, voit keksiä tauluille ym omat aiheet ja nimet.)  
n) Vapaaehtoinen: Maria. Asenna MariaDB ja kokeille sillä CRUD.  


**Vinkit:**  
Karvinen 2016-2023: [Install PostgreSQL on Ubuntu – New user and database in 3 commands](https://terokarvinen.com/2016/03/03/install-postgresql-on-ubuntu-new-user-and-database-in-3-commands/)  
Karvinen 2016-2023: [PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu](https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/)  
'sudo adduser tero'  
Karvinen 2018: [Install MariaDB on Ubuntu 18.04 – Database Management System, the New MySQL](https://terokarvinen.com/2018/09/20/install-mariadb-on-ubuntu-18-04-database-management-system-the-new-mysql/)  




[Lähde](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)   


---
## Tehtävät  



### x) Yrityssoftaa. Keksi esimerkki palvelusta, jota käytetään wepissä selaimella, koodi ajetaan palvelimella ja taustalla on tietokanta. Mitä etuja tällä toteutustavalla on vaihtoehtoisiin toteutustapoihin verrattuna? (Tässä x-alakohdassa ei tarvitse tehdä testejä koneella tai toteuttaa mitään, pelkkä kuvittelu ja vastauksen kirjoittaminen riittää)  

---

### a) Postgre. Asenna PostgreSQL ja testaa se suorittamalla SQL-komento. (Jos teit jo tunnilla, tee uusi Linux-käyttäjä ja tälle tietokanta ja tietokantakäyttäjä.)   

Kirjauduin virtuaalikoneelle:  
 
    nadja@debbiedebian:~$ ssh sudouser@46.101.234.74  
 
 **PostgreSQL:n asennus:**    

    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ sudo apt-get update  

    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ sudo apt-get install postgresql  

    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ psql
    
![Näyttökuva (229)](https://user-images.githubusercontent.com/118609353/219135506-bf19a5fe-93a3-4007-8b25-65b72e07bf3c.png)  

    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ sudo systemctl start postgresql
    
    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ psql  
    
    
Yhä sama error: psql: error: FATAL:  role "sudouser" does not exist.  
Luodaan siis tietokanta sekä tietokantakäyttäjä eli "role" (-u -> yhden komennon ajan "eri käyttäjä"):  
    
    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ sudo -u postgres createdb sudouser  
    
    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ sudo -u postgres createuser sudouser  
    
    sudouser@debian-s-1vcpu-1gb-amd-fra1-01-viapw:~$ psql
  
![Näyttökuva (230) role and database created](https://user-images.githubusercontent.com/118609353/219138383-3f5032ee-4cea-46df-8d84-48cd7c09aaf1.png)



---

### b) Crud. Kokeile CRUD (create, read, update, delete) kirjoittamalla SQL-käsin. (Artikkeli alla vinkeissä kertoo, kuinka tämä tehdään. Jos SQL on tuttua, voit keksiä tauluille ym omat aiheet ja nimet.)  

#### Create  

Luodaan taulu ja lisätään siihen tietoa:  

    CREATE TABLE taulunnimi(sarakkeennimi TIETOTYYPPI, toinensarake TYYPPI(koko), kolmas TYYPPI(koko));  

eli 

    sudouser=> CREATE TABLE tamaontesti (id SERIAL PRIMARY KEY, name VARCHAR(50), otherinfo VARCHAR(300));  

Tiedon lisääminen tauluun (automaattista ID:tä ei syötetä):  

    INSERT INTO taulunnimi(sarakkeennimi, sarakkeennimi2) VALUES (syotettavaArvo1, syotArvo2);

eli 

    sudouser => INSERT INTO tamaontesti(name, otherinfo) VALUES('Pentti', 'Tämä on testirivi');  
    
List of relations:    

    sudouser=> \d  
    
![Näyttökuva (231) create table insert list of relations](https://user-images.githubusercontent.com/118609353/219152704-2623c9bc-d1dd-4ba9-945d-0b080adf0d19.png)  

---


#### Read  

Katsotaan koko taulu: 

    SELECT * FROM taulunnimi; 
    
eli 

    sudouser=> SELECT * FROM tamaontesti; 
    
Haetaan tietty merkkijono taulusta:  

    SELECT * FROM taulunnimi WHERE sarakkeennimi="etsittava";  
eli  
    sudouser=> SELECT * FROM tamaontesti WHERE name='Toinen';  
    
    
![Näyttökuva (232) read](https://user-images.githubusercontent.com/118609353/219156211-75a345d0-92a4-45eb-b1dd-e77fccd72d84.png)  

----

#### Update

Tiedon muuttaminen:  

    UPDATE taulunnimi SET sarake='paivitettavatieto' WHERE sarake'etsittavamerkkijo';  

eli 

    sudouser=> UPDATE tamaontesti SET otherinfo='-' WHERE id=2;
    
Katsotaan:  

    SELECT*FROM tamaontesti; 
    
![Näyttökuva (233) crud update](https://user-images.githubusercontent.com/118609353/219160304-7a2d70f0-23e4-4289-8c0d-783bbe940082.png)

---

#### Delete

Tiedon poistaminen:

    DELETE FROM taulunNimi WHERE sarake='etsittavatieto':
    
eli 

    sudouser=> DELETE FROM tamaontesti WHERE name='Toinen';
    
Katsotaan:  

      sudouser=> SELECT * FROM tamaontesti;  


![Näyttökuva (234) crud delete](https://user-images.githubusercontent.com/118609353/219163892-7294926a-4a84-4c62-a0b5-7f3a2604f17a.png)

**Koko taulun poistaminen** (tyhjensin taulun ensin):

    DROP TABLE taulunnimi;
    
eli 

    sudouser=> DROP TABLE TESTATAAN; 
    
![Näyttökuva (235) drop table](https://user-images.githubusercontent.com/118609353/219169005-a3437875-417c-46fc-9731-78a6caaa00bb.png)  

---

**Poistuminen postgreSQL:stä:**  

    \q 
    
**"Edellinen":**    
    alt gr + q
    
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

Karvinen 2016-2023: [Install PostgreSQL on Ubuntu – New user and database in 3 commands](https://terokarvinen.com/2016/03/03/install-postgresql-on-ubuntu-new-user-and-database-in-3-commands/)  
Karvinen 2016-2023: [PostgreSQL Install and One Table Database – SQL CRUD tutorial for Ubuntu](https://terokarvinen.com/2016/03/05/postgresql-install-and-one-table-database-sql-crud-tutorial-for-ubuntu/)  
Karvinen 2018: [Install MariaDB on Ubuntu 18.04 – Database Management System, the New MySQL](https://terokarvinen.com/2018/09/20/install-mariadb-on-ubuntu-18-04-database-management-system-the-new-mysql/)  


<!--- 
---
--->











