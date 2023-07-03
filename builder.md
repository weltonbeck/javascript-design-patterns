[voltar](/index.md)

# Builder

O padrão Builder (ou Construtor) é um padrão de projeto criacional que permite a construção de objetos complexos passo a passo. Ele separa a construção de um objeto complexo de sua representação, permitindo que o mesmo processo de construção possa criar diferentes representações.

O Builder é útil quando a criação de um objeto envolve várias etapas e configurações opcionais, ou quando existem diferentes formas de construir um objeto com a mesma base. Ele simplifica o processo de construção e permite que o código cliente crie objetos complexos de forma mais legível e flexível.

Aqui está um exemplo em JavaScript de como implementar o padrão Builder:

```JS
// Classe de exemplo: Pizza
class Pizza {
  constructor() {
    this.tipo = null;
    this.tamanho = null;
    this.ingredientes = [];
  }

  adicionarIngrediente(ingrediente) {
    this.ingredientes.push(ingrediente);
  }

  exibirDetalhes() {
    console.log(`Pizza ${this.tipo}, Tamanho: ${this.tamanho}`);
    console.log("Ingredientes: ", this.ingredientes.join(", "));
  }
}

// Classe Builder de Pizza
class PizzaBuilder {
  constructor() {
    this.pizza = new Pizza();
  }

  setTipo(tipo) {
    this.pizza.tipo = tipo;
    return this;
  }

  setTamanho(tamanho) {
    this.pizza.tamanho = tamanho;
    return this;
  }

  adicionarIngrediente(ingrediente) {
    this.pizza.adicionarIngrediente(ingrediente);
    return this;
  }

  build() {
    return this.pizza;
  }
}

// Uso do Builder
const builder = new PizzaBuilder();
const pizza = builder.setTipo('Calabresa')
                     .setTamanho('Grande')
                     .adicionarIngrediente('Queijo')
                     .adicionarIngrediente('Calabresa')
                     .adicionarIngrediente('Tomate')
                     .build();

pizza.exibirDetalhes();
// Saída:
// Pizza Calabresa, Tamanho: Grande
// Ingredientes: Queijo, Calabresa, Tomate

```

Nesse exemplo, temos a classe `Pizza` que será construída passo a passo usando o padrão Builder. O objeto `Pizza` possui propriedades como `tipo`, `tamanho` e `ingredientes`. A classe `PizzaBuilder` é responsável por configurar e construir a pizza, fornecendo métodos para definir o tipo, tamanho e adicionar ingredientes.

O código cliente cria uma instância do `PizzaBuilder` e usa seus métodos de configuração para definir as propriedades desejadas e adicionar ingredientes. Por fim, o método `build()` é chamado para obter o objeto `Pizza` construído. Em seguida, os detalhes da pizza são exibidos usando o método `exibirDetalhes()`.

Dessa forma, o padrão Builder permite a criação flexível de objetos complexos, como pizzas, com diferentes combinações de propriedades e etapas de construção. Ele separa a lógica de construção do objeto da sua representação final, tornando o código mais legível e modular.