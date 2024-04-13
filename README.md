Por supuesto, aquí tienes el markdown completo para agregar al README de tu repositorio:

```markdown
# Práctica Integradora: Ambiente de Big Data con Docker

Durante esta práctica, hemos preparado un entorno de trabajo basado en Docker que incluye Hadoop (HDFS) y varias herramientas de Big Data, como Spark, Hive, HBase, MongoDB, Neo4j, Zeppelin y Kafka.

## Instrucciones de Uso

1. Clona este repositorio:

   ```bash
   git clone https://github.com/lopezdar222/herramientas_big_data
   cd herramientas_big_data
   ```

2. Ejecuta el siguiente comando para levantar el entorno Docker:

   ```bash
   sudo docker-compose -f docker-compose-vX.yml up -d
   ```

3. Accede a las interfaces de las herramientas utilizando las siguientes URL:

   - **Namenode:** http://<IP_Anfitrion>:9870/dfshealth.html#tab-overview
   - **Datanode:** http://<IP_Anfitrion>:9864/
   - **Spark master:** http://<IP_Anfitrion>:8080/
   - **Spark worker:** http://<IP_Anfitrion>:8081/
   - **HBase Master-Status:** http://<IP_Anfitrion>:16010
   - **HBase Zookeeper_Dump:** http://<IP_Anfitrion>:16010/zk.jsp
   - **HBase Region_Server:** http://<IP_Anfitrion>:16030
   - **Zeppelin:** http://<IP_Anfitrion>:8888
   - **Neo4j:** http://<IP_Anfitrion>:7474

## Carga de Archivos CSV en HDFS

Para cargar archivos CSV en HDFS, sigue estos pasos:

1. Utiliza el archivo de configuración `docker-compose-v1.yml` para el entorno.

2. Copia los archivos ubicados en la carpeta `Datasets` al contenedor "namenode":

   ```bash
   sudo docker exec -it namenode bash
   cd home
   mkdir Datasets
   exit
   sudo docker cp <path>/<archivo> namenode:/home/Datasets/<archivo>
   ```

3. Ubícate en el contenedor "namenode":

   ```bash
   sudo docker exec -it namenode bash
   ```

4. Crea un directorio en HDFS llamado "/data":

   ```bash
   hdfs dfs -mkdir -p /data
   ```

5. Copia los archivos CSV a HDFS:

   ```bash
   hdfs dfs -put /home/Datasets/* /data
   ```

Este proceso de creación de la carpeta "data" y copiado de los archivos puede ser automatizado mediante un script de shell.

## Configuración de Hadoop

En nuestro sistema Hadoop, utilizamos ciertas configuraciones predeterminadas para el tamaño de bloque y el factor de replicación en el sistema de archivos distribuido (HDFS). Aquí están los valores clave que pueden ser relevantes para entender el funcionamiento del sistema:

- **Tamaño de bloque (dfs.blocksize):** El tamaño de bloque predeterminado es de 128 MB.
- **Factor de replicación (dfs.replication):** Utilizamos un factor de replicación de 3, lo que significa que cada bloque se replica tres veces en el clúster para proporcionar redundancia y tolerancia a fallos.

Puedes encontrar más detalles sobre estas configuraciones en el archivo de configuración `hdfs-default.xml` del clúster Hadoop.
```

Este markdown proporciona una guía completa para utilizar el entorno Docker, cargar archivos en HDFS y entender las configuraciones predeterminadas de Hadoop. Asegúrate de reemplazar `<IP_Anfitrion>` con la dirección IP real de tu host en todas las URL proporcionadas.
