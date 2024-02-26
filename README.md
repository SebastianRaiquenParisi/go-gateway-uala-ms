# Projecto Uala

Este microservicio forma parte de un proyecto con arquitectura de microservicios que sirve para demostrar mi profundidad de conocimiento en Golang, Concurrencia, Go channels, POO, Kafka, Http, GraphQL, SQL y no-SQL db.

![golang-uala](https://github.com/SebastianRaiquenParisi/go-gateway-uala-ms/assets/75135291/4ab190b1-0f5a-444a-b5f6-62f43875a6a7)

Esta conformado por 3 microservicios *go-gateway-uala-ms*, *go-monitoreo-uala-ms* y *go-db-uala-ms*.
Tambien tiene 2 bases de datos no relacionales (no-sql) en *go-monitoreo-uala-ms* y *go-db-uala-ms*, una relacional (sql).
Utiliza kafka como sistema de mensajeria entre microservicios.

### *go-gateway-uala-ms*
En el caso de *go-gateway-uala-ms* tiene la responsabilidad de verificar si el usuario es parte del sistema y permitirle acceso si lo es, por lo tanto debe exponerse y autentificar tanto por GraphQL como por http.
Tambien cuenta con producers de kafka para enviar eventos a *go-monitoreo-uala-ms* y informacion a *go-db-uala-ms*,
asi como una base de datos relacional que guarda los usuarios y los consulta para si el usuario es correcto generar un jwt que permita loguear al usuario.

Es decir tiene estos paquetes:
- kafka.go (productor y consumidor)
- graphql.go (expone el ms en graphql)
- rest.go (expone el ms en http)
- http.go (consume una api externa)
- db.go (base de datos sql para usuarios)
- jwt.go (crea un jwt para ser usado en los otros ms)

Y estas responsabilidades:
- exponer en http y graphql
- enviar por kafka a *go-db-uala-ms* informacion a procesar
- enviar por kafka a *go-monitoreo-uala-ms* eventos (logueo de usuario)

### *go-monitoreo-uala-ms*

y los eventos realizados (envio de kafka, logueo de usuario y realizacion de operacion que seria guardar lo que devuelva el).
Es decir tiene estos paquetes:

Y estas responsabilidades:
- guardar eventos, funcionar como "monitoreo"
En el caso de *go-db-uala-ms* debe hacer toda la logica interna con los eventos enviados a partir de kafka por *go-gateway-uala-ms*, por ejemplo guardar lo que venga de una api externa
o utilizar esa informacion para hacer internamente una operacion. Luego de realizada debe ser enviado un mensaje de kafka hacia *go-gateway-uala-ms*.

- db.go (base de datos sql)

Este microservicio 


