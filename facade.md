[voltar](/README.md)

# Facade

O padrão de projeto Facade é um padrão estrutural que fornece uma interface simplificada para interagir com um sistema complexo. Ele oculta a complexidade interna do sistema, fornecendo uma interface unificada que facilita o uso e reduz a dependência de componentes individuais.

O Facade atua como uma camada de abstração entre o cliente e os componentes internos do sistema, encapsulando a lógica complexa e fornecendo métodos simples e de alto nível para realizar tarefas específicas. Isso permite que o cliente interaja com o sistema de forma mais simples, sem precisar conhecer os detalhes internos e a complexidade dos componentes individuais.

Principais elementos do padrão Facade:

- `Facade`: É a classe que fornece uma interface simplificada para o cliente interagir com o sistema complexo. Ele conhece os componentes internos do sistema e coordena suas ações para atender às solicitações do cliente.
- `Subsistemas`: São os componentes individuais e complexos do sistema que são ocultados pelo Facade. Eles possuem funcionalidades específicas e são usados pelo Facade para realizar as tarefas solicitadas pelo cliente.
  
Vamos ver um exemplo em JavaScript para ilustrar o padrão Facade:

```JS
// Subsistema 1
class ServicoAutenticacao {
  autenticar(usuario, senha) {
    console.log(`Autenticando usuário ${usuario}...`);
    // Lógica de autenticação
    return true;
  }
}

// Subsistema 2
class ServicoAutorizacao {
  verificarPermissao(usuario, recurso) {
    console.log(`Verificando permissão do usuário ${usuario} para acessar o recurso ${recurso}...`);
    // Lógica de verificação de permissão
    return true;
  }
}

// Subsistema 3
class ServicoNotificacao {
  enviarNotificacao(usuario, mensagem) {
    console.log(`Enviando notificação para o usuário ${usuario}: ${mensagem}`);
    // Lógica de envio de notificação
  }
}

// Facade
class SistemaNotificacao {
  constructor() {
    this.servicoAutenticacao = new ServicoAutenticacao();
    this.servicoAutorizacao = new ServicoAutorizacao();
    this.servicoNotificacao = new ServicoNotificacao();
  }

  notificarUsuario(usuario, recurso, mensagem) {
    if (this.servicoAutenticacao.autenticar(usuario, senha)) {
      if (this.servicoAutorizacao.verificarPermissao(usuario, recurso)) {
        this.servicoNotificacao.enviarNotificacao(usuario, mensagem);
      } else {
        console.log(`Usuário ${usuario} não tem permissão para acessar o recurso ${recurso}.`);
      }
    } else {
      console.log(`Falha na autenticação do usuário ${usuario}.`);
    }
  }
}

// Uso do Facade
const sistemaNotificacao = new SistemaNotificacao();
sistemaNotificacao.notificarUsuario("joao123", "dashboard", "Nova mensagem recebida");
// Autenticando usuário joao123...
// Verificando permissão do usuário joao123 para acessar o recurso dashboard...
// Enviando notificação para o usuário joao123: Nova mensagem recebida

```

Neste exemplo, temos três subsistemas que representam funcionalidades complexas: `ServicoAutenticacao`, `ServicoAutorizacao` e `ServicoNotificacao`. Esses subsistemas possuem lógica específica para autenticação, verificação de permissão e envio de notificações.

Em seguida, temos a classe `SistemaNotificacao`, que atua como o Facade. Ela conhece os subsistemas internos e fornece um método simplificado `notificarUsuario(usuario, recurso, mensagem)` para o cliente interagir com o sistema de notificação.

No método `notificarUsuario`, o Facade coordena as ações dos subsistemas para notificar um usuário sobre uma mensagem em um determinado recurso. Primeiro, realiza a autenticação do usuário chamando o método `autenticar` do `ServicoAutenticacao`. Se a autenticação for bem-sucedida, verifica a permissão do usuário para acessar o recurso através do método `verificarPermissao` do `ServicoAutorizacao`. Se o usuário tiver permissão, envia a notificação chamando o método `enviarNotificacao` do `ServicoNotificacao`.

Ao usar o Facade, podemos simplificar a interação do cliente com o sistema complexo de notificações. O cliente não precisa conhecer os detalhes de autenticação, autorização e envio de notificações, mas apenas chamar o método `notificarUsuario` do Facade, passando os parâmetros necessários.

No exemplo de uso, criamos uma instância do `SistemaNotificacao` e chamamos o método `notificarUsuario` com o usuário "joao123", o recurso "dashboard" e a mensagem "Nova mensagem recebida". O Facade coordena as ações dos subsistemas internos e realiza a notificação, exibindo as mensagens apropriadas de autenticação, permissão e envio de notificação.

A saída resultante será:

    Autenticando usuário joao123...
    Verificando permissão do usuário joao123 para acessar o recurso dashboard...
    Enviando notificação para o usuário joao123: Nova mensagem recebida

Isso demonstra como o padrão Facade simplifica o uso de sistemas complexos, ocultando a complexidade dos subsistemas e fornecendo uma interface unificada para interagir com eles. O Facade permite que o cliente trabalhe com uma interface simples e de alto nível, enquanto as ações complexas são tratadas internamente pelo Facade e pelos subsistemas.
