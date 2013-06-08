# Contribuindo para o Laravel

- [Introdução](#introduction)
- [Requisições Pull](#pull-requests)
- [Coding Guidelines](#coding-guidelines)

<a name="introduction"></a>
## Introdção

Laravel é livre, Software de código aberto, ou seja, qualquer um pode contribuir para o desenvolvimento e melhorias.
o código do Laravel está atualmente no [Github](http://github.com), que fornece métodos faceis para cópiar o projeto e
fundir suas contribuições.

<a name="pull-requests"></a>
## Requisições Pull

O processo de requisição pull difere de novas features e bugs. Antes de enviar a requisição pull para uma nova feature, você
deverá primeiro criar um issue com o titulo `[Proposal]`. A proposta deve descrever a nova feature, bem como ideias de implementações.
A proposta será revisa e ou aprovada ou negada. Uma vez que a proposta é aprovada, uma requisição pull podem ser criada 
para a implementação da nova feature, requisições pull que não seguirem essa diretriz serão imediatamente fechadas. 


Requisições pull para bug pode ser enviadas sem criação de qualquer issue de proposta. Se você acredita que encontrou 
uma solução para um bug que te, sido apresentado no GitHub, por favor deixe um comentário detalhando em sua proposta 
de correção.


### Requisições de Feature
Se você tem ideias para novas implementações, e gostarias de ver-las adicionadas ao Laravel, você pode criar um issue no Github com o titulo `[Request]`.O Pedido de feature será então revisado por um contribuidor do Core do Laravel.

<a name="coding-guidelines"></a>
## Coding Guidelines

Laravel segue as padrão de codificação [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) e [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)

Além destes padrões, a seguir uma lista de outros padrões de codificação que deve ser seguidas:

- declarações de namespace devem estar na mesma linha que `<?php`.
- abertura de class `{` deve estar na mesma linha do nome da classe, por exemplo `class database {`
- Nomes de Interfaces com o sufixo `Interface` (`FooInterface`)
