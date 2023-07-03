[voltar](/README.md)

# Abstract factory

O padrão Abstract Factory (ou Fábrica Abstrata) é um padrão de projeto de criação que permite a criação de famílias de objetos relacionados sem especificar suas classes concretas. Ele fornece uma interface para criar objetos de várias classes relacionadas, sem expor a lógica de criação específica.

O Abstract Factory é útil quando um sistema deve ser independente de como objetos são criados, compostos ou representados. Ele permite que as famílias de objetos sejam criadas de forma consistente e garante que os objetos criados sejam compatíveis entre si.

Aqui está um exemplo em JavaScript que ilustra o padrão Abstract Factory:

```JS
// Abstract Factory de Componentes Visuais
class ComponenteFactory {
  criarBotao() {
    throw new Error('Método "criarBotao" deve ser implementado pela subclasse');
  }

  criarCaixaTexto() {
    throw new Error('Método "criarCaixaTexto" deve ser implementado pela subclasse');
  }
}

// Concrete Factory de Componentes Visuais - Estilo Claro
class ComponenteFactoryClaro extends ComponenteFactory {
  criarBotao() {
    return new BotaoClaro();
  }

  criarCaixaTexto() {
    return new CaixaTextoClaro();
  }
}

// Concrete Factory de Componentes Visuais - Estilo Escuro
class ComponenteFactoryEscuro extends ComponenteFactory {
  criarBotao() {
    return new BotaoEscuro();
  }

  criarCaixaTexto() {
    return new CaixaTextoEscuro();
  }
}

// Classes de Componentes Visuais - Botões
class BotaoClaro {
  renderizar() {
    console.log('Renderizando botão claro...');
  }
}

class BotaoEscuro {
  renderizar() {
    console.log('Renderizando botão escuro...');
  }
}

// Classes de Componentes Visuais - Caixas de Texto
class CaixaTextoClaro {
  renderizar() {
    console.log('Renderizando caixa de texto claro...');
  }
}

class CaixaTextoEscuro {
  renderizar() {
    console.log('Renderizando caixa de texto escuro...');
  }
}

// Uso do Abstract Factory
const estiloClaro = new ComponenteFactoryClaro();
const estiloEscuro = new ComponenteFactoryEscuro();

const botaoClaro = estiloClaro.criarBotao();
const caixaTextoClaro = estiloClaro.criarCaixaTexto();

const botaoEscuro = estiloEscuro.criarBotao();
const caixaTextoEscuro = estiloEscuro.criarCaixaTexto();

botaoClaro.renderizar();         // Saída: Renderizando botão claro...
caixaTextoClaro.renderizar();    // Saída: Renderizando caixa de texto claro...

botaoEscuro.renderizar();        // Saída: Renderizando botão escuro...
caixaTextoEscuro.renderizar();   // Saída: Renderizando caixa de texto escuro...


```

No exemplo, temos as classes concretas `BotaoClaro`, `BotaoEscuro`, `CaixaTextoClaro` e `CaixaTextoEscuro`, que representam os diferentes tipos de botões e caixas de texto correspondentes aos estilos claro e escuro.

Ao usar o Abstract Factory, criamos instâncias das Concrete Factories correspondentes aos estilos que desejamos, ou seja, `ComponenteFactoryClaro` e `ComponenteFactoryEscuro`. Em seguida, usamos essas instâncias para criar objetos concretos chamando os métodos de criação correspondentes, como `criarBotao()` e `criarCaixaTexto()`.

Assim, podemos criar botões e caixas de texto que correspondem aos estilos específicos, como `botaoClaro` e `caixaTextoClaro` para o estilo claro, e `botaoEscuro` e `caixaTextoEscuro` para o estilo escuro. Cada objeto pode ser renderizado de acordo com sua implementação específica.

Dessa forma, o padrão Abstract Factory nos permite criar famílias de objetos relacionados sem nos preocuparmos com as classes concretas específicas, fornecendo uma interface comum para a criação desses objetos. Isso nos permite manter a consistência entre os objetos criados e tornar o código mais flexível para trabalhar com diferentes famílias de objetos.






