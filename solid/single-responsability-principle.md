# S - Single Responsability Principle

  

a letra **S** do solid representa um conceito bastante conhecido o **SRP**(Single Responsability Principle), que  diz o seguinte:

>  “Uma classe deve ter um, e somente um, motivo para ser modificada”
>  

Para exemplificar será usada a classe ```Pessoa```, que possui alguns atributos e um método chamado ```calcularImc```.

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
const pessoa = new Pessoa('Joao Vitor', 1.84, 95)
const imc = joao.calcularImc();

```


Note que a classe ```Pessoa```  tem mais de um motivo para ser alterada, porque se o calculo mudar a classe ```Pessoa``` será afetada. 
a solução é simples e pode ser feita de diversas formas, aqui vamos criar uma segunda classe que se chamara  ```Imc``` e ela terá um método ```calcular```, essa função ira receber o peso e altura através de parametros e por fim ira retornar o resultado. 

```typescript
class Imc{
  static calcular(peso: number, altura: number):number {
    return peso/(altura * altura;
  }
}
const joao = new Pessoa('Joao Vitor', 1.84, 95)
const imc = Imc.calcular(95, 1.84);
```

Dessa forma garantimos que o calculo não afeta a ```Pessoa```  como também torna o reaproveitamento do codigo mais eficiente, visto que agora podemors utilizar a classe Imc em qualquer parte do projeto que precise calcular o mesmo.
