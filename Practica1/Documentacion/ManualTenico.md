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

| Escenario | Protocolo Spanning-Tree | Red Primaria | Red Básicos | Red Diversificado |
| --------- | ----------------------- | ------------ | ----------- | ----------------- |
| 1         | PVST                    | 35s          | 34s         | 33.20s            |
| 2         | Rapid PVST              |              |             |                   |
