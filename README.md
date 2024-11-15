Crea un repositorio para contestar todo o exame.
Este repositorio ten que conter tódo-los ficheiros necesarios para xustifica-la túas respostas.

Contesta as seguintes preguntas, xustificándoas, nun README.md

1. Explica métodos para 'abrir' unha consola/shell a un contenedor en execución.

Por consola puedes poner el comando:

    docker exec -it (nombre del contendor) /bin/bash
    
En VSCode entras al apartado de docker y le das click derecho sobre el contenedor, das click sobre attach sell y ya estaría.

2. No contenedor anterior (en execución), qué opciones tes que ter usado ó arrincalo para poder interactuar coas súas entradas e salidas

Tienes que usar -it.

3. Cómo sería un ficheiro docker-compose para que dous contenedores se comuniquen entre si nunha rede só deles?

Tendrías que poner las siguientes lineas:

    network:
        (nombre de la red)


4. Qué tes que engadir ó ficheiro anterior para que un contenedor teña unha IP fixa?

networks:
      bind9_subnet:
        ipv4_address: ( la ip que quieras ponerle al contenedor )
        
Esto lo tendras que hacer dentro del apartado del contenedor que quieras ponerle la ip

5. Qué comando de consola podo usar para sabe-las ips dos contenedores anteriores?

Con el siguiente comando:

    docker network inspect (nombre de la red)


6. Cál é a funcionalidade do apartado "ports" en docker compose?

El apartado ports se usa para mapear un puerto del hosts al puerto del contenedor y asi puedan conectarse.

7. Para qué serve o rexistro CNAME? Pon un exemplo

Su funcion es que un dominio sirva de alias para otro.
Ejemplos: 

8. Cómo podo facer para que a configuración dun contenedor DNS non se borre se creo outro contenedor?

Creando los contenedores por docker-compose, usando una archivo.yml 

9. Engade unha zoa tendaelectronica.int no teu docker DNS que teña:
- www á IP 172.16.0.1
- owncloud sexa un CNAME de www
- un rexistro de texto có contido "1234ASDF"
Comproba que todo funciona có comando "dig"

    ; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> tendaelectronica.int
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 14261
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

    ;; OPT PSEUDOSECTION:
    ; EDNS: version: 0, flags:; udp: 65494
    ;; QUESTION SECTION:
    ;tendaelectronica.int.                     IN      A

    ;; ANSWER SECTION:
    tendaelectronica.int.              185     IN      A       172.28.5.4

    ;; Query time: 0 msec
    ;; SERVER: 127.0.0.11#53(127.0.0.11) (UDP)
    ;; WHEN: Fri Nov 15 18:34:18 UTC 2024
    ;; MSG SIZE  rcvd: 54

Mostra nos logs que o servicio funciona ben usando a saída da terminal ó levantar o compose ou có comando "docker logs [nomeContenedorOuID]"----> 

    15-Nov-2024 18:57:25.201 running as: named -u bind -g
