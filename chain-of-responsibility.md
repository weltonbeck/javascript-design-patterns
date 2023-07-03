[voltar](/README.md)

# Chain of Responsibility

O padrão Chain of Responsibility é um padrão comportamental que permite que uma solicitação seja passada ao longo de uma cadeia de objetos receptores, até que um objeto possa lidar com essa solicitação. Cada objeto receptor na cadeia tem a oportunidade de lidar com a solicitação ou passá-la para o próximo objeto na cadeia.

Esse padrão promove a ideia de desacoplamento entre o remetente de uma solicitação e seus destinatários, permitindo que diferentes objetos possam tratar a solicitação de maneiras diferentes, sem que o remetente precise conhecer detalhes sobre esses objetos.

Principais elementos do padrão Chain of Responsibility:

- `Handler (Manipulador)`: É a interface que define os métodos para lidar com uma solicitação. Pode ter um método para manipular a solicitação e um método para definir o próximo manipulador na cadeia.
- `ConcreteHandler (Manipulador Concreto)`: É a classe que implementa a interface Handler. Cada manipulador concreto tem a oportunidade de lidar com a solicitação e/ou passá-la para o próximo manipulador na cadeia.
- `Client (Cliente)`: É o objeto que inicia a solicitação e a passa para o primeiro manipulador na cadeia.

Vamos ver um exemplo em JavaScript para ilustrar o padrão Chain of Responsibility:

```JS
// Handler
class ProcessadorDeRequisicao {
  setProximo(processador) {
    this.proximo = processador;
  }

  processar(requisicao) {
    throw new Error("Método processar deve ser implementado pelos subclasse.");
  }
}

// ConcreteHandler
class ProcessadorDeRequisicaoAutenticacao extends ProcessadorDeRequisicao {
  processar(requisicao) {
    if (requisicao.tipo === 'autenticacao') {
      console.log('Processando requisição de autenticação');
      // Lógica de processamento
    } else if (this.proximo) {
      this.proximo.processar(requisicao);
    }
  }
}

class ProcessadorDeRequisicaoAutorizacao extends ProcessadorDeRequisicao {
  processar(requisicao) {
    if (requisicao.tipo === 'autorizacao') {
      console.log('Processando requisição de autorização');
      // Lógica de processamento
    } else if (this.proximo) {
      this.proximo.processar(requisicao);
    }
  }
}

class ProcessadorDeRequisicaoLog extends ProcessadorDeRequisicao {
  processar(requisicao) {
    if (requisicao.tipo === 'log') {
      console.log('Processando requisição de log');
      // Lógica de processamento
    } else if (this.proximo) {
      this.proximo.processar(requisicao);
    }
  }
}

// Cliente
const processadorAutenticacao = new ProcessadorDeRequisicaoAutenticacao();
const processadorAutorizacao = new ProcessadorDeRequisicaoAutorizacao();
const processadorLog = new ProcessadorDeRequisicaoLog();

processadorAutenticacao.setProximo(processadorAutorizacao);
processadorAutorizacao.setProximo(processadorLog);

const requisicao = { tipo: 'log' };
processadorAutenticacao.processar(requisicao);
// Processando requisição de log

```

Neste exemplo, temos três classes concretas que implementam a interface ProcessadorDeRequisicao e atuam como manipuladores na cadeia: `ProcessadorDeRequisicaoAutenticacao`, `ProcessadorDeRequisicaoAutorizacao` e `ProcessadorDeRequisicaoLog`. Cada um desses manipuladores tem a oportunidade de processar a solicitação com base no tipo de requisição recebida. Se um manipulador pode lidar com a solicitação, ele executa a lógica de processamento correspondente. Caso contrário, passa a solicitação para o próximo manipulador na cadeia.

No exemplo de uso, criamos uma instância de cada manipulador e definimos a ordem em que eles devem ser encadeados. Em seguida, criamos uma requisição com o tipo "log" e chamamos o método `processar` do primeiro manipulador na cadeia, `processadorAutenticacao`.

A saída resultante será:

    Processando requisição de log

Isso demonstra como o padrão Chain of Responsibility permite que diferentes manipuladores tenham a oportunidade de processar uma solicitação de maneira sequencial. Cada manipulador verifica se pode lidar com a solicitação e, se não puder, passa a solicitação para o próximo manipulador na cadeia. Dessa forma, a responsabilidade de lidar com a solicitação é delegada ao manipulador apropriado, proporcionando um fluxo flexível e desacoplado.