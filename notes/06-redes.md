# 📓 redes | anotações

esse documento contém anotações de conceitos e informações sobre redes, com o objetivo de facilitar o entendimento e fixação. 

---

## fundamentos

- uma **rede de computadores** é um conjunto de dispositivos que **interagem** entre si a fim de **trocar** recursos e informações.
- apenas a conexão à internet **não** garante a **comunicação** entre dispositivos: seria como estar no **mesmo país**, mas falar **idiomas diferentes**.
- é necessário algo que possibilite a **comunicação** entre eles — é necessário um **protocolo de rede**.
- um **protocolo** é um **conjunto de regras** que **possibilita** a comunicação entre dois dispositivos ou mais — é uma espécie de *língua ponte*.

---

## IP

- o **Internet Protocol** ou endereço de IP é o endereço associado a um dispositivo para comunicação com a rede. é composto por quatro números divididos por pontos. ex.: `192.168.1.10`

> [!NOTE] 
> **IPv4 e IPv6:**  
>   
> o formato **IPv4 (Internet Protocol Version 4)** é o mais comum descrito acima.  
> o formato **IPv6** é o sucessor do anterior e foi criado para suprir o seu eventual esgotamento de endereços.  
> 
> endereços **IPv6** possuem 128 bits de tamanho e são escritos em notação hexadecimal.  
> ex.: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`

---

### WAN, LAN e WLAN

- **WAN (Wide Area Network)**: é a rede exterior de longa distância, conecta diferentes redes.
- **LAN (Local Area Network)**: é a rede que conecta dispositivos em uma distância limitada com conexão via cabo entre os dispositivos e o roteador. ex.: doméstica, escola, empresa.
- **WLAN (Wireless Local Network)**: é uma rede **LAN** que utiliza conexão sem fio (**Wi-Fi**) ao invés de cabos.

> [!TIP] 
> **hosts e packets:**  
>   
> em uma rede, todo dispositivo conectado recebe o nome de **host (hospedeiro)**, e os dados transferidos são quebrados em pedaços menores conhecidos como **packets (pacotes)**.

--- 

## DNS

- Domain Name System funciona como uma lista telefônica, ele **traduz** os **nomes de domínios** em **números de IPs**, permitindo navegar na internet.
- em uma lista telefônica, busca-se o **nome do contato** para obter seu **número**, o DNS faz o mesmo.
- ao digitar o domínio de um site, o navegador busca o IP do domínio no seu provedor de DNS. 
- sem ele, seria preciso conhecer os números de IP dos sites ao invés de seus nomes.

> [!NOTE]   
> **exemplo:**  
>   
> `github.com` — domínio (*nome do contato*)  
> `140.82.112.4` — endereço IP (*número do contato*)

