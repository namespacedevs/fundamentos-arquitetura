# O - Open Closed Principle

  

O principio definido pela letra '**o**' do solid é o **ocp**(open closed principle) e ele diz que:

> Você deve ser capaz de estender o comportamento de uma classe sem modifica-la
> 

Para este exemplo vamos usar a classe  ```ServicoDeFrete```, ela recebe um serviço de frete(exemplo: correios e jadlog) e com base nele calcula o valor do frete.

```typescript
enum ServicosDeFrete {
    correios = 'correios',
    jadlog = 'jadlog'
}


class ServicoDeFrete {
    constructor(servico: ServicosDeFrete){
        this.servico = servico;
    }
    servico: ServicosDeFrete
    calcularValorDaEntrega(peso: number){
        if(this.servico == ServicosDeFrete.correios){
            return peso * 0,3
        }
        if(this.servico == ServicosDeFrete.jadlog){
            return peso * 0,2
        }
        throw `Calculo do serviço ${this.servico} não implementado.`
    }
}

const correios = new ServicoDeFrete(ServicosDeFrete.correios);
const valorDoFrete = correios.calcularValorDaEntrega(2);

```
A classe funciona para o proposito, porém ela fere o **ocp**, pois para cada novo serviço será necessario **modificar** a classe e incluir o novo comportamento, dessa forma as chances de inserir um novo bug no sistema é alta.

para cumprir o **ocp** a refatoração neste caso é simples, basta transformar o ServicoDeFrete em uma interface ou classe abstrata para abstrair o comportamento e implementar uma classe concreta para cada serviço que queira disponibilizar.
```typescript
interface  ServicoDeFrete  {
	calcularValorDaEntrega(peso:  number):  number
}

class  Correios  implements  ServicoDeFrete  {
	calcularValorDaEntrega(peso:  number):  number  {
		return peso *  0.3
	}
}

  

class  Jadlog  implements  ServicoDeFrete  {
  calcularValorDaEntrega(peso:  number):  number  {
    return peso *  0.2
  }
}

const correios =  new  Correios();
const valorDoFreteCorreios = correios.calcularValorDaEntrega(2);

const jadlog =  new  Jadlog();
const valorDoFreteJadlog = jadlog.calcularValorDaEntrega(2);

```

Pronto, agora somos capazer de implementar um novo comportamento sem modificar a classe a nossa classe atendendo o **ocp**.
