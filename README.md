# Docker DAWe Desplegament d'aplicacions web
##
Introducció a Docker
https://dev.to/pwd9000/introduction-to-github-codespaces-building-your-first-dev-container-69l

## Pas a pas amb docker

## Instal·lar Docker a Ubuntu

## Executar el primer docker
   docker run -d --name apache-container -p 8181:80 httpd:latest

## Executar el primer Dockerfile

   ### Configurar el docker file (escriure això al fitxer Docker file)
   
   ```
   # Utilitza l'imatge oficial de nginx (servidor web) en la seva versió Alpine (més lleugera)
   FROM nginx:alpine
   # Crea un arxiu index.html amb el contingut "Hola Mon"
   RUN echo "<h1>Hola Mon</h1>" > /usr/share/nginx/html/index.html
   # Inicia el servidor nginx
   CMD ["nginx", "-g", "daemon off;"]
   ### Crear l'imatge amb la seva etiqueta (Executar això a la línia de comandes)

   # Crea l'imatge i l'etiqueta (atención al punt, que indica on es troba el Dockerfile)
   docker build -t helloworld:latest .

   # Instancia un contenidor a partir de la etiqueta y li pose el nom helloWorld-container
   docker run -d --name helloworld-container -p 8383:80 helloworld:latest
   ```

   ### Fer algunes proves:
   1. Intentar aixecar altra vegada un contenidor amb les mateixes característiques
      Es pot fer, però amb altre nom, i a un altre port
   2. Si volem que el mateix contenidor funcioni al port 8383?
      comandes: docker ps -a, docker kill, docker start docker container prune

   ### Fer algunes modificacions al docker file
   Imaginar que per qualsevol moiut, necessitem que el servidor web serveixi per un port diferent al 80
   [...] //Tema dekl SED 

## Reorganitzar el repositori
   - Arribat a aqquest punt, podem reorganizar el repositorio per a separar el que acabem de fer, del que vindrà
   - Crear una carpeta helloworld, y moure-ho tot allí
   - Matar tots els dockers, col·locar-se a la carpeta helloworld, y comprovar que encara podem crear l'imatge i desplegar el Docker
   - comandes: docker images, docker container, docker container ls, o list, con --all

## Configurar un contenidor persistent
Els canvis que es fan al contenidor, només es mantenen dins del mateix contenidor, i es mantene després de fer un kill, o un stop, i en reiniciar el contenidor amb la comanda start, però és frequent que durant el cicle de vida d'un contenidor, sigui necessari reconstruir-lo a partir d'actualitzacions de l'imatge original.  Per a fer això, és necessari asociar els directoris que es vulguin conservar amb una imatge o volumen al host.  D'aquesta manera, diferents contenidors generats a partir de la mateixa imatge, poden persistir la seva informació.  

### Diferència entre volumes y bind mount
   Els volums es gestionen amb Docker.
   Los bind mount són muntatges de directoris mé semblants als que fa el sistema operatiu
   ### Opció 1: enllazar un volum "al vuelo"
      - provar de llençar un contenidor sense volumen, crear un arxiu a la carpeta /usr/share/nginx/html del contenidor,i comprovar que funciona accedint a aquest arxiu mitjançabnt el servidor web. Matar el contenidor y "prunar-lo".  Crear un nou contenidor i monat-lo amb el mateix volumen.  Fer la mateixa comprovació (compte amb la caché del navegador).  Quín és el resultat?
      - Fer el mateix amb un contenidor amb un colum muntat (veure més avall)
      - Comandes: docker volume ls, docker volume inspect [nombre o id del volumen], docker exec -it [nombre/id] sh (o verlo en el plugin de docker)
      - Executar amb volum: docker run -d --name helloworld-container -p 8383:80 -v hwc:/usr/share/nginx/html helloworld:latest
   ### Opción 2: montar un directori "al vuelo"

   ## Docker compose
      Com es pot veure, l'instalació de contenidors fent servir només el prompt de la consola, comença a complicar segons les comandes que fem servir, i a mida que volem afegir més característiques a l'imatge.

   ### Posar ho tot junt a un sol docker compose
      Ara  muntarem un contenidor amb les mateixes característiques que el contenidor amb el que hem estat provatn, però ho farem configurant un arxiu docker-compose.ymlmontaremos un contenedor con las mismas características que el contenedor con el que hemos estado probando, pero lo haremos configurando un archivo docker-compose.yml

   ### Afegir un segon container al mateix arxiu doker compose
   ### Extra: Mirar el cplugin de Visual studio code per a treballar amb contenidors docker



