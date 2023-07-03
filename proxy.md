[voltar](/README.md)

# Proxy

O padrão de projeto Proxy é um padrão estrutural que permite controlar o acesso a um objeto por meio de um objeto intermediário, chamado de proxy. O proxy atua como uma camada de abstração entre o cliente e o objeto real, permitindo adicionar funcionalidades adicionais, como verificação de permissões, armazenamento em cache, controle de acesso, entre outros.

O Proxy segue a mesma interface que o objeto real, permitindo que o cliente interaja com ele da mesma maneira que interagiria com o objeto real. O proxy, então, encaminha as chamadas de método e manipula essas chamadas de acordo com a lógica adicional que foi implementada.

Principais elementos do padrão Proxy:

- `Proxy`: É a interface que define a mesma interface do objeto real. O proxy possui uma referência ao objeto real e pode executar ações adicionais antes ou depois de encaminhar as chamadas para o objeto real.
- `Proxy Concreto`: É a classe que implementa a interface proxy. Ele mantém uma referência ao objeto real e pode adicionar funcionalidades extras antes ou depois de encaminhar as chamadas para o objeto real.
- `Objeto Real`: É a classe que contém a lógica principal e realiza as operações reais. O objeto real é encapsulado pelo proxy, e o cliente interage principalmente com o proxy, em vez de interagir diretamente com o objeto real.

Vamos ver um exemplo em JavaScript para ilustrar o padrão Proxy:

```JS
// Objeto Real
class ServicoDeNotificacao {
  enviarMensagem(mensagem) {
    console.log(`Enviando mensagem: ${mensagem}`);
  }
}

// Proxy
class ProxyServicoDeNotificacao {
  constructor() {
    this.servicoReal = new ServicoDeNotificacao();
  }

  enviarMensagem(mensagem) {
    if (this.verificarPermissao()) {
      this.servicoReal.enviarMensagem(mensagem);
    } else {
      console.log("Sem permissão para enviar mensagem.");
    }
  }

  verificarPermissao() {
    // Lógica de verificação de permissão
    return true;
  }
}

// Uso do Proxy
const proxy = new ProxyServicoDeNotificacao();
proxy.enviarMensagem("Mensagem importante");
// Enviando mensagem: Mensagem importante
```

Neste exemplo, temos a classe `ServicoDeNotificacao`, que é o objeto real. Ele contém a lógica principal para enviar uma mensagem.

Em seguida, temos a classe `ProxyServicoDeNotificacao`, que é o proxy concreto. Ele mantém uma referência ao objeto real e adiciona uma verificação de permissão antes de encaminhar a chamada para o objeto real. Se a verificação de permissão for bem-sucedida, a mensagem é enviada pelo objeto real; caso contrário, uma mensagem de "Sem permissão" é exibida.

No exemplo de uso, criamos uma instância do `ProxyServicoDeNotificacao` e chamamos o método enviarMensagem passando a mensagem "`Mensagem importante`". O proxy realiza a verificação de permissão e encaminha a chamada para o objeto real se a permissão for concedida.

A saída resultante será:

    Enviando mensagem: Mensagem importante

Isso demonstra como o padrão Proxy permite controlar o acesso ao objeto real. O proxy adiciona uma camada adicional de lógica, como a verificação de permissões, antes de permitir que o cliente acesse o objeto real. Essa abordagem é útil quando queremos adicionar funcionalidades extras ao acesso ao objeto real, sem modificar diretamente a lógica do objeto real.

Além da verificação de permissões, o padrão Proxy também pode ser usado para adicionar outras funcionalidades, como armazenamento em cache, controle de acesso, registro de log, criptografia, entre outras. O proxy atua como um intermediário entre o cliente e o objeto real, controlando o acesso e adicionando essas funcionalidades extras de acordo com as necessidades.

O padrão Proxy é útil quando queremos adicionar uma lógica adicional ao acesso a um objeto, sem modificar o objeto real em si. Ele ajuda a manter a separação de responsabilidades e permite uma maior flexibilidade na adição de funcionalidades extras.
