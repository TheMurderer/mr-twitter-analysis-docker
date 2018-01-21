# Práctica final Cloud Computing
Master Datascience URJC
*Author: Mónica Alexa, Raúl Salazar de Torres*

## Proceso de ejecución de la práctica
Primero deberá ejecutarse el contenedor de python para obtener tweets y posteriormente el de cloudera.

El resultado se verá reflejado en la base de datos mongo, a la cual se puede acceder mediante el comando:
```sh
mongo
```

La información se vuelca en la base de datos **results_sd** y en la colección **results**.

Por tanto, una vez dentro de la consola de mongo deberemos de introducir los siguientes datos para poder visualizar los resultados obtenidos:
```sh
use results_sd
db.results.find()
```

## Lanzamiento de contenedores
### Lanzamiento de contenedor de obtención de tweets
**Nombre del contenedor:** python
**Estructura del comando**
```sh
docker-compose run python
```
Variables de entornos que deben de pasarse como parámetro usando la opción **-e**:
| Nombre del parámetro | Definición |
| -------------------- | ---------- |
| DOWNLOAD_TIME | Tiempo de descarga de tweets |
| NAME_FILE_RESULTS | Nombre del fichero resultante sin extensión |
| ATKEY | Access token KEY de twitter |
| ATSECRET | Access token SECRET de twitter |
| CKEY | Consumer Key de twitter |
| CSECRET | Consumer Secrect de twitter |


Comando de ejemplo a utilizar: 
```sh
docker-compose run -e DOWNLOAD_TIME=20 -e NAME_FILE_RESULTS=salida5 -e ATKEY=214926193-cC5yxpyNnsZklE8H3xZR6cxxoypebgR74uDUdlvy -e ATSECRET=ltz6SahDXs8vcpNsAVXkCeFmuzXz8slpr9AsiL59gOzTt -e CKEY=OqWdq8I3TPlLxylQzACwGL6EP -e CSECRET=HtqbagAZESpfwjTIcAg2ylIBMTrsAmHRxB3pPT854H12Ywbzjw python
```

### Lanzamiento de contenedor de cloudera
**Nombre del contenedor:** cloudera
**Estructura del comando**
```sh
docker-compose run python
```
Variables de entornos que deben de pasarse como parámetro usando la opción **-e**:
| Nombre del parámetro | Definición |
| -------------------- | ---------- |
| NAME_FILE_RESULTS | Nombre del de entrada |


**IMPORTANTE:** El nombre del fichero de entrada debe de corresponder con algún fichero que se haya descargado previamente usando el contenedor de python, y por tanto, se debe de encontrar en la carpeta /input_data.

Comando de ejemplo a utilizar: 
```sh
docker-compose run -e NAME_FILE_RESULTS=salida5 cloudera
```

