# Herramientas Big Data

![Imagen_Big_Data]("imagenes big data\1357.jpg")


Referencia: https://github.com/soyHenry/DS-M4-Herramientas_Big_Data


## Práctica Integradora: Ambiente de Big Data con Docker

Durante esta práctica, hemos preparado un entorno de trabajo basado en Docker que incluye Hadoop (HDFS) y varias herramientas de Big Data, como Spark, Hive, HBase, MongoDB, Neo4j, Zeppelin y Kafka.

## Instrucciones de Uso

1. Lo primero es Clonar este repositorio:

   ```
       git clone https://github.com/soyHenry/DS-M4-Herramientas_Big_Data.git
   ```
2. Dirigirse a:

```
    cd DS-M4-Herramientas_Big_Data
```

3. Luego ejecutar el siguiente comando para levantar el entorno Docker, y comenzar con el 1er ejercicio HDFS.
   NOTA: si bien el original anteponia la palabra 'sudo' en nuestra terminal de Mac no lo usamos, por lo tanto el codigo referido quedo asi: 

   *docker-compose -f docker-compose-vX.yml up -d*

Donde la letra 'X' sera reemplazada por el valor de referencia marcada al principio de cada ejercicio.-
   

## Ejercicio 1) HDFS

Se puede utilizar el entorno docker-compose-v1.yml, por lo tanto, el codigo es: 

```
   docker-compose -f docker-compose-v1.yml up-d
```

Para cargar archivos CSV en HDFS, hay que seguir estos pasos:

1. Copiar los archivos ubicados en la carpeta `Datasets` al contenedor "namenode":

   ``` 
      docker exec -it namenode bash
      cd home
      mkdir Datasets
      exit
      docker cp Datasets namenode:/home/Datasets

   ```

3. Volver a ubicarse nuevamente en el contenedor "namenode":

   ```
      docker exec -it namenode bash
   ```

4. Crear un directorio en HDFS llamado "/data":

   ```
      hdfs dfs -mkdir -p /data
   ```

5. Copia los archivos CSV a HDFS:

   ```
      hdfs dfs -put /home/Datasets/* /data
   ```

Este proceso de creación de la carpeta "data" y copiado de los archivos puede ser automatizado mediante un script de shell, el cual figura el el repositorio original con el nombre de Paso01.sh

## Configuración de Hadoop

Con respecto a la Nota: Busque dfs.blocksize y dfs.replication en http://<IP_Anfitrion>:9870/conf para encontrar los valores de tamaño de bloque y factor de réplica respectivamente entre otras configuraciones del sistema Hadoop.

Hemos aprendido que en nuestro sistema Hadoop, utilizamos ciertas configuraciones predeterminadas para el tamaño de bloque y el factor de replicación en el sistema de archivos distribuido (HDFS). Aquí están los valores clave que pueden ser relevantes para entender el funcionamiento del sistema:

- **Tamaño de bloque (dfs.blocksize):** El tamaño de bloque predeterminado es de 128 MB.
- **Factor de replicación (dfs.replication):** Utilizamos un factor de replicación de 3, lo que significa que cada bloque se replica tres veces en el clúster para proporcionar redundancia y tolerancia a fallos.

