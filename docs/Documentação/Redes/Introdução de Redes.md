---
title: Introdução de Redes
created: 2023-05-14T20:09:19-03:00
updated: 2023-05-14T20:41:56-03:00
---
tags: #redes #OSI #protocolos


# Introdução de Redes

---

> [Hebert Silva](https://site.hev.dev.br) @hebertluiz

## Modelo OSI


No modelo OSI temos 7 divisões para a estrutura de rede.

Podemos lista-las como camadas da seguinte forma:

1. Física
2. Enlace ou Ligação de dados 
3. Rede
4. Transporte 
5. Sessão 
6. Apresentação 
7. Aplicação

---

### 1 - Camada Física

É nessa camada que temos as interações físicas dos meios onde os dados trafegam podendo ser tangíveis como  cobre e fibra óptica ou ondas eletromagnéticas no caso de rádios como Bluetooth e Wifi.

Na camada física não temos estrutura, somente o fluxo bruto dos bits no meio físico. O que temos nesse caso são as especificações funcionais das interfaces sejam elas elétricas, ópticas ou mecânicas. Essa etapas serve como base para transportar os sinais para as camadas superiores.  


### 2 - Camada de Enlace ou Ligação de dados.

Aqui começamos a ter estrutura e um certo nível de resiliência aos dados trafegados. Nesta camada detectamos e, opcionalmente, corrigimos erros que acabam ocorrendo no meio físico. Sejam esses erros causados por interferência ou falhas no próprio meio em si. Há também o controle do fluxo dos dados e o protocolo de comunicação entre dois ou mais sistemas diretamente conectados.


### 3 - Camada de Rede 

Aqui é onde a mágica acontece, nessa camada temos a implementação do endereçamento entre hosts não diretamente conectados e a interface entre redes distintas. É aqui que os roteadores trabalham, mapeando pacotes entre redes distintas. Aqui vamos encontrar o que move a internet, o protocolo IP (IPv4 e  IPv6)


### 4 - Camada de Transporte 

Aqui temos os dois protocolos mais comuns de comunicação UDP e TCP. Esta camada age como interface entre as camadas de 1 a 3 onde a preocupação é a maneira em que os dados são transmitidos e as camadas 5 a 7 onde a preocupação é com os dados contidos nos pacotes endereçando-os as aplicações corretas. Temos também a divisão da sessão em pacotes 

#### `UDP`
  Neste protocolo não temos controle sobre o recebimento e envio dos pacotes, de forma bem simples podemos dizer que não é confiável no sentido de não haver ordenação de pacotes fora de ordem, não há validação de recebimento e não é possível o reenvio de pacotes perdidos.

#### `TCP`
  Podemos dizer que este é um protocolo confiável. Há o suporte para reordenação de pacotes fora de ordem, temos controle de recebimento com confirmação do recebimento e a possibilidade de reenvio de pacotes perdidos. Neste caso temos garantias maiores de que o pacote enviado ao receptor chegou corretamente e foi processado.

### 5 - Camada de Sessão 

A camada de sessão controla os diálogos ou conexões entre computadores. Nessa camada temos implementações para suspender, reiniciar, salvar um ponto de retorno ou terminar sessões entre dois dispositivos. Funcionalidades que não estão disponíveis por padrão no protocolo IP.

Normalmente é implementada diretamente na aplicação em ambientes que usam RCP (Remote Procedure Calls). Em palavras simples são cenários onde uma ação do computador A causa a execução de uma sub-rotina em um outro espaço de endereçamento, normalmente em outro computador B na mesma rede 

Atualmente em sistemas TCP/IP, a camada de sessão não existe por si só. Suas funcionalidades são implementadas como parte do protocolo TCP na camada de Transporte. 


### 6 - Camada de Apresentação  

É nesta camada que fazemos a tradução entre formatos e codificações para transmissão. Como referencia podemos realizar as seguintes ações com os dados nesta camada.

- Compressão
- Encriptação 
- Codificação

Em resumo, temos aqui a transformação dos dados em um formato que a camada de aplicação possa aceitar evitando interferências por conta de formatos e codificações.

### 7 - Camada Aplicação

Aqui temos o topo do modelo OSI que será utilizado para comunicação entre usuários e maquinas. Temos implementados também os protocolos que permitem essa comunicação. 

Nesta camada tudo tem relação com o software e pode ser descrito em um protocolo que implementa uma função de alto nível com os dados. 

Os protocolos abaixo são alguns dos presentes nessa camada: 

- HTTP
- SMTP
- FTP
- Telnet
- SIP
- DNS 


---


## Finalizando  

Com essa base podemos partir para os pontos específicos, os protocolos em si e as especificações técnicas que regem os mesmos.

Vamos ver com detalhes os protocolos abaixo:

- Ethernet 
- IPv4
- TCP/IP
- HTTP
- SIP


## Referencias 

- [Windows Network Architecture and the OSI Model - docs.microsoft.com](https://docs.microsoft.com/en-US/windows-hardware/drivers/network/windows-network-architecture-and-the-osi-model)  
- [Modelo OSI - wikipedia.org](https://pt.wikipedia.org/wiki/Modelo_OSI)