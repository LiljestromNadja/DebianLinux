# Apache 2.4 palvelinohjelman asennus, [Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)

Installing Apache HTTP Server Version 2.4

### Asennus

Tarkistetaan päivitykset:  

    sudo apt-get update  
    
![Näyttökuva (140) apache](https://user-images.githubusercontent.com/118609353/215133885-125686e4-6c37-4763-9dcd-2e1db324db9f.png)

Asennetaan Apache:  

    sudo apt-get install apache2  
    
![Näyttökuva (141) Apache 2](https://user-images.githubusercontent.com/118609353/215134354-644f6649-a27b-4852-b7e8-943e9a810f98.png)

    
Palomuuri, jos sitä ei ole jo asennettu:  

    sudo apt-get install ufw
    
    
Käynnistetään Apache:  

    sudo systemctl start apache2.service
    
Tarkistetaan toimiiko:  

    sudo service apache2 status  
    
![Näyttökuva (146) Apache 7 kaynnistysjatarkistus](https://user-images.githubusercontent.com/118609353/215133585-83120211-8fe6-4f58-a64d-98405764505a.png)

    
Localhost -sivu selaimessa:  
    
    
    
![Näyttökuva (147) Apache8 localhost](https://user-images.githubusercontent.com/118609353/215133158-a5db380d-708f-440b-9131-dac91b14b6da.png)

    
    
### Testailua   

![Näyttökuva (145) Apache 6 httpdeny](https://user-images.githubusercontent.com/118609353/215134817-f9dfaa1f-82f5-4f0d-94aa-570018b01323.png)

##### Sallitaan http-portti 80 (localhost)

    sudo ufw allow http
    
Tarkistetaan, onnistuiko tämä:  

    sudo ufw status    
    
##### sudo ufw allow -komennon kumoaminen ja tarkistus:  

    sudo ufw deny http
    sudo ufw status

    
    
    
    
[Apache HTTP Server Project - Apache HTTP Server Version 2.4](https://httpd.apache.org/docs/2.4/)

    
    
