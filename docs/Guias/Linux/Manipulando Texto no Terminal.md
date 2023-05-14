---
title: Manipulando Texto
created: 2023-05-14T19:59:06-03:00
updated: 2023-05-14T19:59:06-03:00
---


# Manipulando Texto no terminal

---

> [Hebert Silva](https://site.hev.dev.br) @hebertluiz

--- 

## Pré-requisitos  

As seguintes ferramentas disponíveis no sistema:

* `sed`: Editor de sequencia de caracteres.  
* `awk`: Linguagem de programação para processamento de texto.  
* `tr`:  Manipula caracteres, apagando ou substituindo.  
* `column`: Formata texto em colunas.  
* `grep`: Filtra e mostra linhas com base no padrão informado.  
* `mount`: Monta e lista partições do sistema.  

Acesso aos arquivos abaixo e pastas abaixo:

* `/etc/resolv.conf`
* `/tmp/`
* `/etc/profile.d/`

Neste processo iremos usar os arquivos abaixo:

[Lista DDD Brasil](https://www.anatel.gov.br/dadosabertos/PDA/Codigo_Nacional/PGCN.csv) LATIN-1  
[Lista DDD Brasil](https://raw.githubusercontent.com/guia-ti/guia-ti.github.io/main/docs/Arquivos/ddd.csv) UTF-8  
[pprint_csv](https://raw.githubusercontent.com/guia-ti/guia-ti.github.io/main/docs/Arquivos/pprint_csv)

Recomendo também, conhecimento prévio de navegação via terminal em ambiente Linux.

---  

## Esclarecendo Termos  

* `EXPRESSÃO`: Forma de script ou linguagem específica de uma aplicação. Pode representar operações matemáticas ou ações programáticas.  
* `REGEX`: Linguagem utilizada para representar sequencias de caracteres, normalmente chamada de Expressões Regulares. 
* `NEWLINE`: Quebra de linha utilizada para levar o cursor para linha abaixo.  




--- 

## Preparando o ambiente 

Para iniciar vamos baixar alguns arquivos que iremos utilizar, como exemplo abaixo deixo os arquivos fonte com os links de origem:

```bash
echo "Baixando primeiro a lista de DDDs UTF-8"
wget -q https://raw.githubusercontent.com/guia-ti/guia-ti.github.io/main/docs/Arquivos/ddd.csv -O /tmp/ddd.csv

echo "Baixando o script pprint_csv"
wget -q https://raw.githubusercontent.com/guia-ti/guia-ti.github.io/main/docs/Arquivos/pprint_csv -O /tmp/pprint_csv


# Dando permissões de execução ao arquivo pprint_csv.sh
chmod +x /tmp/pprint_csv /tmp/pprint_csv
```

Com os arquivos no `ddd.csv` e `pprint_csv` na pasta `/tmp/` podemos prosseguir. 



--- 

## Manipulando texto com `sed`

#### Introdução  - Sed

Neste ponto vamos manipular o arquivo `/etc/resolv.conf` com o conteúdo abaixo como exemplo:

`/etc/resolv.conf`

```
nameserver 1.1.1.1
nameserver 8.8.8.8
```

Podemos usar o comando abaixo para trocar o 1.1.1.1 por 8.8.4.4:
```shell
# sed 's/1.1.1.1/8.8.4.4/g' /etc/resolv.conf
nameserver 8.8.4.4
nameserver 8.8.8.8
# 
```


#### Indo Mais a Fundo  - Sed

A aplicação aceita os seguintes formatos:
```
sed --expression 'EXPRESSÃO' <ARQUIVO>
sed 'EXPRESSÃO' <ARQUIVO> 
cat <ARQUIVO> | sed 'EXPRESSÃO' [--expression  'EXPRESSÃO']
sed 'EXPRESSÃO' -i <ARQUIVO> 
```

Vemos acima que o `sed` trabalha sempre com uma expressão e ela pode ser dividida em até 3 partes:  

* Ação:  
É onde podemos dizer ao `sed` o que desejamos fazer entre as ações disponíveis temos as seguintes: 
    * `s` Usado para substituir, ele espera uma cadeia de caracteres para busca e outra para substituição. Pode ser utilizado com expressões regulares. ele pode ser utilizado com o parâmetro `g` para aplicar a substituição em todas as ocorrências e não só na primeira.
    * `d` Apaga o conteúdo buscado da saída.  

* Padrão:  
É definido como qualquer sequencia de caracteres e pode ser representado por sequencias literais ou <abbr title="Expressões Regulares">Regex</abbr>  

* Parâmetros: Algumas ações do sed esperam ou aceitam opções que controlam seu comportamento. Como exemplo temos a ação `s` que pode ser controlada pelo parâmetro `g`.  

```bash
# A linha abaixo irá substituir todas as ocorrências de PADRAO por SUBSTITUTO 
sed 's/PADRAO/SUBSTITUTO/g' <ARQUIVO> 

# A linha abaixo irá substituir somente a primeira ocorrência de PADRAO por SUBSTITUTO 
sed 's/PADRAO/SUBSTITUTO/' <ARQUIVO> 

```  

O comando `sed` aceita múltiplas expressões no mesmo comando, para isso podemos usar o parâmetro `-e` ou `--expression` seguido de uma expressão, esse ciclo pode ser repetido quantas vezes desejarmos realizando as ações desejadas.



---

#### Concluindo - Sed

O comando sed sempre retorna as ações realizadas para o terminal, dai podemos apontar a saída para um arquivo. Se desejarmos manipular um arquivo diretamente podemos utilizar a opção `-i` ou `--in-place[=SUFFIX]` se fornecermos um sufixo para esta opção faremos o backup do arquivo. 

```bash
# Realiza a operação no arquivo criando um backup nomeado  /etc/resolv.conf.bkp
sed 's/1.1.1.1/8.8.4.4/g' --in-place=.bkp /etc/resolv.conf

```

Se quiser aprender mais sobre o comando pode acessar o link [GNU Sed](https://www.gnu.org/software/sed/manual/html_node/) onde irá encontrar toda a documentação da ferramenta.


---

## Cortando colunas com AWK

#### Introdução - AWK  

Assim como o sed o AWK é uma aplicação bem complexa, iremos focar somente no seu uso para manipular colunas. 
Conforme podemos ver abaixo utilizando o comando `mount` como fonte do texto a ser manipulado.

```
# mount | awk '{print $1, $3}'
sysfs /sys
proc /proc
devtmpfs /dev
securityfs /sys/kernel/security
tmpfs /dev/shm
devpts /dev/pts
tmpfs /run
tmpfs /sys/fs/cgroup
[...]

# mount 
sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
devtmpfs on /dev type devtmpfs (rw,nosuid,size=1008128k,nr_inodes=252032,mode=755)
securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)
tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,mode=755)
tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
[...]
```



---  

#### Indo Mais a Fundo - AWK

O comando `awk` trabalha com diversos parametros mas vamos trabalhar somente com o `-F` ou `--field-separator`. Ele servirá para informar qual o separador de colunas do nosso texto, por padrão o separador é o caractere espaço ` `.

Assim como o `sed` podemos utilizar dois formatos de entrada sendo eles:  
* Redirecionamento de saída: PIPE  
`cat <ARQUIVO> | awk 'EXPRESSÃO'`
* Caminho do arquivo:  
`awk 'EXPRESSÃO' <ARQUIVO>`

No anterior usamos o delimitador espaço do comando `mount` para mostrar somente os campos 1 e 3 que respectivamente são o `block device` e o ponto de montagem. Este tipo de manipulação pode nos ajudar a visualizar informações e filtrar conteúdos.  

O `awk` recebe as ações a serem realizadas entre aspas simples dentro de chaves. `awk '{AÇÃO}' <ARQUIVO>`, neste caso podemos usar como exemplo a ação `print`, ela recebe um ou mais parâmetros posicionais separados por virgula, cada um deles indicando uma coluna a ser impressa na tela.

```awk
awk '{print $n[,$n...]}
```

--- 

#### Concluindo - AWK  

O universo de possibilidades dentro do AWK é muito grande, existe toda uma linguagem de manipulação de texto interpretada por esta ferramenta. Em muitos cenários ela pode substituir o uso do `sed` e de outras ferramentas no terminal. Fica o convite a quem se interessar para dar um olhada no link [Linguagem AWK](https://guialinux.uniriotec.br/awk/)




--- 

## Ferramentas Mais Básicas  

Descrever algo dessa forma pode ser uma afronta a que tanto as usa, mas mesmo sendo bem simples ou limitadas no que fazem elas merecem espaço aqui por conta do poder que nos dão de buscar e manipular texto.

Vamos falar de `grep`, `tr` e `column`. Possivelmente já conhece ou até já usou alguma delas.


#### `tr`

É uma ferramenta utilizada para trocar ou apagar caracteres únicos, pode ser usada para formatar e até ofuscar o conteúdo de documentos de texto.

Vamos ver dois exemplos:
* Apagar:  
Para apagar algum caractere podemos usar o parâmetro `-d` seguido de uma lista de caracteres a serem removidos podendo conter também nessa lista caracteres de controle como NEWLINE e TAB ou Expressões Regulares.  
```ini
echo "Teste do TR"| tr -d ' '
TestedoTR
```

* Trocar caracteres:  
Podemos substituir caracteres passando dois grupos de caracteres ao `tr` com isso podemos por exemplo substituir espaços em um texto por traços `-`. Formato: `tr ' ' '-'`  
No exemplo abaixo vamos trocar os espaços por traços e também a letra e por E.
```ini
echo "Teste do TR"| tr ' e' '-E'
TEstE-do-TR
```

#### `grep`  

É utilizado para filtrar o conteúdo de arquivos retornando na saída padrão o texto desejado.
Podemos utiliza-lo passando o filtro que desejamos entre aspas, vale lembrar que este filtro pode conter Expressões Regulares dando a possibilidade de filtrar textos complexos.

O parâmetro `-v` pode ser utilizado para inverter o filtro e só nos retornar o conteudo que não combina com o filtro utilizado. No caso abaixo podemos tirar todas as linhas que contem `cgroup` do retorno do comando `mount`.
```
mount |grep -v 'cgroup'
```

E o comando abaixo sem o `-v` irá listar somente as linhas que contem a palavra `cgroup`.
```
mount |grep 'cgroup'
```

#### `column`

É a mais simples das ferramentas, podemos usa-la para formatar texto em colunas com a opção `-t`. Por padrão o separador de colunas é o caractere espaço mas podemos muda-lo caso necessário com a opção `-s` ou `--separator` que aceita um ou mais caracteres como separadores.  
O comando abaixo irá espaçar a saída do comando `mount` deixando-o mais legível.
```
mount |column -t
```

## Conclusão

Vamos agora juntar um pouco do que aprendemos em um pequeno script em Shell/Bash.

A ideia é usar essas ferramentas para mostrar no terminal um arquivo CSV de forma mais legível.

```bash
#!/bin/bash

infile="$*"
if [ -n "$infile" ]
then
    if [ -f "$infile" -a -r $infile ]  
    then
        sed -e 's/[,;]\([,;]\)/ \1/g;' "$infile" \
            | tr -d \"\'\` \
            | column -t -s\;, \
            | less 
        
    else 
        printf -- "ERROR: File does not exists or isn't readable.\n\t"
        printf -- "%s\n\n" "$infile"
        exit 1 # File not found ERROR 1
    fi 
else 
    printf -- "No input file specified\n\tPlease inform an input file:\n" 
    printf -- "\t\tEx.: %s <PATH_TO_FILE>\n\n" "$0"
    exit 2 # No input file ERROR 2
fi

exit 0
```

Com esse arquivo podemos exercitar um pouco de nosso conhecimento de manipulação de texto executando o comando abaixo.

```
/tmp/pprint_csv /tmp/ddd.csv
```

Se quiser usar esse comando no seu terminal pode copiar o arquivo `/tmp/pprint_csv.sh` para a pasta `/etc/profile.d/`. Isso irá carregar a função `pprint_csv` no seu terminal sempre que logar.

```
sudo cp -av /tmp/pprint_csv.sh /etc/profile.d/
```

---

## Links de Referência  

[RegExr](https://regexr.com/)  
[Gnu Sed s command](https://www.gnu.org/software/sed/manual/html_node/The-_0022s_0022-Command.html#The-_0022s_0022-Command)  
[Linguagem AWK](https://guialinux.uniriotec.br/awk/)  
[GitHub Hebert Silva](https://github.com/hebertluiz/)


