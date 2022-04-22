# AWS-KINESIS-DATA-STREAM

Hasta la fecha todos los tutoriales hechos en esta cuenta de GIthub han sido gratis y con el free-tier. Sin embargo, esta funcionabilidad de AWS no es gratis. Por lo que si realizas el tutorial puede que incurras en algún gasto. 

# Kinesis Data Stream: 

Primero de todo creamos nuestro Data Stream, seleccionando "KINESIS DATA STREAMS" y dando a "Create Data Stream". 

Luego, le añadimos un nombre por ejemplo "DemoStream" y en Capacity Mode seleccionamos el Provisiones dandole solo 1 Shard. Vamos sa ir a lo barato para ver cómo funciona. 

Finalmente Creamos el Data Stream. y esperamos a que se crea. 

Una vez que se crea podemos ver los tipos de Consnumidores que tiene el DataStream y los tipos de Producers. nosotros vamos a ir a lo simple y vamos a comunicarnos con AWS por medio del CLI por cloudshell. 

Se puede usar la termina del ordenador si tienes configurado con aws, pero lo del cloudshell es más rápido. 

Dependiendo en la version del AWS CLI se tendrá que utilizar una línea de comandos u otra: 

1. Verificar la versionde AWS: 

```
aws --version
```

## Producer

Lo primero de todo, vamos a mandar un "record" a nuestro KINESIS DATA STREAM; para hacer esto, hay una API CALL "Put-record". 

```


# CLI v2
aws kinesis put-record --stream-name <NOMBRE_DEL_STREAM> --partition-key user1 --data "user signup" --cli-binary-format raw-in-base64-out

# CLI v1
aws kinesis put-record --stream-name <NOMBRE_DEL_STREAM> --partition-key user1 --data "user signup"


```

Podemos ver el resutlado de esto en KINESIS metrics, pero tarda un poco.





## Consumer

Para consumir, primero tenemos que describir el stream

```
aws kinesis describe-stream --stream-name  <NOMBRE_DEL_STREAM>
```

Y una vez que tenemos la descripción y verifiquemos que todo está bien, nos tenemos que quedar con el ShardID por ejemlpo un: "shardID-000000000000". Esto se debe a que cuando especifiquemos que nos lea la información, tnemeos que pasarle de qué shard estaremos leyendo: 

```
aws kinesis get-shard-iterator --stream-name <NOMBRE_DEL_STREAM> --shard-id shardId-000000000000 --shard-iterator-type TRIM_HORIZON
```


Y finalmente si quiero obtener datos de un shard solo: 

```
aws kinesis get-records --shard-iterator shardId-00000000000
```

:)


