# Configurações

- [Introdução](#introduction)
- [Ambiente de configuração](#environment-configuration)
- [Modo de manutenção](#maintenance-mode)

<a name="introduction"></a>
## Introdução

Todas as arquivos de configuração para o Laravel Framework estão armazenadas no diretório `app/config`. Cada opção de todos os arquivos estão documentadas,  então sinta-se avontade para ler e familiarizar-se com as opções disponiveis para você.


All of the configuration files for the Laravel framework are stored in the `app/config` directory. Each option in every file is documented, so feel free to look through the files and get familiar with the options available to you.

[PTBR]
As vezes você pode precisar acessar as configurações em "tempo de execução", você pode fazer isso usando a classe `Config`:

[ENG]
Sometimes you may need to access configuration values at run-time. You may do so using the `Config` class:


**Acessar um valor de configuração**

	Config::get('app.timezone');

Você também pode especificar um valor padrão para retornar se a opção de configuração não existir:

You may also specify a default value to return if the configuration option does not exist:

	$timezone = Config::get('app.timezone', 'UTC');


Note que a sintax "ponto" pode ser usada para acessar um valor de vários arquivos. Você também pode definir um valor de configuração em "tempo de execução".


Notice that "dot" style syntax may be used to access values in the various files. You may also set configuration values at run-time:


**Definir um valor de configuração**

	Config::set('database.default', 'sqlite');

<a name="environment-configuration"></a>

##Ambiente de configuração

[PTBR]
Muitas vezes é util ter diferentes valores de configurações baseados no ambiente da aplicação para executa-la. 
por exemplo, você quer usar um driver de cache diferente em sua maquina de desenvolvimento local do que esta no servidor
de produção. Isto é facil para realizar usando as configurações baseadas no ambiente.

[ENG]
It is often helpful to have different configuration values based on the environment the application is running in. For example, you may wish to use a different cache driver on your local development machine than on the production server. It is easy to accomplish this using environment based configuration.

[PTBR]
Simplismente crie uma pasta dentro do diretório `config` que corresponde ao seu nome de ambiente, tal como `local`, em seguida, crie um arquivo de configuração que deseja substituir e especifique as opções para o seu ambiente, Por exemplo, substitua o driver de cache para o ambiente local, você deve criar um arquivo `cache.php` dentro de `app/config/local` com o seguinte conteúdo:


[ENG]
Simply create a folder within the `config` directory that matches your environment name, such as `local`. Next, create the configuration files you wish to override and specify the options for that environment. For example, to override the cache driver for the local environment, you would create a `cache.php` file in `app/config/local` with the following content:

	<?php

	return array(

		'driver' => 'file',

	);

> **Note:** Não utilize o nome de ambiente como 'testing', pois é reservado para Testes unitários.

[PTBR]
Perceba que você não tem que especificar sempre as options que estão no arquivo base de configuração, mas somente as options que você sobrescreveu. Os arquivos de configuração do ambiente "substituem" os arquivos base.

[ENG]
Notice that you do not have to specify _every_ option that is in the base configuration file, but only the options you wish to override. The environment configuration files will "cascade" over the base files.


[PTBR]
Em seguida, nos precisamos instruir o framewor como determinar qual ambiente está sendo executado. Por padrão o ambiente sempre está como `production`. porém, você pode configurar outros ambiente dentro do arquivo `bootstrap/start.php` que está na raiz de sua instalação. Neste arquivo você irá procurar pela chamada `$app->detectEnvironment`. O Array fornecido para o método é utilizado para determinar o ambiente atual. Você pode adicionar nomes de ambiente e maquinas para o Array, conforme for necessário.


[ENG]
Next, we need to instruct the framework how to determine which environment it is running in. The default environment is always `production`. However, you may setup other environments within the `bootstrap/start.php` file at the root of your installation. In this file you will find an `$app->detectEnvironment` call. The array passed to this method is used to determine the current environment. You may add other environments and machine names to the array as needed.

    <?php

    $env = $app->detectEnvironment(array(

        'local' => array('your-machine-name'),

    ));

[PTBR]
Você também pode fornecer uma `Clausula` para o método `detectEnvironment`, permitindo que você implemente seu próprio ambiente de detecção.


[ENG]
You may also pass a `Closure` to the `detectEnvironment` method, allowing you to implement your own environment detection:

	$env = $app->detectEnvironment(function()
	{
		return $_SERVER['MY_LARAVEL_ENV'];
	});

[PTBR]
Você pode acessar o ambiente atual através o método `environment`:


You may access the current application environment via the `environment` method:

**Acessando o ambiente atual da aplicação**

	$environment = App::environment();

<a name="maintenance-mode"></a>
## Modo de manutenção
[PTBR]
Quando sua aplicação está em modo de manutenção, uma view costumizada será exibida para todas as rotas dentro de sua aplicação. Isto facilita a "desabilitamento" de sua aplicação enquanto está atualizando. Uma chamada para método `App:down` já está presente em seu arquivo `app/start/global.php, A resposta deste método será enviada quando sua aplicação estiver em modo de manutenção.

[ENG]
When your application is in maintenance mode, a custom view will be displayed for all routes into your application. This makes it easy to "disable" your application while it is updating. A call to the `App::down` method is already present in your `app/start/global.php` file. The response from this method will be sent to users when your application is in maintenance mode.

Para habilitar o modo de manutençao, simplismente execute o comando `down` pelo Artisan:

	php artisan down

Para desabilitar o modo de manutenção, use o comando `up`:

	php artisan up

Para mostrar uma view constumizada quando sua aplicação está em modo de manutenção, você pode adicionar algo parecido como o seguinte no arquivo `app/start/global.php`:


	App::down(function()
	{
		return Response::view('maintenance', array(), 503);
	});
