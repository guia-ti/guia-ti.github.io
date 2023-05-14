# Lista de Códigos SIP

---

##  1xx—Respostas Provisórias  e Informativas
Indica o Status de uma chamada antes dela ser completada.

- 100 Trying  

    Indica que o dispositivo mais próximo do servidor recebeu uma solicitação e alguma ação será tomada em relação a isso.  
  
  
- 180 Ringing  

    Indica que o agente do usuário ( Softphone, ATA, TelefoneIP, Asterisk, etc .. ) recebeu uma solicitação e esta chamando o destino. Geralmente através de toques, Alertas sonoros, notificaçoes ou mensagens.  

- 181 Call is Being Forwarded  

    Um servidor pode ou não, opcionalmente, usar esse status para avisar se uma chamada esta sendo encaminhada para um ou vários destinos.  

- 182 Queued  

    Indica que o destino está temporariamente indisponível, então a chamada foi colocada em uma fila até que o mesmo esteja disponível. Um servidor poderá também mandar múltiplas respostas 182 para manter a situação da fila atualizada.  

- 183 Session in Progress  

    Essa resposta pode ser usada para mandar informações extras de uma chamada que ainda esta sendo criada.  

- 199 Early Dialog Terminated  

    Pode ser usada pelo Servidor VoIP (Ex: PBX) para indicar que o fluxo das entidades SIP ( Incluindo o cliente, agente usuário ) terminou muito cedo.  

## 2xx—Respostas bem sucedidas
Indica se uma solicitação foi completada com êxito, e qual foi o comportamento gerado.

- 200 OK  

    Indica que a solicitação foi completada com sucesso. 

- 202 Accepted  

    Indica que a solicitação foi aceita para ser processada. Porem o processamento ainda não foi completado. 
    >_Obsoleto - No momento essa resposta não é mais utilizada nos sistemas mais recentes_.

- 204 No Notification  

    Indica que a solicitação teve sucesso, porem a chamada não vai ter uma notificação.
    >Ex: Ligou em um 0800, Completou no sistema, dando um OK, porém não vai notificar o Cliente, agente ou usuário. Sem alertas e notificações.  

## 3xx—Respostas de redirecionamento. 
Informações sobre um novo local do usuário ou destinos alternativos, serviços alternativos que possam prosseguir com a sessão.

- 300 Multiple Choices  

    O endereço IP ou chamada foi redirecionado a varias opções para o usuário ou cliente escolher, cada uma indo para um local diferente, enquanto o usuário ou agente do usuário pode selecionar a opção desejada e redirecionar a solicitação de chamada até esse local. 
    > Talvez esta mensagem apareça em alguns casos de URA, por Exemplo.  

- 301 Moved Permanently  

    O usuário não pode mais ser encontrado no endereço em que foi mandada a solicitação ou chamada.  

- 302 Moved Temporarily  

    O usuário não pode completar a chamada porque o endereço solicitado esta temporariamente desabilitado, fora de serviço ou expirou.  
    > Pode haver informação adicional de um novo destino de contato.

- 305 Use Proxy  

    A fonte solicitada só pode ser alcançada através de um Proxy.

- 380 Alternative Service  

    A chamada falhou, porem alternativas para esse endereço estão sendo mostrados no corpo da mensagem.  

## 4xx—Respostas de falha ou erros no cliente

- 400 Bad Request  

    A solicitação não pode ser compreendida devido a uma sintaxe errada. 
    > Numero digitado errado, cadastro errado, registro errado, ou a operadora - GVT, Net Virtua, etc - ter algum tipo de bloqueio, ou até mesmo um erro interno na rede do cliente. 

- 401 Unauthorized  

    O pedido não pode ser completado pois não foi possível autenticar o usuário.  

- 402 Payment Required

    Mensagem informada por uma operadora VOIP ( Terminação ) quando a rota fica sem saldo.
    >Caso esta mensagem apareça, será necessário contato com a operadora.  

- 403 Forbidden  

    O servidor compreendeu a solicitação, porem esta se negando a completar ou aceita-la.
    >Muitas vezes este erro ocorre em alguma das pontas devido à uma configuração errada de uma rota de saída, ou uma rota de entrada. Ou algum tipo de bloqueio em uma das pontas.  

- 404 Not Found  

    O servidor reporta que o usuário solicitado não existe no domínio de destino. 
    >Essa resposta também aparece caso alguma informação, como o domínio, ou mesmo um número de entrada, não seja igual ao especificado no servidor, no destino ou na ponta que fez a solicitação.  

