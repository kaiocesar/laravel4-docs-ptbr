# Utilização básica com banco de dados

- [Configuração](#configuration)
- [Execução de consultas](#running-queries)
- [Transactions no banco de dados](#database-transactions)
- [Acessar conexões](#accessing-connections)
- [Carregar consultas](#query-logging)

<a name="configuration"></a>
## Configuração

Laravel conecta com o banco de dados e executa consultas extremamente simples. O banco de dados é configurado pelo arquivo `app/config/database.php`. Neste arquivo pode-se definir todas suas conexões de banco de dados, bem como especificar  qual conexão deverá utilizar-se por padrão. Exemplo para todos sistemas de banco de dados suportados e fornecidos neste arquivo.

Atualmente o Laravel suporta quatro sistemas de banco de dados: MySQL, Postgres, SQLite e SQL Server.




<a name="running-queries"></a>
## Execução de consultas

Ao configurar sua conexão com o banco de dados, você pode executar consultas usando a classe `DB`.


**Executando uma consulta com SELECT**

	$results = DB::select('select * from users where id = ?', array(1));

O método `select` sempre retornará um `array` com resultados.


**Executando uma instrução INSERT**

	DB::insert('insert into users (id, name) values (?, ?)', array(1, 'Dayle'));

**Executando uma instrução UPDATE**

	DB::update('update users set votes = 100 where name = ?', array('John'));

**Executando uma instrução DELETE**

	DB::delete('delete from users');

> **Observe:** As instruções `update` e `delete` retornam um numero de linhas afetadas pela operação.

[ptbr]
**Executando uma instrução geral**

[eng]
**Running A General Statement**

	DB::statement('drop table users');
	
Pode-se listar os eventos de uma consulta utilizando o método `DB::listen`:

**Listando eventos de uma consulta**

	DB::listen(function($sql, $bindings, $time)
	{
		//
	});

<a name="database-transactions"></a>

## Transactions no banco de dados
Para executar um conjunto de operações transaction dentro do banco de dados, você pode utilizar o método `transaction`:

	DB::transaction(function()
	{
		DB::table('users')->update(array('votes' => 1));

		DB::table('posts')->delete();
	});

<a name="accessing-connections"></a>

## Acessar uma conexão
Quando se utiliza várias conexões, você pode acessar-los atráves do método `DB::connection`:

	$users = DB::connection('foo')->select(...);
[PTBR]
Você pode acessar, por exemplo uma instancia PDO

[ENG]
You may also access the raw, underlying PDO instance:

	$pdo = DB::connection()->getPdo();

Sometimes you may need to reconnect to a given database:

	DB::reconnect('foo');

<a name="query-logging"></a>
## Query Logging

By default, Laravel keeps a log in memory of all queries that have been run for the current request. However, in some cases, such as when inserting a large number of rows, this can cause the application to use excess memory. To disable the log, you may use the `disableQueryLog` method:

	DB::connection()->disableQueryLog();
