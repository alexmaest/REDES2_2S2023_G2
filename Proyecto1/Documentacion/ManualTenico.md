![Net Image](https://www.tokioschool.com/wp-content/uploads/2021/05/TOKIOBLOG-tipos-de-redes-informaticas-0123.jpg "Banner | Network Image")

# Manual técnico | Proyecto 1 <img src="https://media.tenor.com/dHk-LfzHrtwAAAAi/linux-computer.gif" alt="drawing" width="30"/>

## Integrantes Grupo 2

| Carnet    | Nombre                        |
| --------- | ----------------------------- |
| 201800476 | Marvin Alexis Estrada Florian |
| 201902781 | Rodrigo Antonio Porón De León |

## Topología implementada

Se utilizó la herramienta Packet Tracer para la implementación de la topología solicitada, constando de 8 switches 3560, 4 switches 3650 y 4 switches 2960 de capa 2, utilizando 4 PC-PT y 4 Laptop-PT, cada switch configurado con sus respectivos puertos truncales y de acceso como se detallará más adelante:

![IP](images/topology.png)

Para la conexión de switches 3650 con cable de fibra óptica, se realizó la configuración de agregar puertos y un módulo de fuente de poder a los 4 switches centrales de la topología:

![MODULE](images/module.png)

## Configuración de Ip

Existen 9 redes dentro de la topología con una ip determinada con la siguientes direcciones en la tabla:

| Dirección    | Máscara de subred |
| ------------ | ----------------- |
| 192.168.12.0 | 255.255.255.0     |
| 192.168.22.0 | 255.255.255.0     |
| 192.168.32.0 | 255.255.255.0     |
| 192.168.42.0 | 255.255.255.0     |
| 12.0.0.0     | 255.0.0.0         |
| 22.0.0.0     | 255.0.0.0         |
| 32.0.0.0     | 255.0.0.0         |
| 42.0.0.0     | 255.0.0.0         |
| 52.0.0.0     | 255.0.0.0         |

## Configuración de puertos

En este apartado, se realizó la configuración de los puertos de cada switch, a nivel general se configuraron únicamente para los que tienen contacto directo con alguna PC-PT, Laptop-PT, los 2 servidores DHCP y el servidor Web se colocaron en modo acceso, para todos los demás puertos se configuraron en modo trunked para una correcta comunicación entre toda la toología, por lo que a continuación se muestran algunos ejemplos de las configuraciones realizadas:

- MSW2: Configuración de puertos truncal

  ![PORTS](images/ports_01.png)

- MSW5: Configuración de puertos truncal

  ![PORTS](images/ports_02.png)

- SW1: Configuración de puertos de acceso para los dispositivos finales y truncal

  ![PORTS](images/ports_03.png)

- MSW3: Configuración de puertos de acceso para el servidor web y truncal

  ![PORTS](images/ports_04.png)

- MSW1: Configuración de puertos de acceso para ambos servidores DHCP y truncal

  ![PORTS](images/ports_05.png)

## VTP
Se realizó la configuración del protocolo VTP, donde se determinó que el switch server sería el MSW4, ingresando sus respectivos comandos de la siguiente manera:

  ![VTP](images/vtp_01.png)

Por lo que en consecuencia, se procedió a la configuración de todos los demás switches de la topología, siendo estos los clientes del mismo protocolo como se muestra a continuación:

  ![VTP](images/vtp_02.png)

Dando como credenciales que el dominio sería grupo2 y la contraseña redes2, esto como parte de la libertad proporcionada de colocar las mismas a nuestro criterio.

## VLAN

Iniciando esta configuración se tomó como base las VLAN's solicitadas, como se muestra a continuación en la tabla:

| Nombre       | Número |
| ------------ | ------ |
| Ventas       |   12   |
| Informatica  |   22   |
| ACentral     |   32   |
| BCentral     |   42   |
| CCentral     |   52   |
| DCentral     |   62   |
| ECentral     |   72   |

Para realizar esta configuración, se ingresaron las VLAN's respectivamente en el switch MSW4 mencionando anteriormente que este es el server del protocolo VTP, por lo que se muestran los comandos ingresados:

![VLAN](images/vlan_01.png)

Esta configuración, se aplicó en todos los switches clientes de la topología al aplicarse el protocolo vtp, estas VLAN's fueron trasmitidas a dichos switches.

## InterVLAN Routing

El enrutamiento interVLAN permite que los dispositivos en diferentes VLANs se comuniquen entre sí, lo que es esencial en estas redes para controlar el tráfico y mejorar la seguridad, por lo que se configuró sobre cada uno de los switches capa 3 3650 del centro de la topología de la siguiente manera:

- Configuración sobre MSW4: Se agrega el gateway 192.168.12.1 con máscara de subred 255.255.255.0, el 192.168.22.1 con máscara de subred 255.255.255.0, el 22.0.0.1 con máscara de subred 255.0.0.0, 32.0.0.1 con máscara de subred 255.0.0.0 y 52.0.0.1 con máscara de subred 255.0.0.0, el MSW2 se realizó de forma parecida con sus respectivas red:

  ![ROUTING](images/routing_01.png)

- Configuración sobre MSW3: Se agrega el gateway 192.168.22.4 con máscara de subred 255.255.255.0 para el servidor web, el 12.0.0.1 con máscara de subred 255.0.0.0, 22.0.0.1 con máscara de subred 255.0.0.0

  ![ROUTING](images/routing_02.png)

- Configuración sobre MSW1: Se agrega el gateway 192.168.12.3 con máscara de subred 255.255.255.0 para un servidor DHCP, el 192.168.22.3 con máscara de subred 255.255.255.0 para un servidor DHCP, el 22.0.0.1 con máscara de subred 255.0.0.0, 32.0.0.2 con máscara de subred 255.0.0.0 y 42.0.0.2 con máscara de subred 255.0.0.0

  ![ROUTING](images/routing_03.png)

## LACP (PortChannel)

Se realizó la configuración del PortChannel, donde es una técnica que se utiliza para combinar múltiples enlaces físicos en un solo enlace lógico de alta velocidad. Esto mejora la capacidad y la redundancia de la conexión entre dos dispositivos, como un switch y un servidor o entre dos switches, por lo que estos 2 ejemplos de comandos mostrados a continuación detalla como configurar el mismo:

- Configuración de un Switch 3650 para la realización del LACP, donde se agregan todas las VLAN's, añadiendo los puertos Gig1/0/1, Gig1/0/2 y Gig1/0/3:

  ![LACP](images/lacp_01.png)

- Configuración de un Switch 3560 para la realización del LACP, donde se agregan todas las VLAN's, añadiendo los puertos Fa0/1, Fa0/2 y Fa0/3:

  ![LACP](images/lacp_02.png)

## DHCP

Se realizó la configuración del protocolo DHCP en los 2 switches DHCP1 y DHCP2, donde se les ingresó las ip de forma estática, en conjunto con su respectivo gateway, DNS:

  ![DHCP](images/dhcp_01.png)

Añadiendo las 2 redes respecticas de cada VLAN, para poder asignar la ip de forma dinámica en cada servidor de la siguiente manera:

  ![DHCP](images/dhcp_02.png)

Este procedimiento se realizó en el servidor web para asignarle su ip de forma estática, este perteneciendo a la red 192.168.22.0 con ip 192.168.22.4 respectiva.

###### _2023 - Laboratorio de Redes de computadoras 2_
---