15-Nov-2024 18:57:25.201 compiled by GCC 13.2.0
15-Nov-2024 18:57:25.201 compiled with OpenSSL version: OpenSSL 3.0.13 30 Jan 2024
15-Nov-2024 18:57:25.201 linked to OpenSSL version: OpenSSL 3.0.13 30 Jan 2024
15-Nov-2024 18:57:25.201 compiled with libuv version: 1.48.0
15-Nov-2024 18:57:25.201 linked to libuv version: 1.48.0
15-Nov-2024 18:57:25.202 compiled with libxml2 version: 2.9.14
15-Nov-2024 18:57:25.202 linked to libxml2 version: 20914
15-Nov-2024 18:57:25.202 compiled with json-c version: 0.17
15-Nov-2024 18:57:25.202 linked to json-c version: 0.17
15-Nov-2024 18:57:25.202 compiled with zlib version: 1.3
15-Nov-2024 18:57:25.202 linked to zlib version: 1.3
15-Nov-2024 18:57:25.202 ----------------------------------------------------
15-Nov-2024 18:57:25.202 BIND 9 is maintained by Internet Systems Consortium,
15-Nov-2024 18:57:25.202 Inc. (ISC), a non-profit 501(c)(3) public-benefit 
15-Nov-2024 18:57:25.202 corporation.  Support and training for BIND 9 are 
15-Nov-2024 18:57:25.202 available at https://www.isc.org/support
15-Nov-2024 18:57:25.202 ----------------------------------------------------
15-Nov-2024 18:57:25.202 found 4 CPUs, using 4 worker threads
15-Nov-2024 18:57:25.202 using 4 UDP listeners per interface
15-Nov-2024 18:57:25.205 DNSSEC algorithms: RSASHA1 NSEC3RSASHA1 RSASHA256 RSASHA512 ECDSAP256SHA256 ECDSAP384SHA384 ED25519 ED448
15-Nov-2024 18:57:25.205 DS algorithms: SHA-1 SHA-256 SHA-384
15-Nov-2024 18:57:25.205 HMAC algorithms: HMAC-MD5 HMAC-SHA1 HMAC-SHA224 HMAC-SHA256 HMAC-SHA384 HMAC-SHA512
15-Nov-2024 18:57:25.205 TKEY mode 2 support (Diffie-Hellman): yes
15-Nov-2024 18:57:25.205 TKEY mode 3 support (GSS-API): yes
15-Nov-2024 18:57:25.208 loading configuration from '/etc/bind/named.conf'
15-Nov-2024 18:57:25.208 unable to open '/etc/bind/bind.keys'; using built-in keys instead
15-Nov-2024 18:57:25.209 looking for GeoIP2 databases in '/usr/share/GeoIP'
15-Nov-2024 18:57:25.209 using default UDP/IPv4 port range: [32768, 60999]
15-Nov-2024 18:57:25.209 using default UDP/IPv6 port range: [32768, 60999]
15-Nov-2024 18:57:25.210 listening on IPv4 interface lo, 127.0.0.1#53
15-Nov-2024 18:57:25.211 listening on IPv4 interface eth0, 172.28.5.1#53
15-Nov-2024 18:57:25.211 IPv6 socket API is incomplete; explicitly binding to each IPv6 address separately
15-Nov-2024 18:57:25.211 listening on IPv6 interface lo, ::1#53
15-Nov-2024 18:57:25.214 generating session key for dynamic DNS
15-Nov-2024 18:57:25.214 sizing zone task pool based on 1 zones
15-Nov-2024 18:57:25.214 none:99: 'max-cache-size 90%' - setting to 7147MB (out of 7941MB)
15-Nov-2024 18:57:25.215 using built-in root key for view _default
15-Nov-2024 18:57:25.215 set up managed keys zone for view _default, file 'managed-keys.bind'
15-Nov-2024 18:57:25.216 configuring command channel from '/etc/bind/rndc.key'
15-Nov-2024 18:57:25.216 command channel listening on 127.0.0.1#953
15-Nov-2024 18:57:25.216 configuring command channel from '/etc/bind/rndc.key'
15-Nov-2024 18:57:25.216 command channel listening on ::1#953
15-Nov-2024 18:57:25.216 not using config file logging statement for logging due to -g option
15-Nov-2024 18:57:25.217 managed-keys-zone: loaded serial 2
15-Nov-2024 18:57:25.217 /var/lib/bind/db.asircastelao.int:14: file does not end with newline
15-Nov-2024 18:57:25.217 zone asircastelao.int/IN: loaded serial 10000002
15-Nov-2024 18:57:25.217 all zones loaded
15-Nov-2024 18:57:25.218 running
15-Nov-2024 18:57:25.234 managed-keys-zone: Initializing automatic trust anchor management for zone '.'; DNSKEY ID 20326 is now trusted, waiving the normal 30-day waiting period.


(o apartado 9 realízase na máquina virtual)





