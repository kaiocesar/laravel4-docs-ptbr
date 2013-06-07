# Cache

- [Configuração](#configuration)
- [Utilização de cache](#cache-usage)
- [Incrementação & decrementação](#increments-and-decrements)
- [Sessões de Caches](#cache-sections)
- [Cache de banco de dados](#database-cache)

<a name="configuration"></a>
## Configuração

[PTBR]
Laravel fornece uma API unificada para vários sistemas de cache. A configuração do cache está localiza em `app/config/cache.php`. Neste arquivo você pode especificar o driver de cache que você gostaria de utilizar como default para sua aplicação. Laravel suporta os populares backends de cache como [Memcached](http://mencahed.org) e [Redis](http://redis.io), externamente.

[END]
Laravel provides a unified API for various caching systems. The cache configuration is located at `app/config/cache.php`. In this file you may specify which cache driver you would like used by default throughout your application. Laravel supports popular caching backends like [Memcached](http://memcached.org) and [Redis](http://redis.io) out of the box.

[PTBR]
O arquivo de configuração de cache também contém várias outras opções, que estão documentados no próprio arquivo, Para configurações corretamente, certifique-se de ler sobre essas opções. Por padrão, Laravel está  configurado para usar o driver de cache `file`, que armazenará a serialização, cacheando os objetos em um arquivo. Para aplicação maiores, é recomendado que você utilize o cache na memoria como Memcached ou APC.

[ENG]
The cache configuration file also contains various other options, which are documented within the file, so make sure to read over these options. By default, Laravel is configured to use the `file` cache driver, which stores the serialized, cached objects in the filesystem. For larger applications, it is recommended that you use an in-memory cache such as Memcached or APC.


<a name="cache-usage"></a>
##Utilização de cache 

**Armazenando um item no cache**

	Cache::put('chave', 'valor', $variavel);


**Armazenando um item no cache "se o item não existir"**

	Cache::add('chave', 'valor', $variavel);


**Checando a existem de cache**

	if (Cache::has('valor'))
	{
		//
	}


**Obtendo valor do item do cache**

	$valor = Cache::get('chave');


**Obtendo um item ou retornando um valor padrão**


	$valor = Cache::get('chave', 'valor padrão');

	$valor = Cache::get('chave', function() { return 'valor padrão'; });

**Storing An Item In The Cache Permanently**

**Armazendando um item no cache permanentimente**

	Cache::forever('chave', 'valor');
[PTBR]
Derrepente você pode querer recuperar um item do cache, mais também armazar um valor padrão se a requisiçao do item não existir. Você pode fazer isto usando o metodo `Cache::remember`:

[ENG]
Sometimes you may wish to retrieve an item from the cache, but also store a default value if the requested item doesn't exist. You may do this using the `Cache::remember` method:

	$value = Cache::remember('users', $minutes, function()
	{
		return DB::table('users')->get();
	});

[PTBR]
Pode também combiar os metodos `remember` e `forever`:

[ENG]
You may also combine the `remember` and `forever` methods:

	$value = Cache::rememberForever('users', function()
	{
		return DB::table('users')->get();
	});

Observe que todos os items armazenados em cache são serelizados, para que você seja livre para armazenar qualquer tipo de dados.

Note that all items stored in the cache are serialized, so you are free to store any type of data.

**Remover um item do cache**

	Cache::forget('key');

<a name="increments-and-decrements"></a>
## Incrementações e Decrementações

Todos os drives, exceto `file` e `database` suportam os operadores  `increment` e `decrement`:

**Incrementando um valor**

	Cache::increment('chave');

	Cache::increment('chave', $amount);

**Decrementando um valor**

	Cache::decrement('chave');

	Cache::decrement('chave', $amount);

<a name="cache-sections"></a>
## Sessão de cache

> **Atenção:** Sessões de cache não são suportadas quando se utiliza os drivers de cache `file` ou `database`.

Sessões de cache permitem agrupar items relacionados em cache, e então descarregue na sessão. Para acessar uma sessão, use o metodo `section`:


**Acessando uma sessão de cache**

	Cache::section('pessoa')->put('John', $john);

	Cache::section('pessoa')->put('Anne', $anne);

Também pode acessar os items da sessão de cache, 
You may also access cached items from the section, as well as use the other cache methods such as `increment` and `decrement`:

**Accessing Items In A Cache Section**

	$anne = Cache::section('people')->get('Anne');

Then you may flush all items in the section:

	Cache::section('people')->flush();

<a name="database-cache"></a>

## Cache de banco de dados
[PTBR]
Ao utilizar o driver de cache `database`, você precisa setar a tabela que contem os items de cache. A seguir um exemplo de declaração `schema`  para table:

[ENG]
When using the `database` cache driver, you will need to setup a table to contain the cache items. Below is an example `Schema` declaration for the table:

	Schema::create('cache', function($tabela)
	{
		$table->string('chave')->unique();
		$table->text('valor');
		$table->integer('expiração'); // aqui cabe um valor numerico
	});
