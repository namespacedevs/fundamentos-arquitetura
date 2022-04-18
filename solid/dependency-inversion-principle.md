# D - Dependency Inversion Principle

<h2>Definição</h2>
Segundo Uncle Bob esse principio é definido da seguinte forma:

>1. Módulos de alto nível não devem depender de módulos de baixo nível. Ambos devem depender da abstração.

>2. Abstrações não devem depender de detalhes. Detalhes devem depender de abstrações.
> 
em outras palavras:
>Não dependa de implementações e sim de abstrações.
> 
<h2>Violando do principio</h2>
Imagine que temos uma classe de serviço de usuário e essa consome um repositório também de usuários.  
uma forma de quebra muito comum é a injeção do repositório no serviço via implementação, observe o exemplo:

```typescript
class  UsuarioServico{
	constructor(private _usuarioRepositorio:  UsuarioRepositorio){  }
	criar(nome:  string):  void{
		return  this._usuarioRepositorio.inserir(nome);
	}
	remover(id:  number):  void{
		return  this._usuarioRepositorio.apagar(id);
	}
}
```

```typescript
class  UsuarioRepositorio  {
	inserir(nome:  string){
		console.log(`${nome}, foi cadastrado com sucesso!.`);
	}
	apagar(id:  number):  void{
		console.log(`Usuario de id ${id} foi apagado.`);
	}
}
```
Note que a classe **UsuarioServico** depende diretamente da classe **UsuarioRepositorio**, violando assim o **DIP**(Dependency Inversion Principle).
