# I - Interface Segregation Principle

<h2>Definição</h2>
                                                                                                                                                          
O principio definido pela letra '**I**' do solid é o **I**nterface Segregation Principle(Princípio de Segregação de Interface) ou **ISP**, que diz:

> Clientes não devem ser forçados a depender de Interfaces que eles não utilizam.
> 
Em outras palavra:
> As classes não devem ser forçadas a implementar interfaces que não utilizam. 
> 

<h2>Violando do principio</h2>
Um exemplo de violação é o das aves, onde uma classe Pinguim implementa a interface Ave, esse exemplo pode ser encontrado no LSP. 
No caso do ISP, iremos usar uma interface chamada Carro, 
ela ira conter a sequinte estrutura:

```typescript
interface  Carro  {
	ligar():  boolean;
	acionarAirbag():  boolean;
}
```

Essa interface poderia ter muitos outros métodos, como acelerar, frear e muitos outros. porém, para efeito de exemplo somente esses dois são suficientes.

Ao criar uma classe concreta utilizando a interface chegamos a seguinte estrutura.
```typescript
class  Corola  implements  Carro  {
	ligar():  boolean  {
		console.log('Ligando o carro...');
		console.log('Carro ligado!');
		return  true;
	}
	acionarAirbag():  boolean  {
		console.log('Acionando airbag');
		console.log('Airbag acionado com sucesso!');
		return  true;
	}
}
```
que se utilizada irá funcionar perfeitamente:
```typescript
const corola =  new  Corola();
corola.ligar();
corola.acionarAirbag();
```

```typescript
// Retorno no console
[LOG]: "Ligando o carro..."  
----------
[LOG]: "Carro ligado!"  
----------
[LOG]: "Acionando airbag"  
----------
[LOG]: "Airbag acionado com sucesso!"
```

Ok, até o momento tudo bem, mas e se precisarmos criar uma classe para representar uma Kombi?  
Esse carro não tem airbag como também não foi projetado para receber essa tecnologia. nesse caso estaríamos forçando nossa classe a implementar métodos que ela não utiliza, ferindo o princípio do ISP.

```typescript
class  Kombi  implements  Carro  {
	ligar():  boolean  {
		console.log('Ligando o carro...');
		console.log('Carro ligado!');
		return  true;
	}
	acionarAirbag():  boolean  {
		throw  new  Error("Erro: este carro não possui airbag.");
	}
}
```
<h2>Atendendo do principio</h2>

Atender o principio do **ISP** significa dizer que você terá que dividir seus contratos em contratos menores e mais especificos. no nosso caso Carro e CarroComAirbag.
```typescript
interface  Carro  {
	ligar():  boolean;
}
interface  CarroComAirbag  extends  Carro  {
	acionarAirbag():  boolean;
}
```
Após a segregação da interface o principio é atendido, veja como ficam as classe concretas **Corola** e **Kombi**.
```typescript
class  Corola  implements  CarroComAirbag  {
	ligar():  boolean  {
		console.log('Carro ligado com sucesso!');
		return  true;
	}
	acionarAirbag():  boolean  {
		console.log('Airbag acionado com sucesso!');
		return  true;
	}
}
```

```typescript
class  Kombi  implements  Carro  {
	ligar():  boolean  {
		console.log('Carro ligado com sucesso!');
		return  true;
	}
}
```
