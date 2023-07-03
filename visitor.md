[voltar](/README.md)

# Visitor

O padrão Visitor é um padrão comportamental que permite separar a estrutura de um objeto de suas operações ou algoritmos. Ele permite adicionar novas operações a objetos existentes sem modificar suas classes.

O padrão Visitor é útil quando temos uma estrutura de objetos complexa e queremos realizar diferentes operações nessa estrutura. Em vez de adicionar essas operações às classes dos objetos individuais, o padrão Visitor nos permite definir operações em classes separadas chamadas visitantes.

Vamos ver um exemplo simplificado em JavaScript:

```js
// Elementos da estrutura
class Product {
  constructor(name, price) {
    this.name = name;
    this.price = price;
  }

  accept(visitor) {
    visitor.visit(this);
  }
}

class Order {
  constructor() {
    this.products = [];
  }

  addProduct(product) {
    this.products.push(product);
  }

  accept(visitor) {
    visitor.visit(this);
  }
}

// Visitantes
class PriceCalculatorVisitor {
  visit(product) {
    console.log(`Calculando o preço do produto ${product.name}`);
    // Realiza a operação desejada no objeto Product
    // Neste exemplo, apenas exibe o preço do produto
    console.log(`Preço: R$ ${product.price}`);
  }

  visit(order) {
    console.log('Calculando o preço total do pedido');
    let totalPrice = 0;
    for (const product of order.products) {
      totalPrice += product.price;
    }
    console.log(`Preço total do pedido: R$ ${totalPrice}`);
  }
}

// Uso
const product1 = new Product('Camiseta', 29.99);
const product2 = new Product('Calça', 59.99);

const order = new Order();
order.addProduct(product1);
order.addProduct(product2);

const visitor = new PriceCalculatorVisitor();

product1.accept(visitor);
product2.accept(visitor);
order.accept(visitor);

```

Neste exemplo, temos as classes `Product` e `Order` que representam elementos da estrutura. Ambas implementam um método `accept(visitor)` que permite que um visitante execute uma operação em cada elemento da estrutura.

Em seguida, temos a classe `PriceCalculatorVisitor`, que é o visitante responsável por realizar cálculos de preços. Ele implementa os métodos `visit(product)` e `visit(order)` para calcular o preço de um produto individual e o preço total de um pedido, respectivamente.

No exemplo de uso, criamos instâncias de produtos e um pedido. Em seguida, criamos uma instância do visitante `PriceCalculatorVisitor`. Chamamos o método `accept(visitor)` em cada produto e no pedido, passando o visitante como parâmetro. O visitante executa a operação desejada em cada objeto visitado.

A saída resultante exibirá as mensagens de cálculo de preço para cada produto individualmente e para o pedido como um todo.

O padrão Visitor permite adicionar novas operações a uma estrutura de objetos sem modificar as classes desses objetos. Isso promove o princípio de aberto/fechado (open/closed principle) e facilita a extensibilidade da estrutura. Cada visitante pode implementar sua própria operação específica sem afetar as classes dos elementos visitados.
