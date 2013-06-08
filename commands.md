# Artisan Development

- [Introdução](#introduction)
- [Construção de um comando](#building-a-command)
- [Registrando um comando](#registering-commands)
- [Chamada para outros comandos](#calling-other-commands)

<a name="introduction"></a>
## Introdução

[PTBR]
 Além dos comandos fornecidos com o Artisan, você pode construir seus próprios comandos para trabalhar com sua aplicação. Você pode armazenar seus comandos costumizados no diretorio `app/commands`; porém, você está livre para escolher o localização, enquanto seus comandos possam ser baseados nas configurações do `composer.json`.
 

[ENG]
In addition to the commands provided with Artisan, you may also build your own custom commands for working with your application. You may store your custom commands in the `app/commands` directory; however, you are free to choose your own storage location as long as your commands can be autoloaded based on your `composer.json` settings.



<a name="building-a-command"></a>
## Construindo um comando

### Gerando a class

[PTBR]
Para criar um novo comando, você pode usar o `command:make` pelo Artisan, que irá gerar um help do comando para inicialização: 


[ENG]
To create a new command, you may use the `command:make` Artisan command, which will generate a command stub to help you get started:

**Gerar um novo commando Class**

	php artisan command:make FooCommand

[PTBR]
Por padrão, gerar comandos armazenará

[ENG]
By default, generated commands will be stored in the `app/commands` directory; however, you may specify custom path or namespace:

	php artisan command:make FooCommand --path="app/classes" --namespace="Classes"


### Escrevendo o comando
### Writing The Command

[PTBR]
Uma vez que seu comando gerado, você deverá preencher as propriedades `name` e `description` da classe, que serão utilizados ao exibir o comando `list`.

[ENG]
Once your command is generated, you should fill out the `name` and `description` properties of the class, which will be used when displaying your command on the `list` screen.

[PTBR]
O método `fire` será chamado quando seu comando for executado. Você pode  colocar qualquer lógica de comando neste método

[ENG]
The `fire` method will be called when your command is executed. You may place any command logic in this method.

### Opções e argumentos

[PTBR]
Os métodos `getArguments` e `getOptions` são onde você pode definir qualquer argumento ou opções de seu comando recebido.
ambos os métodos retornam um array de comandos, que são descrito em uma lista de opções de array.

[ENG]
The `getArguments` and `getOptions` methods are where you may define any arguments or options your command receives. Both of these methods return an array of commands, which are described by a list of array options.

[PTBR]
Ao definir `argumento`, os valores de definição do array seram representados da seguinte forma:

[ENG]
When defining `arguments`, the array definition values represent the following:

	array($name, $mode, $description, $defaultValue)


[PTBR]
O argumento `mode` pode ser qualquer um dos seguintes: `InputArgument::REQUIRED` ou `ÌnputArgument::OPTIONAL`,

Ao definir `options`, os valores de definição do array seram representados da seguinte forma:


[ENG]
The argument `mode` may be any of the following: `InputArgument::REQUIRED` or `InputArgument::OPTIONAL`.

When defining `options`, the array definition values represent the following:

	array($name, $shortcut, $mode, $description, $defaultValue)

[PTBR]
para `òptions`, o argumento `mode` pode ser: `ÌnputOption::VALUE_REQUIRED`, `InputOption::VALUE_OPTIONAL`, `
InputOption::VALUE_IS_ARRAY`,`InputeOption::VALUE_NONE`,
o mode `VALUE_IS_ARRAY`  indica que o switch pode ser usado várias vezes ao chamar o comando:

[ENG]
For options, the argument `mode` may be: `InputOption::VALUE_REQUIRED`, `InputOption::VALUE_OPTIONAL`, `InputOption::VALUE_IS_ARRAY`, `InputOption::VALUE_NONE`.

The `VALUE_IS_ARRAY` mode indicates that the switch may be used multiple times when calling the command:

	php artisan foo --option=bar --option=baz

[PTBR]
A opção `VALUE_NONE` indica que o option é simplesmente usado como um "Switch":

The `VALUE_NONE` option indicates that the option is simply used as a "switch":

	php artisan foo --option

### Obtendo a entrada do comando

Enquanto seu comando é executado, vocè obviamente precisará acessar o valor para o arguments e as options aceitas por sua
aplicação. Para faze-o, pode-se usar os métodos `àrgument` e `option`:

While your command is executing, you will obviously need to access the values for the arguments and options accepted by your application. To do so, you may use the `argument` and `option` methods:


** Obter valor de um arguments de comando**

	$value = $this->argument('name');

**Obtér todos os arguments**

	$arguments = $this->argument();

**Obtér o valor de uma option de comando**

	$value = $this->option('name');

**Obtér todoas as Options**

	$options = $this->option();


### Escrita

[PTBR]
Para enviar uma saida para o console, pode-se usar os métodos `info`, `comment`, `question` e `error`. cada método
utiliza as cores ANSI adequadas para o seu propósito.

[ENG]
To send output to the console, you may use the `info`, `comment`, `question` and `error` methods. Each of these methods will use the appropriate ANSI colors for their purpose.

**Enviando informações via console**

	$this->info('Display this on the screen');


**Enviando uma mensagem de erro via console**

	$this->error('Something went wrong!');

### Perguntas frequentes

[PTBR]
Você pode também usar os métodos `ask` e `confirm` para solicitar ao usuário a entrada de dados:

[ENG]
You may also use the `ask` and `confirm` methods to prompt the user for input:

**Perguntar ao user via input**
**Asking The User For Input**

	$name = $this->ask('What is your name?');

**Perguntar ao usuário via Input Secret

**Asking The User For Secret Input**

	$password = $this->secret('What is the password?');

**Asking The User For Confirmation**

	if ($this->confirm('Do you wish to continue? [yes|no]'))
	{
		//
	}

You may also specify a default value to the `confirm` method, which should be `true` or `false`:

	$this->confirm($question, true);

<a name="registering-commands"></a>
## Registering Commands

Once your command is finished, you need to register it with Artisan so it will be available for use. This is typically done in the `app/start/artisan.php` file. Within this file, you may use the `Artisan::add` method to register the command:

**Registering An Artisan Command**

	Artisan::add(new CustomCommand);

If your command is registered in the application [IoC container](/docs/ioc), you may use the `Artisan::resolve` method to make it available to Artisan:

**Registering A Command That Is In The IoC Container**

	Artisan::resolve('binding.name');

<a name="calling-other-commands"></a>
## Calling Other Commands

Sometimes you may wish to call other commands from your command. You may do so using the `call` method:

**Calling Another Command**

	$this->call('command.name', array('argument' => 'foo', '--option' => 'bar'));
