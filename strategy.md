[voltar](/README.md)

# Strategy

O padrão Strategy é um padrão comportamental que permite que um objeto altere seu comportamento em tempo de execução, selecionando uma estratégia específica dentre várias disponíveis. Ele encapsula algoritmos em classes separadas, permitindo que sejam facilmente substituídos e variados independentemente do objeto que os utiliza.

Um exemplo prático do padrão Strategy é um sistema de processamento de pagamentos que oferece diferentes estratégias de pagamento, como pagamento com cartão de crédito, pagamento com boleto bancário ou pagamento com carteira digital. Cada estratégia representa um algoritmo de pagamento diferente.

Vamos ver um exemplo simplificado em JavaScript:

```js
// Estratégias (Strategies)
class CreditCardPaymentStrategy {
  pay(amount) {
    console.log(`Pagamento de R$${amount} feito com cartão de crédito.`);
  }
}

class BankSlipPaymentStrategy {
  pay(amount) {
    console.log(`Pagamento de R$${amount} feito com boleto bancário.`);
  }
}

class DigitalWalletPaymentStrategy {
  pay(amount) {
    console.log(`Pagamento de R$${amount} feito com carteira digital.`);
  }
}

// Contexto (Context)
class PaymentProcessor {
  constructor(strategy) {
    this.strategy = strategy;
  }

  setStrategy(strategy) {
    this.strategy = strategy;
  }

  processPayment(amount) {
    this.strategy.pay(amount);
  }
}

// Uso
const paymentProcessor = new PaymentProcessor(new CreditCardPaymentStrategy());

paymentProcessor.processPayment(100); // Pagamento de R$100 feito com cartão de crédito.

paymentProcessor.setStrategy(new BankSlipPaymentStrategy());
paymentProcessor.processPayment(250); // Pagamento de R$250 feito com boleto bancário.

paymentProcessor.setStrategy(new DigitalWalletPaymentStrategy());
paymentProcessor.processPayment(50); // Pagamento de R$50 feito com carteira digital.

```

Neste exemplo, temos as classes `CreditCardPaymentStrategy`, `BankSlipPaymentStrategy` e `DigitalWalletPaymentStrategy`. Cada uma dessas classes representa uma estratégia de pagamento diferente e implementa um método `pay(amount)` para processar o pagamento com a estratégia específica.

A classe `PaymentProcessor` atua como o contexto que recebe a estratégia de pagamento atual. Ela possui um método `setStrategy(strategy)` para definir a estratégia de pagamento desejada e um método `processPayment(amount)` para processar o pagamento com base na estratégia atualmente definida.

No exemplo de uso, criamos uma instância do `PaymentProcessor` chamada `paymentProcessor` e definimos a estratégia inicial como `CreditCardPaymentStrategy`. Chamamos o método `processPayment(amount)` para realizar o pagamento com o valor especificado. Em seguida, usamos o método `setStrategy(strategy)` para alterar a estratégia de pagamento para `BankSlipPaymentStrategy` e `DigitalWalletPaymentStrategy` e chamamos novamente o método `processPayment(amount)` para realizar os pagamentos correspondentes.

A saída resultante mostra as mensagens de pagamento de acordo com a estratégia selecionada em cada caso.

O padrão Strategy permite que o comportamento de um objeto seja alterado dinamicamente em tempo de execução, selecionando a estratégia adequada para uma determinada situação. Ele promove a flexibilidade, o desacoplamento e a reutilização de código ao encapsular algoritmos em classes separadas. Isso facilita a adição de novas estratégias e a modificação do comportamento do objeto sem afetar seu código cliente.