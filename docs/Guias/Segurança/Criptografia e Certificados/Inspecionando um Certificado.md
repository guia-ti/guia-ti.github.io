---
created: 2023-05-14T20:52:15-03:00
updated: 2023-05-15T10:58:16-03:00
title: Inspecionando um Certificado
tags: [ guia, criptografia, certificado, x509, openssl ]
---
# Inspecionando um Certificado 

Para inspecionar um certificado digital vamos utilizar o comando `openssl`.
O objetivo é ter acesso a todas as informações presentes no mesmo e filtrar caso necessário informações específicas.

## Pré-Requisitos
- Um certificado TLS/SSL
  > Pode ser baixado o certificado [neste link](https://raw.githubusercontent.com/guia-ti/guia-ti.github.io/main/docs/Arquivos/guia-ti.hev.dev.br.crt)
- Acesso ao binário `openssl`

## Validando o Conteúdo de um Certificado

Para inspecionar todo o conteúdo do certificado podemos utilizar o comando abaixo
```bash 
openssl x509 -noout -text -in certificado.crt
```

O comando começa especificando qual módulo do `openssl` será utilizado, neste acaso `x509` para o padrão de certificado que será fornecido na entrada. Após isso são especificadas as opções abaixo para determinar o arquivo de entrada e as informações a serem exibidas na saída:

- `-noout` 
  Limita a saída a somente os campos solicitados, é util para remover informações irrelevantes da saída do comando.

- `-text`
  Define que o todos os dados do certificado devem ser exibidos em formato texto. 
  
  - `-in <CERTIFICADO>`
  Informa o arquivo de entrada que será analisado.

### Opções Adicionais 
Há também outras opções que podem ser utilizadas, todas elas estão descritas no manual do `openssl` ou pelo comando `openssl x509 -help`, vale ao menos citar algumas das opções. 

- `-dates` 
  Exibe um conjunto de datas de validade do certificado
- `-enddate`
  Exibe a data de expiração do certificado
- `-startdate`
  Exibe a data de inicio da validade do certificado 
- `-subject`
  Exibe o commonName (CN) do certificado.
- `-issuer`
  Exibe a organização emissora do certificado.
- `-ext <EXTENSÃO>` 
  Exibe as extensões adicionais do certificado. Por exemplo os nomes alternativos (SAN).
```text
openssl x509 -noout -ext subjectAltName -in <CERTIFICADO>
```
![[Pasted image 20230514220423.png]]
### Exemplo de Execução
Abaixo um exemplo do retorno do comando usando como entrada o arquivo `guia-ti.hev.dev.br.crt`.
![[Pasted image 20230514215159.png]]

### Conteúdo Completo do Certificado
```text
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            03:76:4c:0b:91:c7:5c:80:f9:cb:a0:9e:53:49:13:1f:f0:3f
        Signature Algorithm: sha256WithRSAEncryption
        Issuer: C = US, O = Let's Encrypt, CN = R3
        Validity
            Not Before: May 14 00:09:31 2023 GMT
            Not After : Aug 12 00:09:30 2023 GMT
        Subject: CN = guia-ti.hev.dev.br
        Subject Public Key Info:
            Public Key Algorithm: rsaEncryption
                RSA Public-Key: (2048 bit)
                Modulus:
                    00:ab:c7:1b:0c:ed:c6:01:f8:ea:a9:b3:cf:08:17:
                    4f:a2:cb:7c:34:c4:66:12:e6:ef:f3:98:17:79:c9:
                    65:ee:66:4c:1f:9a:92:7d:33:ee:07:fa:2e:15:62:
                    f7:b4:f3:1f:d5:4f:2e:b1:67:a8:49:42:bf:e3:cc:
                    9a:b7:30:46:c2:68:f5:28:a9:64:69:6f:4c:4b:64:
                    24:c9:dc:ed:46:9f:a4:1f:c2:ef:6f:36:d0:bc:69:
                    27:b8:e2:d6:18:70:40:2c:b4:f5:ee:8f:f7:0d:8c:
                    6e:03:92:e7:5d:d6:3e:bc:bb:c9:5b:28:10:a0:5a:
                    f6:37:f5:e1:9e:15:23:72:6e:8e:69:01:09:a4:8c:
                    a4:c9:d7:db:05:01:90:48:4b:90:20:8c:38:7a:0a:
                    60:74:79:18:26:30:8e:60:0b:17:b9:24:a0:80:df:
                    3f:14:00:d3:09:e7:34:47:35:63:7c:54:d2:a0:9d:
                    e1:57:d1:cb:13:d3:3c:30:24:97:8e:ea:34:00:9f:
                    cc:6c:0c:6a:f7:54:bc:5e:60:dc:46:31:c2:09:de:
                    d9:c3:e3:63:1e:8f:1c:c5:90:90:e8:da:86:be:7d:
                    f1:c3:1f:1a:86:69:9b:0b:e0:b2:0c:47:08:c8:92:
                    59:2b:66:2f:fa:a1:38:a1:2f:10:65:f6:97:fd:16:
                    87:33
                Exponent: 65537 (0x10001)
        X509v3 extensions:
            X509v3 Key Usage: critical
                Digital Signature, Key Encipherment
            X509v3 Extended Key Usage:
                TLS Web Server Authentication, TLS Web Client Authentication
            X509v3 Basic Constraints: critical
                CA:FALSE
            X509v3 Subject Key Identifier:
                63:4E:15:85:56:5A:A4:94:02:C2:16:42:A4:A5:97:9A:38:02:57:97
            X509v3 Authority Key Identifier:
                keyid:14:2E:B3:17:B7:58:56:CB:AE:50:09:40:E6:1F:AF:9D:8B:14:C2:C6

            Authority Information Access:
                OCSP - URI:http://r3.o.lencr.org
                CA Issuers - URI:http://r3.i.lencr.org/

            X509v3 Subject Alternative Name:
                DNS:guia-ti.hev.dev.br
            X509v3 Certificate Policies:
                Policy: 2.23.140.1.2.1
                Policy: 1.3.6.1.4.1.44947.1.1.1
                  CPS: http://cps.letsencrypt.org

            CT Precertificate SCTs:
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : B7:3E:FB:24:DF:9C:4D:BA:75:F2:39:C5:BA:58:F4:6C:
                                5D:FC:42:CF:7A:9F:35:C4:9E:1D:09:81:25:ED:B4:99
                    Timestamp : May 14 01:09:31.709 2023 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:44:02:20:4E:FA:0D:E9:08:B3:91:D9:87:42:12:4C:
                                AA:C2:99:F5:46:93:63:48:EC:69:18:87:4A:B8:B0:3A:
                                00:42:6F:FF:02:20:36:B1:D2:CF:C6:32:60:A1:8D:FF:
                                E1:CF:69:E4:08:69:A2:6E:0A:B0:FE:A7:62:D9:E2:62:
                                5B:C8:C0:54:89:35
                Signed Certificate Timestamp:
                    Version   : v1 (0x0)
                    Log ID    : AD:F7:BE:FA:7C:FF:10:C8:8B:9D:3D:9C:1E:3E:18:6A:
                                B4:67:29:5D:CF:B1:0C:24:CA:85:86:34:EB:DC:82:8A
                    Timestamp : May 14 01:09:31.747 2023 GMT
                    Extensions: none
                    Signature : ecdsa-with-SHA256
                                30:44:02:20:11:20:48:53:36:DA:99:3F:96:2D:B9:DC:
                                C8:6C:DB:9F:F8:69:16:4D:B9:77:D4:5E:97:D4:2C:5F:
                                88:D1:20:A4:02:20:7C:33:1D:DC:26:51:50:FC:F8:EA:
                                BE:0B:64:A8:10:81:FD:B3:57:F3:5E:FC:DF:8E:7B:44:
                                4C:AB:43:62:0A:74
    Signature Algorithm: sha256WithRSAEncryption
         7f:77:bb:ef:0e:a6:06:be:7f:40:c2:de:0d:7b:96:ce:f6:64:
         7c:44:73:9f:18:54:09:7e:df:cd:2f:dd:14:e3:db:7a:d7:5f:
         1a:f5:41:38:65:3b:ca:ae:d1:a3:c4:1f:d5:21:ab:ea:bd:94:
         1c:14:4a:62:f0:fd:27:d6:67:fe:a6:57:70:4e:6c:bc:0c:51:
         7f:29:a4:22:f2:1a:e9:8f:07:5a:5d:63:45:47:23:ea:50:f0:
         73:22:0f:4d:b5:16:c3:f3:4c:f4:f8:52:02:14:c4:f8:7c:84:
         46:49:e8:27:c2:55:06:b8:05:8c:19:83:f7:45:74:eb:e3:b1:
         30:6d:e2:ee:0b:9c:6f:d8:56:0f:25:99:a3:0f:5c:b8:23:63:
         09:15:4a:5e:66:49:05:2f:31:e5:17:fc:ab:99:20:9e:2e:0f:
         0f:5a:c7:9c:4e:70:e7:b8:f7:70:5c:1e:ae:e2:ff:56:99:44:
         7b:7d:9d:8c:92:77:9d:3c:cd:a1:70:4a:fb:f3:87:8e:4c:13:
         ae:65:3c:5b:ab:68:b2:db:00:0e:28:cd:f9:10:95:8c:3e:37:
         44:c5:74:13:b7:9e:6e:0e:72:04:08:9f:09:81:16:fb:97:2c:
         e2:68:23:ea:16:7c:d7:ed:e3:b3:81:ce:6e:ef:d4:90:6a:2c:
         56:f4:67:54


```