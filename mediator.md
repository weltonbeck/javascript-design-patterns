[voltar](/README.md)

# Mediador

O padrão Mediator é um padrão comportamental que define um objeto centralizado (o mediador) que coordena as interações entre vários objetos (os colegas). Ele promove o baixo acoplamento entre os colegas, evitando que eles se comuniquem diretamente, e em vez disso, os direciona a se comunicarem por meio do mediador.

O padrão Mediator é útil quando há um conjunto complexo de interações entre objetos e o acoplamento direto entre eles se torna difícil de manter. Ele ajuda a organizar e controlar as interações, fornecendo um ponto central de comunicação.

Os principais elementos do padrão Mediator são:

- `Mediator (Mediador)`: É a interface ou classe abstrata que define o contrato para o mediador. Geralmente, possui métodos para registrar colegas, receber e direcionar mensagens entre eles.
- `ConcreteMediator (Mediador Concreto)`: É a implementação concreta do mediador. Ele gerencia as interações entre os colegas e implementa a lógica de coordenação.
- `Colleague (Colega)`: São os objetos que se comunicam por meio do mediador. Cada colega conhece apenas o mediador e não tem conhecimento direto dos outros colegas. Ele interage com outros colegas por meio do mediador.
- `ConcreteColleague (Colega Concreto)`: São as implementações concretas dos colegas. Eles enviam e recebem mensagens por meio do mediador.

Aqui está um exemplo em JavaScript que ilustra o padrão Mediator:

```js
// Mediator
class Mediator {
  constructor() {
    this.colleague1 = null;
    this.colleague2 = null;
  }

  setColleague1(colleague1) {
    this.colleague1 = colleague1;
  }

  setColleague2(colleague2) {
    this.colleague2 = colleague2;
  }

  send(message, colleague) {
    if (colleague === this.colleague1) {
      this.colleague2.receive(message);
    } else if (colleague === this.colleague2) {
      this.colleague1.receive(message);
    }
  }
}

// Colleague
class Colleague {
  constructor(mediator) {
    this.mediator = mediator;
  }

  send(message) {
    this.mediator.send(message, this);
  }

  receive(message) {
    console.log(`Mensagem recebida: ${message}`);
  }
}

// Uso
const mediator = new Mediator();

const colleague1 = new Colleague(mediator);
const colleague2 = new Colleague(mediator);

mediator.setColleague1(colleague1);
mediator.setColleague2(colleague2);

colleague1.send("Olá do Colleague 1!");
// Mensagem recebida: Olá do Colleague 1!
colleague2.send("Olá do Colleague 2!");
// Mensagem recebida: Olá do Colleague 2!

```

Neste exemplo, temos a classe `Mediator` que atua como o mediador. Ele possui referências para os objetos `Colleague` (`colleague1` e `colleague2`). O método `setColleague1` e `setColleague2` são usados para configurar os colegas no mediador.

A classe `Colleague` representa os colegas que se comunicam por meio do mediador. Cada colega possui uma referência ao mediador e utiliza o método `send` para enviar mensagens. Quando um colega recebe uma mensagem, ele chama o método `receive` para exibir a mensagem.

No exemplo de uso, criamos uma instância do mediador e duas instâncias de colegas. Em seguida, configuramos os colegas no mediador usando os métodos `setColleague1` e `setColleague2`.

Depois disso, os colegas podem se comunicar enviando mensagens por meio do mediador. O colega 1 envia a mensagem "Olá do Colleague 1!" chamando o método `send`, e o colega 2 recebe a mensagem através do mediador e a exibe. Da mesma forma, o colega 2 envia a mensagem "Olá do Colleague 2!" e o colega 1 recebe e exibe a mensagem.

A saída resultante será:

    Mensagem recebida: Olá do Colleague 1!
    Mensagem recebida: Olá do Colleague 2!

Isso demonstra como o padrão Mediator permite a comunicação indireta entre objetos, reduzindo o acoplamento entre eles. O mediador centraliza a lógica de coordenação e gerencia as interações entre os colegas, permitindo que eles se comuniquem de forma eficiente e desacoplada. Isso promove a flexibilidade, extensibilidade e reutilização de código.