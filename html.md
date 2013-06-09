# Forms & HTML

- [Criar um Form](#opening-a-form)
- [Proteção CSRF](#csrf-protection)
- [Criar form apartir de um model](#form-model-binding)
- [Labels](#labels)
- [Text, Text Area, Password e Hidden Fields](#text)
- [Checkboxes e Radio Buttons](#checkboxes-and-radio-buttons)
- [File Input](#file-input)
- [Drop-Down Lists](#drop-down-lists)
- [Buttons](#buttons)
- [Custom Macros](#custom-macros)

<a name="opening-a-form"></a>
## Criar um Form

**Criar um elemento Form**

	{{ Form::open(array('url' => 'foo/bar')) }}
		//
	{{ Form::close() }}


Por padrão, a Tag `method` do form será do tipo `POST`, porém você tem liberdade para espeficar um `method` diferente:

By default, a `POST` method will be assumed; however, you are free to specify another method:

	echo Form::open(array('url' => 'foo/bar', 'method' => 'put'))


> **Note:** Since HTML forms only support `POST`, `PUT` and `DELETE` methods will be spoofed by automatically adding a `_method` hidden field to your form.


Você também pode criar forms que apontam para rotas ou actions de controllers:

	echo Form::open(array('route' => 'route.name'))

	echo Form::open(array('action' => 'Controller@method'))
	
Se o seu Form vai aceitar o upload de arquivo, então adicione a opção `files` para o array, desta form:

	echo Form::open(array('url' => 'foo/bar', 'files' => true))

<a name="csrf-protection"></a>
## Proteção CSRF

Laravel fornece um método fácil para proteger sua aplicação de falsificações de requisições [cross-site](http://pt.wikipedia.org/wiki/Cross-site_scripting). Primeiro, um Token é gerado para a session do usuário, não se preocupe, isto é feito automaticamente, O Token CSRF será adicionado automaticamente a um campo do tipo hidden, Porém, se você quiser gerar o campo hidden, você pode usar o método `token`:

**Adicionando o Token CSRF para um Form**

	echo Form::token();

**Anexar um filtro CSRF para uma Rota**

	Route::post('profile', array('before' => 'csrf', function()
	{
		//
	}));

<a name="form-model-binding"></a>
## Form Model Binding

Frequentemente, você vai querer popular um form baseando-se no conteudo de um model, ao faze-lo, use o método `Form::model`


**Opening A Model Form**

	echo Form::model($user, array('route' => array('user.update', $user->id)))
Agora, Quando você gerar um elemento de form, como entrada de texto, o valor do campo input será automaticamente o mesmo do campo do model. Por Exemplo, para um campo do form nomeado como `email`,  o atributo `email` model usuario, seria definido como o value do input do form. Porém, 
Now, when you generate a form element, like a text input, the model's value matching the field's name will automatically be set as the field value. So, for example, for a text input named `email`, the user model's `email` attribute would be set as the value. However, there's more! If there is an item in the Session flash data matching the input name, that will take precedence over the model's value. So, the priority looks like this:

1. Session Flash Data (Old Input)
2. Explicitly Passed Value
3. Model Attribute Data

This allows you to quickly build forms that not only bind to model values, but easily re-populate if there is a validation error on the server!

> **Note:** When using `Form::model`, be sure to close your form with `Form::close`!

<a name="labels"></a>
## Labels

**Generating A Label Element**

	echo Form::label('email', 'E-Mail Address');

**Specifying Extra HTML Attributes**

	echo Form::label('email', 'E-Mail Address', array('class' => 'awesome'));

> **Note:** After creating a label, any form element you create with a name matching the label name will automatically receive an ID matching the label name as well.

<a name="text"></a>
## Text, Text Area, Password & Hidden Fields

**Generating A Text Input**

	echo Form::text('username');

**Specifying A Default Value**

	echo Form::text('email', 'example@gmail.com');

> **Note:** The *hidden* and *textarea* methods have the same signature as the *text* method.

**Generating A Password Input**

	echo Form::password('password');

<a name="checkboxes-and-radio-buttons"></a>
## Checkboxes and Radio Buttons

**Generating A Checkbox Or Radio Input**

	echo Form::checkbox('name', 'value');
	
	echo Form::radio('name', 'value');

**Generating A Checkbox Or Radio Input That Is Checked**

	echo Form::checkbox('name', 'value', true);
	
	echo Form::radio('name', 'value', true);

<a name="file-input"></a>
## File Input

**Generating A File Input**

	echo Form::file('image');

<a name="drop-down-lists"></a>
## Drop-Down Lists

**Generating A Drop-Down List**

	echo Form::select('size', array('L' => 'Large', 'S' => 'Small'));

**Generating A Drop-Down List With Selected Default**

	echo Form::select('size', array('L' => 'Large', 'S' => 'Small'), 'S');

**Generating A Grouped List**

	echo Form::select('animal', array(
		'Cats' => array('leopard' => 'Leopard'),
		'Dogs' => array('spaniel' => 'Spaniel'),
	));

<a name="buttons"></a>
## Buttons

**Generating A Submit Button**

	echo Form::submit('Click Me!');

> **Note:** Need to create a button element? Try the *button* method. It has the same signature as *submit*.

<a name="custom-macros"></a>
## Custom Macros

It's easy to define your own custom Form class helpers called "macros". Here's how it works. First, simply register the macro with a given name and a Closure:

**Registering A Form Macro**

	Form::macro('myField', function()
	{
		return '<input type="awesome">';
	});

Now you can call your macro using its name:

**Calling A Custom Form Macro**

	echo Form::myField();
