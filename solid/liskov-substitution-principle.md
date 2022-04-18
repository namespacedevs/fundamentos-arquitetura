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


<h2>Atendendo do principio</h2>

Atender o principio de substituição de Liskov irá tornar suas abstrações mais coesas. para demostrar isso vamos melhorar nossa definção de aves para o contexto do voo.
**Aves** **que voam** possuem a classificação de **Carinatas** e as **que não voam** são denominadas como **Ratitas**.  Além disso, uma caracterisca curiosa das aves é que todas tem bico, sendo assim a interface ou classe abstrata Ave continua tendo sua importancia e com sua implementação valida. depois de toda essa estruturação e contexto nossas classes ficam assim:
```typescript
abstract  class  Ave  {
	bicar():  void  {
		console.log('bicando...')
	}
}
```

```typescript
abstract  class  Carinata  extends  Ave  {
	voar():  void  {
		console.log('Carinata voando...')
	}
} 

abstract  class  Ratita  extends  Ave  {
	bicar():  void  {
		console.log('Ratita bicando...')
	}
}
```

```typescript
class  Aguia  implements  Carinata{
	bicar():  void  {
		console.log('Aguia bicando.');
	}
	voar():  void  {
		console.log('Aguia voando a 240km/h.')
	}
} 

class  Pardal  implements  Carinata{
	bicar():  void  {
		console.log('Pardal bicando.');
	}
	voar():  void  {
		console.log('Pardal voando a 46 km/h.')
	}
}
class  Pinguim  implements  Ratita{
	bicar():  void  {
		console.log('Pinguim bicando.');
	}
}
```
Além das alterações nas classes é necessario modificar a função **testeVoo** para aceitar apenas **Carinata**.

```typescript
function testeVoo(ave:  Carinata)  {
	ave.voar();
}

const aguia =  new  Aguia();
const pardal =  new  Pardal();

testeVoo(aguia);
testeVoo(pardal);
```
Dessa forma garantimos a integridade do sistema, que não será quebrado por falta de implementação de um classe que possui um métodos mais que não implementa nada no mesmo.

além disso podemos testar a substituição da **Ave** por **qualquer** outra **derivada**, usando a seguinte função:
```typescript
function testeBicar(ave:  Ave)  {
	ave.bicar();
}
testeBicada(aguia);
testeBicada(pardal);
testeBicada(pinguim);
```
E dessa forma atendemos o principio de substituição de Liskov.

