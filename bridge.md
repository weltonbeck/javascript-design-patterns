[voltar](/README.md)

# Bridge

O padrão Bridge é um padrão de projeto estrutural que separa uma abstração da sua implementação, permitindo que elas variem independentemente. Ele é útil quando queremos evitar uma explosão de subclasses ao lidar com diferentes combinações de abstrações e implementações.

O padrão Bridge é composto por duas hierarquias: a hierarquia da abstração e a hierarquia da implementação. A classe abstrata da hierarquia da abstração possui uma referência para um objeto da hierarquia da implementação. Através dessa referência, os métodos da classe abstrata delegam o trabalho para a implementação correspondente.

Aqui está um exemplo em JavaScript que ilustra o padrão Bridge:

```JS
// Implementação da hierarquia da implementação
class DispositivoSaida {
  renderizarForma(forma) {
    throw new Error('O método renderizarForma deve ser implementado.');
  }
}

class Tela extends DispositivoSaida {
  renderizarForma(forma) {
    console.log(`Renderizando a forma ${forma} na tela.`);
  }
}

class Impressora extends DispositivoSaida {
  renderizarForma(forma) {
    console.log(`Imprimindo a forma ${forma} na impressora.`);
  }
}

// Abstração
class Forma {
  constructor(dispositivo) {
    this.dispositivo = dispositivo;
  }

  desenhar() {
    throw new Error('O método desenhar deve ser implementado.');
  }
}

// Abstração refinada
class Circulo extends Forma {
  constructor(dispositivo, x, y, raio) {
    super(dispositivo);
    this.x = x;
    this.y = y;
    this.raio = raio;
  }

  desenhar() {
    this.dispositivo.renderizarForma(`Círculo de raio ${this.raio} no ponto (${this.x}, ${this.y})`);
  }
}

class Quadrado extends Forma {
  constructor(dispositivo, x, y, lado) {
    super(dispositivo);
    this.x = x;
    this.y = y;
    this.lado = lado;
  }

  desenhar() {
    this.dispositivo.renderizarForma(`Quadrado de lado ${this.lado} no ponto (${this.x}, ${this.y})`);
  }
}

// Uso da Bridge
const tela = new Tela();
const impressora = new Impressora();

const circulo = new Circulo(tela, 100, 100, 50);
circulo.desenhar();
// Saída: Renderizando a forma Círculo de raio 50 no ponto (100, 100) na tela.

const quadrado = new Quadrado(impressora, 200, 200, 80);
quadrado.desenhar();
// Saída: Imprimindo a forma Quadrado de lado 80 no ponto (200, 200) na impressora.

```

Neste exemplo, temos a hierarquia da implementação com as classes `DispositivoSaida` como a classe abstrata e `Tela` e `Impressora` como implementações concretas.

Em seguida, temos a classe abstrata `Forma` que recebe uma instância de `DispositivoSaida` no construtor e possui o método `desenhar()`. As classes `Circulo` e `Quadrado` estendem Forma e implementam o método `desenhar()` de acordo com cada forma específica.

No uso da bridge, criamos instâncias das implementações concretas, `Tela` e `Impressora`, e passamos essas instâncias para as abstrações, `Circulo` e `Quadrado`. Ao chamar o método `desenhar()`, o trabalho é delegado para a implementação correspondente, e a forma é renderizada na tela ou impressa, dependendo do dispositivo de saída utilizado.

Dessa forma, o padrão Bridge permite que as abstrações de formas geométricas sejam desenhadas em diferentes dispositivos de saída sem que as classes das formas e dos dispositivos de saída sejam fortemente acopladas.

No exemplo, a primeira chamada `circulo.desenhar()` utiliza o dispositivo de saída `Tela`, resultando na saída `"Renderizando a forma Círculo de raio 50 no ponto (100, 100) na tela"`. A segunda chamada `quadrado.desenhar()` utiliza o dispositivo de saída `Impressora`, resultando na saída `"Imprimindo a forma Quadrado de lado 80 no ponto (200, 200) na impressora"`.

Isso ilustra como o padrão Bridge permite que diferentes abstrações (formas) e diferentes implementações (dispositivos de saída) possam variar independentemente. Novas formas e dispositivos de saída podem ser adicionados sem afetar as classes existentes, proporcionando uma maior flexibilidade e extensibilidade no sistema.

O padrão Bridge é especialmente útil quando se espera que a hierarquia das abstrações e a hierarquia das implementações evoluam independentemente ou quando há várias combinações possíveis entre as abstrações e as implementações. Ele permite que o código seja mais modular, facilitando a manutenção, a extensão e a reutilização de componentes em diferentes contextos.