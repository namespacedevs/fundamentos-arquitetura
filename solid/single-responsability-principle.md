# S - Single Responsability Principle

  

A letra '**S**' do SOLID representa um conceito bastante conhecido: o **SRP** (Single Responsability Principle). Que  diz o seguinte:

>  Uma classe deve ter um, e somente um, motivo para ser modificada.
>  

Para exemplificar, será usada a classe ```Pessoa```, que possui alguns atributos e um método chamado ```calcularImc```.

```typescript
class Pessoa{
  nome: string
  altura: number
  peso: number
  calcularImc():number {
    return this.peso/(this.altura * this.altura;
  }
}


//caso de uso:
const pessoa = new Pessoa('João Vitor', 1.84, 95)
const imc = joao.calcularImc();

```


Note que a classe ```Pessoa```  tem mais de um motivo para ser alterada, porque se o cálculo mudar, a classe ```Pessoa``` será afetada. 
A solução é simples e pode ser feita de diversas formas. Neste exemplo, vamos criar uma segunda classe que se chamará  ```Imc``` e ela terá um método ```calcular```. Essa função irá receber o peso e altura através de parâmetros e por fim, irá retornar o resultado. 

```typescript
class Imc{
  static calcular(peso: number, altura: number):number {
    return peso/(altura * altura;
  }
}
const joao = new Pessoa('João Vitor', 1.84, 95)
const imc = Imc.calcular(95, 1.84);
```

Dessa forma, garantimos que o cálculo não afeta a ```Pessoa```,  como também, torna o reaproveitamento do código mais eficiente, visto que agora podemos utilizar a classe Imc em qualquer parte do projeto que precise calcular o mesmo.
