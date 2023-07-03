[voltar](/README.md)

# Observer

O padrão Observer é um padrão comportamental que permite que objetos observadores sejam notificados automaticamente quando ocorre uma alteração em um objeto observado, também conhecido como sujeito. Ele estabelece uma relação de um-para-muitos entre o sujeito e os observadores, permitindo que vários observadores acompanhem as mudanças no sujeito sem acoplamento rígido entre eles.

Um exemplo real do padrão Observer é o sistema de notificações em uma aplicação de mensagens instantâneas. Considere um aplicativo de chat onde vários usuários podem se conectar e trocar mensagens entre si. Nesse caso, o sujeito é a entidade responsável por gerenciar as mensagens e notificar os usuários conectados quando uma nova mensagem é recebida. Os observadores são os usuários que desejam ser notificados quando uma nova mensagem chega.

Vamos dar uma olhada em um exemplo simplificado em JavaScript que ilustra o padrão Observer nesse contexto:

```js
// Sujeito (Subject)
class ChatRoom {
  constructor() {
    this.messages = [];
    this.observers = [];
  }

  addObserver(observer) {
    this.observers.push(observer);
  }

  removeObserver(observer) {
    this.observers = this.observers.filter((obs) => obs !== observer);
  }

  addMessage(message) {
    this.messages.push(message);
    this.notifyObservers(message);
  }

  notifyObservers(message) {
    this.observers.forEach((observer) => {
      observer.update(message);
    });
  }
}

// Observador (Observer)
class User {
  constructor(name) {
    this.name = name;
  }

  update(message) {
    console.log(`${this.name} recebeu uma nova mensagem: ${message}`);
  }
}

// Uso
const chatRoom = new ChatRoom();

const user1 = new User('Alice');
const user2 = new User('Bob');
const user3 = new User('Charlie');

chatRoom.addObserver(user1);
chatRoom.addObserver(user2);
chatRoom.addObserver(user3);

chatRoom.addMessage('Olá a todos!');

chatRoom.removeObserver(user2);

chatRoom.addMessage('Como vocês estão?');

// Alice recebeu uma nova mensagem: Olá a todos!
// Bob recebeu uma nova mensagem: Olá a todos!
// Charlie recebeu uma nova mensagem: Olá a todos!
// Alice recebeu uma nova mensagem: Como vocês estão?
// Charlie recebeu uma nova mensagem: Como vocês estão?

```

Neste exemplo, temos a classe `ChatRoom`, que atua como o sujeito. Ela mantém uma lista de mensagens e uma lista de observadores. Os métodos `addObserver` e `removeObserver` são usados para adicionar e remover observadores da lista. O método `addMessage` é usado para adicionar uma nova mensagem à lista e, em seguida, notificar todos os observadores sobre a nova mensagem usando o método `notifyObservers`.

A classe `User` representa os observadores. Cada usuário tem um nome e implementa o método `update`, que é chamado quando uma nova mensagem é recebida. Neste exemplo, o método `update` simplesmente exibe uma mensagem no console informando que o usuário recebeu uma nova mensagem.

No exemplo de uso, criamos uma instância da `ChatRoom` e três instâncias de `User`. Em seguida, adicionamos os usuários como observadores usando o método `addObserver`. Em seguida, adicionamos uma nova mensagem à sala de bate-papo usando o método `addMessage`. Isso aciona a notificação para todos os observadores, e cada usuário registrado exibe uma mensagem informando que recebeu a nova mensagem.

Também ilustramos a remoção de um observador usando o método `removeObserver`. Neste caso, removemos o usuário `user2` da lista de observadores. Quando uma nova mensagem é adicionada após a remoção do observador, apenas os usuários `user1` e `user3` são notificados.

A saída resultante será:

    Alice recebeu uma nova mensagem: Olá a todos!
    Bob recebeu uma nova mensagem: Olá a todos!
    Charlie recebeu uma nova mensagem: Olá a todos!
    Alice recebeu uma nova mensagem: Como vocês estão?
    Charlie recebeu uma nova mensagem: Como vocês estão?

Isso demonstra como o padrão Observer permite que objetos observadores sejam notificados automaticamente sobre alterações em um objeto observado. No exemplo, a `ChatRoom` é o sujeito e os `User` são os observadores. Quando uma nova mensagem é adicionada à sala de bate-papo, todos os usuários registrados como observadores são notificados e podem executar ações com base na nova mensagem recebida. Isso permite uma comunicação flexível e desacoplada entre os diferentes componentes da aplicação.