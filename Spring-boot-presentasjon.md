#Hva er Spring boot

Spring boot er bygget på toppen av Spring og tilbyr alle muligheter som spring tilbyr, men har 
som formål å minimere tid brukt på konfigurasjon og oppsett.

Dette gjøres på 2 måter
* Spring boot kommer med default oppsett basert på hva den finner på class path. Den prøver å autokonfigurere "alt".
* Xml config kan brukes men default så skreddersyr man konfigurasjon via @Configuration annoterte klasser

Spring boot kan kjøre med en embedded http server, default er tomcat, men kan også kjøre med jetty eller undertow.

#Spring boot starter dependencies
Dependency managment kan være komplisert å håndtere, spesiellt for store prosjekter. Spring boot kommer med en 
sett dependencies som skal lette utvikler jobben for dette.

Disse har alle samme navnekonvensjon: spring-boot-starter- *

For eksempel for å lage rest endpoints, legg til følgende i pom fila:
```
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

Eksempler:
* spring-boot-starter-web (inkluderer tomcat som default container)
* spring-boot-starter-websocket
* spring-boot-starter-test
* spring-boot-starter-jdbc
* spring-boot-starter-actuator
* spring-boot-starter-security
* pluss en haug med andre  
  
  
#Migrere fra Spring til Spring boot
Litt kort om hva som må til  for å migrerere eksisterende spring apps til spring boot
* Sett opp spring boot starters
* Application entry point 
    - En java klasse med main metode som er annotert med @SpringBootApplication
    - Denne gir @Configuration, @EnableAutoConfiguration og @ComponentScan
* Import konfigurasjon og komponenter
    - Enten flytt alle @Configuration klasser under samme pakka som main klasse fila eller importer dem explicit
    - Migrer xml configurasjon eller bruk  @ImportResource
* Migrer application resources
    * Default så leter spring boot under:
    ```
        /resources
        /public
        /static
        /META-INF/resources
    ```
* Migrer  application properties
* Migrer Spring web application
    * Erstatt all web specific dependencies med spring-boot-starter-web dependency, masse config kan fjernes
    og @EnableWebMvc blir lagt til i main app class, samt at det konfes opp en DispatcherServlet.
         
         
Dok: https://docs.spring.io/spring-boot/docs/current/reference/html/index.html
