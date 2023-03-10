

# h13_HelloWorld

**Tehtävänanto:**  

a) Käännä "Hei maailma" kolmella kielellä.  
b) Vapaaehtoinen: greetme. Tee ohjelma, joka ottaa käyttäjän nimen komentoriviparametrina ja tervehtii 'greetme Tero' vastaa "Hello, Tero" ja 'greetme foo' vastaa "Hello, foo".  
c) Vapaaehtoinen: Tee greetme kahdella muullakin kielellä.  

**Vinkit:**

- [Karvinen 2018: Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/)  
- Mille vain kielelle voi hakea hakukoneesta hei maailman "hello world python"  
- Javalla yksi luokka per tiedosto, luokan nimi pitää olla sama sekä tiedoston nimessä että sisällä, isoja ja pieniä kirjaimia myöten. Hello.java, "class Hello".
- Pythonista käytetään versiota kolme, usein komento 'python3'.  
- Käyttäjän syötteet kannattaa ottaa ensisijaisesti suoraan komentoriviltä. Kumpaa itse käyttäisit mieluummin: 'curl https://terokarvinen.com' - vai 'zlur' "Hei, syötä haluamasi weppisivun osoite..."  



[Lähde: Linux-palvelimet 2023 alkukevät](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)   

---
## Tehtävät  

### a) Käännä "Hei maailma" kolmella kielellä.   

Luodaan hakemisto hei ja siirrytään sinne:  

    nadja@debian:~$ mkdir hei  
    nadja@debian:~/hei$ cd hei

**Python:**  

Luodaan tiedosto **hello.py**:  

    nadja@debian:~/hei$ micro hello.py
    
    ->
    print("Hello World!")
    
    ^S + ^Q
    
    
    nadja@debian:~/hei$ python3 hello.py

    ->
    Hello World!

    
    
    
![Näyttökuva 2023-03-07 175859](https://user-images.githubusercontent.com/118609353/223477054-2985c46c-8533-44c3-96a0-aa80be7446ae.png)

**Java:**  

Luodaan Javalle oma kansio:  

        nadja@debian:~/hei$ mkdir javalainen
        nadja@debian:~/hei$ cd javalainen/ 
        
Ja tiedosto **Hello.java:**  

        nadja@debian:~/hei/javalainen$ micro Hello.java  
        
        ->

    public class Hello{
	    public static void main(String[] args){
		    System.out.println("Hello World!");
 	    }
    }

Asennetaan jdk:  

    sudo apt-get install openjdk-17-jdk  
    
    
Kokeillaan:  

    nadja@debian:~/hei/javalainen$ java Hello.java
    
    ->
    Hello World!


![Näyttökuva 2023-03-07 182402](https://user-images.githubusercontent.com/118609353/223484601-d33ce230-949b-4148-b9ae-41dd499c3ae3.png)


**C:**  

    nadja@debian:~/hei$ micro moicee.c
    
    ->
    
    #include <stdio.h>
    int main()
      {
      printf("Hello World\n");
      }
      
      
Kokeillaan:  

    nadja@debian:~/hei$ gcc moicee.c -o moiceec
    nadja@debian:~/hei$ ./moiceec 
    
    ->
    Hello World
    
    
![Näyttökuva 2023-03-07 185454](https://user-images.githubusercontent.com/118609353/223492906-c7d9be56-32f8-496e-a9b7-b5e30073a2fe.png)




  

---

### b) Vapaaehtoinen: greetme. Tee ohjelma, joka ottaa käyttäjän nimen komentoriviparametrina ja tervehtii 'greetme Tero' vastaa "Hello, Tero" ja 'greetme foo' vastaa "Hello, foo".  
 
**Python:**  

 Muokataan tiedostoa **hello.py:**  
 
    nadja@debian:~/hei$ micro hello.py 
    
    ->
    print("Hello World!")
    print("")
    
    username = input("Kirjoita nimesi: ")
    print("Heipä hei " + username + "!")
    
    
    nadja@debian:~/hei$ python3 hello.py 



![Näyttökuva 2023-03-07 183544](https://user-images.githubusercontent.com/118609353/223487819-a927fdee-db9e-4570-97ee-f15c37af055e.png)


 
    
 

---
### c) Vapaaehtoinen: Tee greetme kahdella muullakin kielellä.  

**Java** 

Muokataan tiedostoa **Hello.java:**  

    nadja@debian:~/hei/javalainen$ micro Hello.java 
    
    ->
    
    import java.util.Scanner;  // Import the Scanner class

    public class Hello{
	    public static void main(String[] args){
	
		  System.out.println("Hello World!");

	
		  Scanner scanner = new Scanner(System.in);
		  System.out.println("Annapa nimesi, niin moikataan: ");

		  String nimi= scanner.nextLine();
		  System.out.println("Tervehdys " + nimi + "!");
	
 	    }
    }
    
    
    
Kokeillaan:  
    
    nadja@debian:~/hei/javalainen$ java Hello.java


![Näyttökuva 2023-03-07 184515](https://user-images.githubusercontent.com/118609353/223490436-0744ffa3-654b-4b2a-95e9-6bf7590909b1.png)
	

**C:**  

Muokataan tiedostoa **moicee.c:**  

	nadja@debian:~/hei$ micro moicee.c
	
	->
	#include <stdio.h>
	int main()
	{
 		printf("Hello World\n");

		char nimi[30];


		printf("Kirjoita nimesi: \n");


		scanf("%s", nimi);


		printf("Tervehdys %s", nimi);
		printf("\n");


	}  
	
Kokeillaan:  

	nadja@debian:~/hei$ gcc moicee.c -o moiceec  
	nadja@debian:~/hei$ ./moiceec

	
![Näyttökuva 2023-03-08 000233](https://user-images.githubusercontent.com/118609353/223563631-1b79ca76-6b2c-4961-8b5f-0d47f9746a2c.png)


---
### Tunnilla  

Kuuluuko netti:  
       
    nadja@debian:~$ ping -c 1 8.8.8.8 | grep loss

    ->    
    1 packets transmitted, 1 received, 0% packet loss, time 0ms

Date:  

    nadja@debian:~$ date --iso
    
    ->
    2023-03-07
    
    
Whoami:  

    nadja@debian:~$ whoami
    
    ->
    nadja
   
   

    nadja@debian:~$ micro huomenta

    ->  
    ping -c 1 8.8.8.8 | grep loss
    date --iso
    whoami
    
Bash:  

    nadja@debian:~$ bash huomenta
    
    ->
    1 packets transmitted, 1 received, 0% packet loss, time 0ms
    2023-03-07
    nadja
    

![Näyttökuva 2023-03-07 175032](https://user-images.githubusercontent.com/118609353/223474724-c611b76d-18dd-4179-a6cd-da7b1175c8fa.png)





---
---

#### Lähteet  
  
[Linux-palvelimet alkukevät 2023](https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/)  

[Karvinen 2018: Hello World Python3, Bash, C, C++, Go, Lua, Ruby, Java](https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/)  

 












