*15 de junho de 2021 365Tech*

Lolcat é um utilitário que exibe resultados do seus comandos no console nas cores de arco-íris.

## Instalação

=== "Linux"
    ```sh
    apt-get install ruby  [APT based Systems]
    yum install ruby	  [Yum based Systems]
    ```
=== "MacOs"

    ```sh
    $ brew install lolcat
    ```


Verifique se o Ruby foi instalador verificando sua versão:
```sh
ruby --version

# ruby 2.7.0p0 (2019-12-25 revision 647ee6f091) [x86_64-linux-gnu]
```

Baixe e instale a versão mais recente do lolcat do repositório git usando os seguintes comandos:

```sh 
unzip master.zip
```
```sh
cd lolcat-master/bin
```
```sh
gem install lolcat
```



Assim que o lolcat estiver instalado, você pode verificar a versão:

```sh
lolcat --version

# lolcat 100.0.1 (c)2011 moe@busyloop.net
```

Para obter ajuda, você pode usar:
```sh
lolcat --help
```

## Exemplos
Este utilitário pode ser usado com vários comandos ou scripts, por exemplo:
```sh
$ ps | lolcat
```

Para exibir a data, você pode usar:
```sh
$ date | lolcat
```

Ao usar o calendario:
```sh
$ cal | lolcat
```

O exemplo de ping:
```sh
$ ping google.com -c10 | lolcat
```

É possivel criar efeitos de banner, basta exibir o texto passando os seguintes parametros:
```sh
$ echo "365Tech DevOps" | lolcat -a -d 500
```


!!! tip "Dica"
    *Lolcat é apenas para você deixar seus resultados mais divertidos, mas pode ser muito ultil quando você quiser destacar alguma notificação quando estiver rodando seus scripts.* 