- 405 Method Not Allowed  

    O método especificado no pedido foi compreendido, porem não é permitido pelo endereço que esta recebendo a solicitação.  

- 406 Not Acceptable

    O recurso identificado pelo pedido só é capaz de gerar e completar respostas SIP que possuam características específicas. Não foi aceito conforme o que foi enviado na solicitação. 
    >Um exemplo disso é solicitar um serviço de SMS para um ponto que não possua tecnologia para isso.  

- 407 Proxy Authentication Required

    Este código é enviado na maioria das vezes por operadoras VOIP, terminações, números de entrada. 
    >O motivo geralmente ou é algum bloqueio no Firewall, por parte deles, ou alguma configuração de rede que está bloqueando o solicitante.  
    
- 408 Request Timeout  

    Não foi possível encontrar o usuário a tempo. O servidor não pôde enviar ou receber uma resposta dentro de um limite adequado de tempo. 
    >Geralmente quando uma rede de um servidor cai, esta é a mensagem dada.  

- 409 Conflict  

    Usuário já esta registrado 
    >_Esta mensagem é OBSOLETA. Aparece apenas em versões mais antigas de Sistemas VOIP_ ( Ex. Asterisk )   

- 410 Gone  

    Era uma vez uma informação que vivia aqui, porem não vive mais.
    A mensagem informa que sabe da existencia informação existiu, porém ela não se encontra mais no local.  

- 411 Length Required  

    O servidor não vai aceitar nenhum pedido sem um conteúdo / duração valida.
    Esta mensagem apareceria creio eu, em casos de Telemarketing por exemplo. Em que os áudios e mensagens enviadas precisam ter sua duração exata especificada.  

- 412 Conditional Request Failed  

    A pre-condição dada não foi cumprida e falhou.  

- 413 Request Entity Too Large  

    O corpo do pedido é longo demais.  

- 414 Request-URI Too Long  

    A sequencia de caracteres informados é maior do que o servidor esta disposto a interpretar.  

- 415 Unsupported Media Type  

    Corpo da solicitação esta em um formato não suportado. Algum CODEC pode estar faltando. Com o CODEC ideal, este erro pode ser resolvido e a Media passar a ser suportada.  

- 416 Unsupported URI Scheme  

    Um erro que ocorre caso a sequencia dos dados / caracteres informados para registro esteja incorreta, ou seja utilizado um texto com uma fonte diferente da interpretada pelo servidor...
    Pode também aparecer caso uma rota esteja mal configurada, por exemplo, um número entrante esteja em um servidor, porém em uma das pontas, estiver alcançando um Gateway diferente do q deveria... Comum em rotas / números vindo de fora... Internacionais.  

- 417 Unknown Resource-Priority  

    Teve uma solicitação para dar prioridade a um recurso, porem nao teve um local, um destino para essa opção encaminhar a solicitação.  

- 420 Bad Extension  

    Protocolo SIP - Servidor não compreendeu extensão usada. Este erro geralmente está relacionado às configurações da rota, em algum dos pontos. 

- 421 Extension Required  

    Esse servidor precisa usar uma extensão especifica. Como por exemplo, um servidor que requer uma conexão ponto a ponto...  

- 422 Session Interval Too Small  

    O tempo de expiração contem uma duração abaixo do tempo minimo. Provavelmente este erro vá aparecer em algum esquema de Telemarketing, ou URA Reversa. Não sabemos ao certo. 

- 423 Interval Too Brief  

    Tempo de expiração do recurso muito curta. Explicação é a mesma do erro 422. Alguma URA ou esquema de Telemarketing. 

- 424 Bad Location Information  

    O local do pedido foi mal informado ou insatisfatório. 

- 428 Use Identity Header  

    A politica do servidor requer um cabeçalho de identificação via URI, e o mesmo não foi informado. 

- 429 Provide Referrer Identity  

    O servidor nao recebeu um token valido no pedido. Este erro deve acontecer se o servidor exigir algum tipo de token de identificação para ser enviada junto com a solicitação... 

- 430 Flow Failed  

    Uma corrente especifica para um agente do usuário falhou, porem outros podem ter sucedido. Essa resposta aparece quando existem conexões entre proxies. 

- 433 Anonymity Disallowed  

    A solicitação foi recusada porque era anonima. 

- 436 Bad Identity-Info  

    O pedido possui um cabeçalho de identificação porem o esquema URI do mesmo nao pode ser diferenciado e compreendido. 

