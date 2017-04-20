# logstash

 Iniciar Elastic 

```sudo systemctl start elasticsearch ```

Descargar e instalar la llave publica 

``` rpm --import https://artifacts.elastic.co/GPG-KEY-elasticsearch ```

Abrir en /etc/yum.repos.d/ el archivo logstash.repo con la siguiente configuración.

```
[logstash-5.x]
name=Elastic repository for 5.x packages
baseurl=https://artifacts.elastic.co/packages/5.x/yum
gpgcheck=1
gpgkey=https://artifacts.elastic.co/GPG-KEY-elasticsearch
enabled=1
autorefresh=1
type=rpm-md ```

Realizar un yum

```sudo yum install logstash ```

Consultar la ruta de logstash y abrir la ruta obtenida

```whereis logstash```

En la ruta obtenida crear un archivo tipo .conf con el script(anteriormente darle permisos a /var/log/messages)

```
input{
   file{
      path => "/var/log/messages"
      start_position => beginning
   }
}

output {
    elasticsearch {
        hosts => [ "localhost:9200" ]
        index => "indexname"
    }
}
```
Ejecutar el siguiente comando cambiando el nombre del conf

```sudo bin/logstash -f name_task.conf ```



Para consultar los indices

```curl 'localhost:9200/_cat/indices?v' ```
```curl 'localhost:9200/index/_search?pretty'```







