# 📡 comandos de rede no Linux

este documento é composto por descrições de comandos no contexto de redes em um ambiente Linux e é complementar às [anotações sobre redes](notes/06-redes.md).

---

 ```bash 
 $ ip a  # exibe informações detalhadas sobre as interfaces de rede
 ```

 
- `lo` — é a interface *loopback* que o sistema usa para se comunicar consigo mesmo, sempre exibe o IP `127.0.0.1`  
- `eth0` — é a primeira interface Ethernet (cabeada), conecta o sistema à rede local (LAN) ou externa (WAN). possui nomenclaturas alternativas, como `enp0s3` 
- `docker0` — essa interface é exibida se Docker estiver instalado

> [!IMPORTANT] 
> **MAC Address:**  
> 
> o endereço **MAC (Media Access Control)** é conhecido como o **endereço físico** de um dispositivo, e está gravado a nível de hardware associado ao **NIC (Network Interface Card)**.  
> é possível encontrá-lo junto ao `link/ether`.

- `inet` — é onde se localiza o endereço **IPv4**, exibe um para cada interface disponível
- `inet6` — refere-se ao endereço **IPv6**, a linha seguida por `scope link` indica este endereço na interface `eth0`, usado para comunicação apenas na rede local *(link-local)*.

