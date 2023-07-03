[voltar](/README.md)

# Decorator

O padrão de projeto Decorator é um padrão estrutural que permite adicionar comportamentos adicionais a objetos de forma dinâmica e flexível. Ele permite estender a funcionalidade de um objeto sem a necessidade de modificar a sua estrutura ou classe base.

O Decorator envolve um objeto em uma série de objetos decoradores que adicionam funcionalidades extras ao objeto original. Cada decorador possui uma interface semelhante à do objeto que está sendo decorado, permitindo que os decoradores sejam usados de forma transparente em conjunto com o objeto base.

Principais elementos do padrão Decorator:

- `Componente`: É a interface ou classe abstrata que define a interface para o objeto original e seus decoradores. Geralmente, possui os métodos comuns a serem implementados tanto pelo objeto quanto pelos decoradores.
- `Objeto Concreto`: É a classe que implementa o Componente e representa o objeto original que será decorado.
- `Decorador`: É a classe abstrata que implementa a interface do Componente e também contém uma referência ao Componente. Pode ser uma classe concreta ou uma classe abstrata com subclasses concretas.
- `Decorador Concreto`: São as subclasses de Decorador, que adicionam funcionalidades extras ao objeto original.

Vamos a um exemplo em JavaScript para ilustrar o padrão Decorator:

```JS
// Componente
class Notificacao {
  enviar(mensagem) {
    console.log(`Notificação: ${mensagem}`);
  }
}

// Decorador
class DecoradorNotificacao {
  constructor(notificacao) {
    this.notificacao = notificacao;
  }

  enviar(mensagem) {
    this.notificacao.enviar(mensagem);
  }
}

// Decorador Concreto
class NotificacaoEmail extends DecoradorNotificacao {
  enviar(mensagem) {
    super.enviar(`Enviando por email: ${mensagem}`);
  }
}

class NotificacaoSMS extends DecoradorNotificacao {
  enviar(mensagem) {
    super.enviar(`Enviando por SMS: ${mensagem}`);
  }
}

// Uso do Decorator
const notificacao = new Notificacao();
const notificacaoComEmail = new NotificacaoEmail(notificacao);
const notificacaoComSMS = new NotificacaoSMS(notificacao);

notificacaoComEmail.enviar("Aviso importante por email");
// Notificação: Enviando por email: Aviso importante por email
notificacaoComSMS.enviar("Alerta urgente por SMS");
// Notificação: Enviando por SMS: Alerta urgente por SMS
```

Neste exemplo, temos o Componente `Notificacao`, que representa o objeto original com um método `enviar(mensagem)` para enviar notificações.

A seguir, temos a classe abstrata `DecoradorNotificacao`, que implementa a mesma interface do `Componente`. Essa classe serve como base para os decoradores concretos e possui uma referência ao `Componente` que será decorado.

As classes `NotificacaoEmail` e `NotificacaoSMS` são os Decoradores Concretos. Cada uma delas estende o `DecoradorNotificacao` e adiciona funcionalidades extras aos métodos `enviar(mensagem)` do `Componente` original.

No uso do padrão Decorator, criamos uma notificação básica `notificacao`, em seguida, criamos dois decoradores: `notificacaoComEmail` e `notificacaoComSMS`, que envolvem a notificação básica e adicionam funcionalidades de envio por email e SMS, respectivamente.

Ao chamar o método `enviar(mensagem)` em cada decorador, a mensagem é passada para o decorador anterior e, em seguida, para o objeto original, garantindo que a funcionalidade extra seja adicionada ao comportamento padrão do objeto original.

No exemplo, quando chamamos `notificacaoComEmail.enviar("Aviso importante por email")`, a mensagem é enviada primeiro pelo decorador de email, que adiciona a prefixo "Enviando por email:", e em seguida, é chamado o método `enviar()` do decorador anterior (`DecoradorNotificacao`), que, por sua vez, chama o método `enviar()` do objeto original `notificacao`.

Da mesma forma, ao chamar `notificacaoComSMS.enviar("Alerta urgente por SMS")`, a mensagem é enviada pelo decorador de SMS, que adiciona o prefixo "Enviando por SMS:", e em seguida, passa para o decorador anterior (`DecoradorNotificacao`), que, por fim, chama o método `enviar()` do objeto original.

A saída resultante será:

    Notificação: Enviando por email: Aviso importante por email
    Notificação: Enviando por SMS: Alerta urgente por SMS
    
Isso demonstra como o padrão Decorator permite estender o comportamento de um objeto original de forma dinâmica e transparente, adicionando funcionalidades extras através de decoradores. Os decoradores podem ser combinados e adicionados em qualquer ordem, oferecendo grande flexibilidade na composição de comportamentos adicionais aos objetos.