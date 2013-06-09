# Controllers

- [O Basico sobre Controllers](#basic-controllers)
- [Filtros nos Controllers](#controller-filters)
- [RESTful Controllers](#restful-controllers)
- [Recurso de Controllers](#resource-controllers)
- [Manipulação de métodos indefinidos](#handling-missing-methods)

<a name="basic-controllers"></a>
## O Basico sobre controllers

Ao invés de definir toda a lógica do seu nível de rotas em um unico arquivo `routes.php`, você pode querer organiza todo o 
comportamente dos controllers que tipicamente estão armazenados no diretório `app/controllers`, e este diretório está registrado na opção `classmap` do seu arquivo padrão `composer.json`


Aqui está um exemplo básico de uma classes de controller:

	class UserController extends BaseController {

		/**		 
		 * Exibi o perfil para o usuário
		 */
		public function showProfile($id)
		{
			$user = User::find($id);

			return View::make('user.profile', array('user' => $user));
		}

	}

Todos os Controllers deveram estender a classe `BaseController`. o `BaseController` está também armazenado no diretório `app/controllers`
e pode ser usado um local para compartilhar a lógica dos controllers. o `BaseController``estende a classe `Controller` da framework. Agora, podemos rotear a ação deste controller:

	Route::get('user/{id}', 'UserController@showProfile');

Você pode escolher por empacotar ou organizar sua aplicação usando namespaces do PHP, simplismente use o nome completo da classe quando definir a rota.

	Route::get('foo', 'Namespace\FooController@method');

Você também pode especificar um nome de rota para controller:


	Route::get('foo', array('uses' => 'FooController@method',
											'as' => 'name'));

To generate a URL to a controller action, you may use the `URL::action` method:

	$url = URL::action('FooController@method');

You may access the name of the controller action being run using the `currentRouteAction` method:

	$action = Route::currentRouteAction();

<a name="controller-filters"></a>
## Controller Filters

[Filters](/docs/routing#route-filters) may be specified on controller routes similar to "regular" routes:

	Route::get('profile', array('before' => 'auth',
				'uses' => 'UserController@showProfile'));

However, you may also specify filters from within your controller:

	class UserController extends BaseController {

		/**
		 * Instantiate a new UserController instance.
		 */
		public function __construct()
		{
			$this->beforeFilter('auth');

			$this->beforeFilter('csrf', array('on' => 'post'));

			$this->afterFilter('log', array('only' =>
								array('fooAction', 'barAction')));
		}

	}

You may also specify controller filters inline using a Closure:

	class UserController extends BaseController {

		/**
		 * Instantiate a new UserController instance.
		 */
		public function __construct()
		{
			$this->beforeFilter(function()
			{
				//
			});
		}

	}

<a name="restful-controllers"></a>
## RESTful Controllers

Laravel allows you to easily define a single route to handle every action in a controller using simple, REST naming conventions. First, define the route using the `Route::controller` method:

**Defining A RESTful Controller**

	Route::controller('users', 'UserController');

The `controller` method accepts two arguments. The first is the base URI the controller handles, while the second is the class name of the controller. Next, just add methods to your controller, prefixed with the HTTP verb they respond to:

	class UserController extends BaseController {

		public function getIndex()
		{
			//
		}

		public function postProfile()
		{
			//
		}

	}

The `index` methods will respond to the root URI handled by the controller, which, in this case, is `users`.

If your controller action contains multiple words, you may access the action using "dash" syntax in the URI. For example, the following controller action on our `UserController` would respond to the `users/admin-profile` URI:

	public function getAdminProfile() {}

<a name="resource-controllers"></a>
## Resource Controllers

Resource controllers make it easier to build RESTful controllers around resources. For example, you may wish to create a controller that manages "photos" stored by your application. Using the `controller:make` command via the Artisan CLI and the `Route::resource` method, we can quickly create such a controller.

To create the controller via the command line, execute the following command:

	php artisan controller:make PhotoController

Now we can register a resourceful route to the controller:

	Route::resource('photo', 'PhotoController');

This single route declaration creates multiple routes to handle a variety of RESTful actions on the photo resource. Likewise, the generated controller will already have stubbed methods for each of these actions with notes informing you which URIs and verbs they handle.

**Actions Handled By Resource Controller**

Verb      | Path                  | Action       | Route Name
----------|-----------------------|--------------|---------------------
GET       | /resource             | index        | resource.index
GET       | /resource/create      | create       | resource.create
POST      | /resource             | store        | resource.store
GET       | /resource/{id}        | show         | resource.show
GET       | /resource/{id}/edit   | edit         | resource.edit
PUT/PATCH | /resource/{id}        | update       | resource.update
DELETE    | /resource/{id}        | destroy      | resource.destroy

Sometimes you may only need to handle a subset of the resource actions:

	php artisan controller:make PhotoController --only=index,show

	php artisan controller:make PhotoController --except=index

And, you may also specify a subset of actions to handle on the route:

	Route::resource('photo', 'PhotoController',
					array('only' => array('index', 'show')));

<a name="handling-missing-methods"></a>
## Handling Missing Methods

A catch-all method may be defined which will be called when no other matching method is found on a given controller. The method should be named `missingMethod`, and receives the parameter array for the request as its only argument:

**Defining A Catch-All Method**

	public function missingMethod($parameters)
	{
		//
	}
