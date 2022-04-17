# L - Liskov Substitution Principle

<h2>Definição</h2>
                                                                                                                                                          
O principio definido pela letra '**L**' do solid é o **LSP**(Princípio de Substituição de Liskov) que diz:

> Se para cada objeto o1 do tipo S há um objeto o2 do tipo T de forma que, para todos os programas P definidos em termos de T, o comportamento de P é inalterado quando o1 é substituído por o2 então S é um subtipo de T.
> 
Apesar de ter uma definição complexa, o principio pode ser resumido da seguinte forma:
> As classes derivadas devem ser substituíveis por suas classes bases
> 
<h2>Violando do principio</h2>
Um exemplo simples de violação acontece quando uma classe derivada não implementa um método da classe base, como no exemplo abaixo:

```typescript
interface  Ave  {
	voar():  void;
}

class  Aguia  implements  Ave{
	voar():  void  {
		console.log('Aguia voando a 240km/h.')
	}
}

class  Pardal  implements  Ave{
	voar():  void  {
		console.log('Pardal voando a 46 km/h.')
	}
}

function testeVoo(ave:  Ave)  {
	ave.voar();
}
```

No exemplo, fica claro que as classe **Aguia** e **Pardal**, podem **substituir** a classe Ave. para efeitos de teste a função **testeDeVoo**,  recebe uma ave e executa o método voar. note que indenpende da **Ave** a função continua funcionando perfeitamente.
```typescript
const aguia =  new  Aguia();
const pardal =  new  Pardal();

testeVoo(aguia);
testeVoo(pardal);
```


Porém, essa estrutura quebra quando implementamos a classe **Pinguim**, o motivo é simples, piguins são aves, entretando eles não possuem a capacidade de voar.

Veja como ficaria um exemplo utilizando a mesma estruta anterior, mas, adicionando a classe Pinguim e tentando substituir ela por sua classe base.
```typescript
class  Pinguim  implements  Ave{

	voar():  void  {
		throw  new  Error("Error: Pinguim não voa!.");
	}
}
const pinguim =  new  Pinguim();

testeVoo(pinguim);
```

Ao tentar repetir nosso teste obtemos a violação do principio, o pinguim mesmo sendo uma ave não é capaz de substituir sua classe base, gerando o seguinte erro:
```bash
	[ERR]: "Executed JavaScript Failed:"
	[ERR]: "Error: Pinguim não voa!".
```
