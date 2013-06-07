# Artisan CLI(Command Line - Linha de comando)

- [Introdução](#introduction)
- [Utilização](#usage)

<a name="introduction"></a>
## Introdução

- [PTBR]
Artisan é o nome da interface por commando de linha, incluido com o laravel. Ele fornece um numero de comando uteis para se utilizar em ambiente de desenvolvimento de sua aplicação.

-[ENG]
Artisan is the name of the command-line interface included with Laravel. It provides a number of helpful commands for your use while developing your application. It is driven by the powerful Symfony Console component.

<a name="usage"></a>
## Utilização

[PTBR]
Para visualizar uma lista de todos os comando disponivel do Artisan, você pode usar o comando `list`

[ENG]
To view a list of all available Artisan commands, you may use the `list` command:

[PTBR]
**Listagem de todos os comando disponiveis**

[ENG]
**Listing All Available Commands**

	php artisan list
[PTBR]
Cada comando também inclue um "help" que mostra e descreve os argumentos e opções disponíveis do comando. Para visualizar a tela de help, simplismente preceda o nome do comando com  `help`:

**Visualizando a tela de Help para um comando**
  php artisan help migrate


[ENG]
Every command also includes a "help" screen which displays and describes the command's available arguments and options. To view a help screen, simply precede the name of the command with `help`:

**Viewing The Help Screen For A Command**

	php artisan help migrate


[PTBR]
Você pode especificar o ambiente de configuração que deverá ser executado com a opção `--env`:

**Espeficicando o ambiente de configuração**
	php artisan migrate --env=local


[ENG]
You may specify the configuration environment that should be used while running a command using the `--env` switch:

**Specifying The Configuration Environment**

	php artisan migrate --env=local

[PTBR]
Você pode também visualizar a versão atual da sua instalação Laravel, utilizando a opção `--version`:
You may also view the current version of your Laravel installation using the `--version` option:

**Exibindo sua versão atual do Laravel**
	
	php artisan --version

**Displaying Your Current Laravel Version**

	php artisan --version


[PENDENDO DE CORREÇÕES E REVISÃO FINAL]
