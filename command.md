[voltar](/README.md)

# Command

O padrão Command é um padrão comportamental que encapsula uma solicitação como um objeto, permitindo que você parametrize clientes com diferentes solicitações, enfileire ou registre solicitações e ofereça suporte a operações desfazer.

O padrão Command permite que você separe o remetente de uma solicitação do objeto que realmente realiza a ação. Ele é composto por quatro elementos principais: o Command (comando), o Receiver (receptor), o Invoker (invocador) e o Client (cliente).

- `Command`: É uma interface ou classe abstrata que define o contrato para um comando. Geralmente possui um método execute que é responsável por executar a ação solicitada.
- `ConcreteCommand`: É uma implementação concreta da interface Command. Ele encapsula uma solicitação específica e mantém uma referência ao objeto Receiver que executará a ação.
- `Receiver`: É o objeto que contém a lógica real de execução da ação solicitada pelo Command.
- `Invoker`: É o objeto que invoca o Command para executar a ação. Ele possui uma referência ao objeto Command e pode chamar seu método execute.
- `Client`: É o objeto que cria um Command e atribui um Receiver a ele. O Client também pode configurar o Invoker para executar o Command quando necessário.

Aqui está um exemplo em JavaScript que ilustra o padrão Command:

```JS
// Command
class Command {
  execute() {
    throw new Error("Método execute deve ser implementado pelos subclasse.");
  }
}

// ConcreteCommand
class LigacaoCommand extends Command {
  constructor(receiver) {
    super();
    this.receiver = receiver;
  }

  execute() {
    this.receiver.ligar();
  }
}

class DesligamentoCommand extends Command {
  constructor(receiver) {
    super();
    this.receiver = receiver;
  }

  execute() {
    this.receiver.desligar();
  }
}

// Receiver
class Luz {
  ligar() {
    console.log("Luz ligada");
  }

  desligar() {
    console.log("Luz desligada");
  }
}

// Invoker
class Interruptor {
  setCommand(command) {
    this.command = command;
  }

  pressionar() {
    this.command.execute();
  }
}

// Client
const luz = new Luz();

const ligarCommand = new LigacaoCommand(luz);
const desligarCommand = new DesligamentoCommand(luz);

const interruptor = new Interruptor();

interruptor.setCommand(ligarCommand);
interruptor.pressionar(); // Ligar a luz

interruptor.setCommand(desligarCommand);
interruptor.pressionar(); // Desligar a luz
// Luz ligada
// Luz desligada

```
Neste exemplo, temos a classe `Command` que define a interface para um comando. Em seguida, temos as classes `LigacaoCommand` e `DesligamentoCommand` que são implementações concretas do `Command`. Cada uma delas encapsula uma ação específica e possui uma referência ao objeto `Receiver` (no caso, a classe `Luz`) que executará a ação.

O `Receiver` (no caso, a classe `Luz`) contém a lógica real de execução da ação solicitada pelo `Command`. Ele possui métodos `ligar` e `desligar` que representam as ações específicas.

O `Invoker` (no caso, a classe `Interruptor`) é responsável por invocar o `Command` para executar a ação. Ele possui um método `setCommand` para configurar o comando desejado e um método `pressionar` que chama o método `execute` do comando atribuído.

No exemplo de uso, criamos uma instância da classe `Luz` como o objeto `Receiver`. Em seguida, criamos instâncias das classes `LigacaoCommand` e `DesligamentoCommand`, passando o objeto `Luz` correspondente como argumento para o construtor.

Em seguida, criamos uma instância da classe `Interruptor` como o objeto `Invoker`. Configuramos o comando para ligar a luz usando o método `setCommand` e, em seguida, chamamos o método `pressionar` para executar a ação de ligar a luz. Em seguida, configuramos o comando para desligar a luz e chamamos o método `pressionar` novamente para executar a ação de desligar a luz.

A saída resultante será:

    Luz ligada
    Luz desligada

Isso demonstra como o padrão Command permite encapsular solicitações como objetos, permitindo que diferentes comandos sejam atribuídos dinamicamente a um invocador. O invocador não precisa conhecer detalhes sobre a implementação do comando ou do receptor, mas apenas chama o método `execute` do comando para realizar a ação desejada.

O padrão Command é útil quando você deseja parametrizar objetos com diferentes solicitações, enfileirar ou registrar solicitações para processamento posterior, desfazer operações ou fornecer um mecanismo para desfazer e refazer ações. Ele promove a flexibilidade, desacoplamento e extensibilidade do código.