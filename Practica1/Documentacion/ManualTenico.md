## Elección de escenario con mejor resultado de convergencia\*\*

### PVST

La convergencia para este protocolo se realizó de la siguiente manera:

#### Red Primaria

![Convergencia PVST](images/pvst1.png)

Se comenzó a hacer ping desde el host 1 al host 2, se procedió a apagar el enlace que permitía la comunicación entre estas dos vlans y se observó que el tiempo de convergencia fue de 35 segundos.

![Convergencia PVST](images/pvst2.png)

#### Red Básicos

![Convergencia PVST](images/pvst3.png)

Se realizó el mismo procedimiento que en la red primaria, los pings fueron desde 192.168.22.1 hacia 192.168.22.2, se apagó el enlace que permitía la comunicación entre estas dos vlans y se observó que el tiempo de convergencia fue de 34 segundos.

![Convergencia PVST](images/pvst4.png)

#### Red Diversificado

![Convergencia PVST](images/pvst5.png)

Al igual que en la medición de convergencias anteriores, los pings fueron desde 192.168.32.1 hacia 192.168.32.3, se apagó el enlace que permitía la comunicación entre estas dos vlans y se observó que el tiempo de convergencia fue de 33.20 segundos.

![Convergencia PVST](images/pvst6.png)

### Rapid PVST

Rapid PVST es un protocolo que permite la convergencia de la red de manera más rápida que PVST, esto se debe a que se implementa el protocolo RSTP en cada vlan, por lo que se tiene un árbol de expansión por cada vlan.

Para hacer uso de este modo se configuró en todos los switch lo siguiente:

![Configuracion Rapid PVST](images/rpvst1.png)

Lo cual es la configuración para que los switches utilicen el protocolo Rapid PVST en lugar de PVST.

Para todas las redes se realizó el mismo procedimiento que en PVST, se utilizaron los mismos hosts y se apagaron los mismos enlaces, los resultados fueron los siguientes:

#### Red Primaria

La convergencia fue inmediata, no se perdió ningún paquete.

![Convergencia Rapid PVST](images/rpvst2.png)

#### Red Básicos

La convergencia fue inmediata, no se perdió ningún paquete.

![Convergencia Rapid PVST](images/rpvst3.png)

#### Red Diversificado

La convergencia fue inmediata, no se perdió ningún paquete.

Algo que se observó en esta red es que al momento de activar el enlace que se había apagado, se perdió un paquete.

![Convergencia Rapid PVST](images/rpvst4.png)

| Escenario | Protocolo Spanning-Tree | Red Primaria | Red Básicos | Red Diversificado |
| --------- | ----------------------- | ------------ | ----------- | ----------------- |
| 1         | PVST                    | 35s          | 34s         | 33.20s            |
| 2         | Rapid PVST              | 0s           | 0s          | 0s                |

### Elección de escenario

Se eligió el escenario 2, ya que la convergencia es inmediata, no se pierden paquetes y se tiene un árbol de expansión por cada vlan, lo cual permite que la red sea más eficiente. Por lo que tomando como referencia un caso de la vida real, el protocolo Rapid PVST es el más adecuado para la mayoría de las redes y en este caso, para la red que se está trabajando.
