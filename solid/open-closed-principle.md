# O - Open Closed Principle

  

O principio definido pela letra '**O**' do solid é o **OCP** (Open Closed Principle) e ele diz que:

> Deve ser possível estender o comportamento de uma classe sem modificá-la.
> 

Para este exemplo, vamos usar a classe  ```ServicoDeFrete```. Ela recebe um serviço de frete (exemplo: correios e jadlog) e, com base nisso, calcula o valor do frete.

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
A classe funciona para o propósito, porém ela fere o **OCP**, pois para cada novo serviço será necessário **modificar** a classe e incluir o novo comportamento. Dessa forma, as chances de inserir um novo bug no sistema são altas.

Para cumprir o **OCP**, a refatoração, neste caso é, simples. Basta transformar o ```ServicoDeFrete``` em uma interface ou classe abstrata para abstrair o comportamento e implementar uma classe concreta para cada serviço a ser disponibilizado.
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

Pronto! Agora somos capazes de implementar um novo comportamento sem modificar a nossa classe atendendo o **OCP**.
