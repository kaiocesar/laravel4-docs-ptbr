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

Laravel segue os padrões de projeto [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) e  
[PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md)


Laravel follows the [PSR-0](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md) 
and [PSR-1](https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md) 
coding standards.
In addition to these standards, below is a list of other coding standards that should be followed:

- Namespace declarations should be on the same line as `<?php`.
- Class opening `{` should be on the same line as the class name.
- Function and control structure opening `{` should be on a separate line.
- Interface names are suffixed with `Interface` (`FooInterface`)
