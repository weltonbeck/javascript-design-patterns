[voltar](/README.md)

# Memento

O padrão Memento é um padrão comportamental que permite capturar e restaurar o estado interno de um objeto sem violar seu encapsulamento. Ele captura o estado de um objeto em um determinado momento e o armazena em um objeto chamado "memento". Posteriormente, esse estado pode ser restaurado para o objeto original.

O padrão Memento é útil quando você precisa salvar e restaurar o estado de um objeto, geralmente em situações em que você deseja implementar o recurso de desfazer ou salvar e restaurar pontos de verificação.

Os principais elementos do padrão Memento são:

- `Originator (Criador)`: É a classe que possui o estado interno que deseja salvar ou restaurar. Ela cria o memento contendo uma cópia do seu estado atual e também pode restaurar seu estado a partir de um memento.
- `Memento`: É a classe que representa o estado capturado do Originator. Ele fornece métodos para acessar o estado salvo, mas apenas o Originator tem permissão para modificá-lo.
- `Caretaker (Zelador)`: É a classe que é responsável por armazenar e gerenciar os mementos. Ela pode solicitar ao Originator que crie um novo memento ou solicitar ao Originator que restaure o estado de um memento existente.
  
Aqui está um exemplo em JavaScript que ilustra o padrão Memento:

```js
// Originator
class Editor {
  constructor() {
    this.content = '';
  }

  type(text) {
    this.content += text;
  }

  getContent() {
    return this.content;
  }

  save() {
    return new Memento(this.content);
  }

  restore(memento) {
    this.content = memento.getState();
  }
}

// Memento
class Memento {
  constructor(state) {
    this.state = state;
  }

  getState() {
    return this.state;
  }
}

// Caretaker
class History {
  constructor() {
    this.mementos = [];
  }

  push(memento) {
    this.mementos.push(memento);
  }

  pop() {
    return this.mementos.pop();
  }
}

// Uso
const editor = new Editor();
const history = new History();

editor.type('Primeira linha\n');
history.push(editor.save());

editor.type('Segunda linha\n');
editor.type('Terceira linha\n');
history.push(editor.save());

editor.type('Quarta linha\n');
console.log(editor.getContent());

editor.restore(history.pop());
console.log(editor.getContent());

editor.restore(history.pop());
console.log(editor.getContent());
// Primeira linha
// Primeira linha
// Primeira linha

```

Neste exemplo, temos a classe `Editor` que representa o Originator. Ele possui uma propriedade `content` que armazena o estado interno do editor. Os métodos `type` são usados para adicionar texto ao conteúdo. O método `save` cria e retorna um novo memento contendo uma cópia do estado atual do editor. O método `restore` é usado para restaurar o estado do editor a partir de um memento.

A classe `Memento` representa o memento. Ele possui uma propriedade `state` que armazena o estado capturado do Originator. O método `getState` retorna o estado salvo.

A classe `History` atua como o Caretaker. Ela mantém uma lista de mementos e fornece métodos para adicionar mementos à lista (`push`) e recuperar o último memento da lista (`pop`).

No exemplo de uso, criamos uma instância do `Editor` e uma instância do `History`. Em seguida, usamos o método `type` para adicionar algumas linhas de texto ao conteúdo do editor. Após cada adição de texto, usamos o método `save` para criar um memento e adicioná-lo ao histórico.

Em seguida, usamos o método `getContent` para exibir o conteúdo atual do editor, que inclui todas as linhas de texto adicionadas.

Em seguida, usamos o método `restore` para restaurar o estado do editor a partir do último memento no histórico. Isso reverte o editor para o estado anterior, eliminando a última linha de texto adicionada. Exibimos novamente o conteúdo do editor.

Finalmente, usamos o método `restore` novamente para restaurar o estado do editor a partir do memento anterior no histórico. Isso reverte o editor ainda mais, eliminando também a segunda linha de texto adicionada. Exibimos o conteúdo do editor novamente.

A saída resultante será:

    Primeira linha
    Primeira linha
    Primeira linha
    
Isso demonstra como o padrão Memento permite que um objeto capture e restaure seu estado interno sem violar seu encapsulamento. O Originator é responsável por criar e armazenar os mementos, enquanto o Caretaker gerencia os mementos e decide quando restaurar o estado do Originator. Isso permite implementar recursos como desfazer e salvar pontos de verificação em um objeto de forma flexível e desacoplada.