- 437 Unsupported Certificate  

    O servidor nao pode validar um certificado para o domínio que realizou o pedido. 

- 438 Invalid Identity Header  

    O servidor obteve um certificado valido do domínio que fez o pedido, porem não conseguiu uma assinatura válida. 

- 439 First Hop Lacks Outbound Support  

    O proxy de saída que o usuário esta tentando registrar nao suporta a opção de saida do RFC 5626, porem o registrador suporta.  

- 470 Consent Needed  

    A fonte do pedido não tem permissão para realizar tal pedido. O recipiente em q a fonte se encontra não o autorizou a completar a ação. É necessario q o mesmo autorize.  

- 480 Temporarily Unavailable  

    Local solicitado se encontra indisponível no momento.  

- 481 Call/Transaction Does Not Exist  

    O servidor recebeu um pedido porem ele nao bate com nenhum dialogo ou transação.  

- 482 Loop Detected.  

    O servidor detectou um Loop.  

- 483 Too Many Hops  

    Foi detectado um número limite de pulos entre pontos, e este limite foi excedido.  

- 484 Address Incomplete  

    A solicitação URI esta incompleta.  

- 485 Ambiguous  

    A solicitação URI pode conter vários significados. Provavelmente este erro se resolva caso a URI seja mais específica e com mais parametros...  

- 486 Busy Here  

    Destino esta ocupado.  

- 487 Request Terminated  

    Solicitação cancelada pelo destino ou por algum agente entre a fonte do pedido e o destino.  

- 488 Not Acceptable Here  

    Alguns aspectos da descrição da sessão ou a solicitação URI nao são aceitas.  

- 489 Bad Event  

    O servidor nao entendeu o pacote de evento informado no cabeçalho de eventos. Um exemplo, caso algum ATA envie uma notificação de algum recurso, tal como o "keep-alive", e o q recebeu esta notificação não compreenda a mesma, pode retornar esta mensagem.  

- 491 Request Pending  

    O servidor já possui pedidos do mesmo dialogo.  

- 493 Undecipherable  

    O pedido contem um corpo MIME encriptado no qual o recipiente nao pôde decriptar.   

- 494 Security Agreement Required  

    O servidor recebeu um pedido no qual uma negociação no mecanismo de segurança é necessário e a resposta contem uma lista de mecanismos de segurança para o solicitador escolher.

## 5xx—Erros de falha do servidor.

- 500 Server Internal Error  

    O servidor nao pôde completar o pedido por causa de uma condição inesperada.  

- 501 Not Implemented  

    O servidor nao possui a habilidade de completar o pedido, isso ocorre porque o servidor que realizou tal pedido nao reconhece o método do pedido.  

- 502 Bad Gateway  

    O servidor esta agindo como uma gateway ou proxy e recebeu uma resposta invalida de um servidor - Gateway invalido ou proxy invalido / Defeituoso.  

- 503 Service Unavailable  

    O servidor esta em manutenção ou temporariamente sobrecarregado e nao pode processar o pedido.  

- 504 Server Time-out  

    O servidor tentou acessar outro servidor porem nao recebeu uma resposta.  

- 505 Version Not Supported  

    A versão do protocolo SIP no pedido nao é suportada pela versão do servidor.  

- 513 Message Too Large  

    O tamanho da mensagem é maior do que o servidor é capaz de processar.  

- 580 Precondition Failure  

    O servidor é incapaz ou nao quer obedecer ou aceitar as condições / restrições especificadas no pedido.  

## 6xx—Respostas de Falhas Globais.
  

- 600 Busy Everywhere  

    Todos os destinos possíveis estão ocupados.   

- 603 Decline  

    O destino nao deseja participar da chamada ou não pode aceita-la. Adicionalmente o destino também sabe que nao existem outros destinos alternativos - Como por exemplo uma caixa postal.  

- 604 Does Not Exist Anywhere  

    O servidor possui a informação de que o solicitado nao existe em lugar algum.  

- 606 Not Acceptable  

    O agente do usuário contactou com sucesso porem alguns aspectos da descrição da sessão, como por ex. a media requisita, velocidade da internet, ou o estilo em que o endereço foi digitado, nao são aceitas.  

--- 

# Referencias 

- [InforSolutions - Códigos de Resposta e Erro SIP](https://www.inforsolutions.com.br/ticket_sol/knowledgebase.php?article=2)  
