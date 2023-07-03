[voltar](/index.md)

# Factory

O padrão Factory (ou Factory Method) é um padrão de criação de objetos que fornece uma interface para criar objetos de diferentes tipos, sem expor a lógica de criação diretamente ao código que os utiliza. Ele encapsula a lógica de criação em uma classe separada, conhecida como "fábrica", que é responsável por instanciar os objetos desejados.

O Factory é útil quando você precisa criar objetos com base em certas condições ou parâmetros, sem que o código cliente precise conhecer os detalhes da implementação específica de cada objeto. Ele promove a encapsulação, o desacoplamento e a extensibilidade do código.

Aqui está um exemplo em JavaScript de como implementar o padrão Factory:

```JS
// Classe de exemplo: Carro
class Carro {
  constructor(modelo, ano) {
    this.modelo = modelo;
    this.ano = ano;
  }

  exibirDetalhes() {
    console.log(`Modelo: ${this.modelo}, Ano: ${this.ano}`);
  }
}

// Fábrica de Carros
class FabricaDeCarros {
  criarCarro(modelo, ano) {
    return new Carro(modelo, ano);
  }
}

// Uso do Factory
const fabrica = new FabricaDeCarros();
const carro1 = fabrica.criarCarro('Fiat', 2020);
const carro2 = fabrica.criarCarro('Ford', 2021);

carro1.exibirDetalhes(); // Saída: Modelo: Fiat, Ano: 2020
carro2.exibirDetalhes(); // Saída: Modelo: Ford, Ano: 2021
```

Neste exemplo, temos a classe `Carro` que representa um carro com propriedades de modelo e ano. A classe `FabricaDeCarros` é a fábrica que encapsula a lógica de criação de objetos `Carro`. Ela possui um método `criarCarro` que recebe o modelo e o ano e retorna uma nova instância de `Carro`.

Ao utilizar o Factory, o código cliente (neste caso, o uso da fábrica) não precisa saber como exatamente o objeto `Carro` é criado. Ele apenas invoca o método `criarCarro` da fábrica, fornecendo os parâmetros necessários, e recebe o objeto `Carro` criado pela fábrica.

Dessa forma, o Factory permite adicionar lógica de criação complexa ou criar diferentes tipos de objetos com base em condições específicas, sem afetar o código que utiliza esses objetos. Isso torna o código mais flexível, modular e fácil de manter.