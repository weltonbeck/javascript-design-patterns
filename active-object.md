[voltar](/README.md)

# Active object

O padrão Active Object é um padrão de projeto concorrente que encapsula a execução de um método em um objeto separado, permitindo que seja executado de forma assíncrona. Ele é útil quando há a necessidade de executar operações em segundo plano sem bloquear a execução do programa principal.

O padrão Active Object envolve o objeto com uma interface que permite a chamada de métodos assíncronos. Essas chamadas são colocadas em uma fila de requisições, e um executor de tarefas processa a fila sequencialmente.

Vamos ver um exemplo em JavaScript:

```js
class ActiveObject {
  constructor() {
    this.queue = [];
  }

  async doSomething(value) {
    return new Promise(resolve => {
      this.queue.push(() => {
        // Simulando um atraso assíncrono
        setTimeout(() => {
          console.log(`Executando doSomething com valor ${value}`);
          resolve();
        }, 2000);
      });

      if (this.queue.length === 1) {
        this.processQueue();
      }
    });
  }

  processQueue() {
    const task = this.queue[0];
    task();

    this.queue.shift();

    if (this.queue.length > 0) {
      setTimeout(() => {
        this.processQueue();
      }, 0);
    }
  }
}

// Uso
const activeObject = new ActiveObject();

activeObject.doSomething(1);
activeObject.doSomething(2);
activeObject.doSomething(3);
```

Neste exemplo, temos a classe `ActiveObject` que encapsula a execução assíncrona do método `doSomething`. Quando o método é chamado, ele coloca uma função na fila de requisições e, se a fila estiver vazia, inicia o processamento da fila chamando o método `processQueue`.

A função `doSomething` utiliza uma `Promise` para simular um atraso assíncrono de 2 segundos. Quando o tempo de espera é concluído, a função é executada e a `Promise` é resolvida.

No exemplo de uso, criamos uma instância de `ActiveObject` chamada `activeObject` e chamamos o método `doSomething` três vezes com diferentes valores. Como a execução é assíncrona, as chamadas são colocadas na fila e processadas sequencialmente.

A saída resultante exibirá a execução do método `doSomething` para cada valor após um atraso de 2 segundos.

O padrão Active Object permite a execução assíncrona de métodos em segundo plano, evitando bloqueios na execução principal. Ele é útil em situações em que operações demoradas precisam ser executadas de forma assíncrona e não devem interferir na execução do programa principal.
