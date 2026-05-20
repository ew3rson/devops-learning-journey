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

- o **Internet Protocol** ou endereço de IP é o endereço associado a um dispositivo para comunicação com a rede. é composto por **quatro octetos** (ou bytes) divididos por pontos. ex.: `192.168.1.10`

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
- **WLAN (Wireless Local Area Network)**: é uma rede **LAN** que utiliza conexão sem fio (**Wi-Fi**) ao invés de cabos.

> [!TIP] 
> **hosts e packets:**  
>   
> em uma rede, todo dispositivo conectado recebe o nome de **host (hospedeiro)**, e os dados transferidos são quebrados em pedaços menores conhecidos como **packets (pacotes)**.

--- 

## como um roteador funciona

- o processo de roteamento funciona de forma **similar** a de um serviço de **entrega de correspondências** — ao enviar uma carta para alguém, essa carta passa por um processo de envio que **prioriza** o seu **destino geral** (estado/cidade); a partir daí, o destino é **filtrado** de acordo com as regiões específicas do endereço (bairro, CEP), para então chegar no endereço principal: a rua.   
- em redes, é a *routing table* que define o processo de entrega e que contém as informações e as regras que dizem ao roteador como realizar a entrega dos pacotes para o destino informado.  
- a *routing table* pode ter uma regra que diz que "deve-se enviar o pacote para o **roteador B**, para que chegue à **rede A**"; ou pode não possuir regra nenhuma, utilizando a forma padrão, que costuma direcionar o tráfego para a internet.  

### saltos ou *hops*

- é a nomenclatura que define a forma de **medir** a locomoção/distância dos pacotes na rede.
- um salto representa a etapa em que um pacote passa por um dispositivo intermediário, como um roteador.
- se um pacote deve passar por **dois** roteadores para ir da **origem A até o destino B**, diz-se que a distância é de **dois saltos**.

---

## gateway, subnet e CIDR

### gateway

- é a **porta de saída** de uma rede — quando um dispositivo quer se comunicar com algo **fora** da sua rede local, ele envia o pacote para o gateway.
- o roteador (dispositivo) costuma estar associado ao gateway, pois exerce funções similares.

### sub-rede e máscara de sub-rede

- **subnet (sub-rede)** é uma divisão de uma rede maior em blocos menores — permite organizar e isolar grupos de dispositivos dentro de uma mesma rede.
- a **máscara de sub-rede** é o que distingue essa divisão: ela indica quais bits do endereço IP identificam a **rede** e quais identificam o **dispositivo (host)**.

```
IP:      192.168.1.50
máscara: 255.255.255.0
		 ^^^^^^^^^^^ ^ 
	        rede     host
```

- assim, o dispositivo consegue determinar se o destino está **dentro** da rede (comunicação direta) ou **fora** dela (precisa passar pelo gateway).
- no exemplo acima, qualquer IP que comece com `192.168.1.` está na mesma rede. qualquer outro vai para o gateway.
- a criação de sub-redes é crucial para **organizar grandes redes** de forma eficaz, pois a divisão auxilia na gestão e na solução de problemas.

### CIDR

- **CIDR (Classless Inter-Domain Routing)** é uma notação compacta para representar uma subnet — substitui a notação longa da máscara por um número após uma barra.
- o número indica **quantos bits** do endereço IP pertencem à rede.

```
255.255.255.0 

em binário:
11111111.11111111.11111111.00000000

= 24 bits ou 3 octetos/bytes "ligados" -> /24
```

- a notação compacta indica quantos octetos/bytes são **dedicados ao endereço de rede**
- os **zeros**, que correspondem à seção de hosts, indicam o **número de endereços** que podem ser atribuídos a **dispositivos**.

#### calculando hosts disponíveis

- apesar de um octeto possuir **256 combinações** possíveis, **nem todas** podem ser atribuídas aos hosts.

> [!NOTE] 
> em toda subnet, **dois endereços** estão **reservados** — o da **própria rede** e o endereço de **broadcast**:  
> 
> 1. **network address:** onde todos os bits de host são **zero** -> `ex.: 192.168.1.0`
> 2. **broadcast address:** onde todos os bits de host são **um** -> `ex.: 192.168.1.255`   
> 
> dessa forma, é possível atribuir endereços de IP do `192.168.1.1` ao `192.168.1.254` com uma máscara `255.255.255.0`.

##### exemplo:

```
IP: 123.12.24.0/23
bytes/octetos: 4*8 = 32 bits

cálculo:
1. 32-23 = 9    # subtrai o prefixo CIDR do total de bits
2. 2^9   = 512  # calcula o número total de endereços na sub-rede
3. 512-2 = 510  # subtrai os 2 endereços reservados para a rede e broadcast
```

| notação | máscara         | hosts disponíveis              |
|---------|-----------------|--------------------------------|
| `/8`    | 255.0.0.0       | (2^24) - 2 = ~16 milhões       |
| `/16`   | 255.255.0.0     | (2^16) - 2 = 65.534            |
| `/24`   | 255.255.255.0   | (2^8) - 2 = 254                |

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

