[voltar](/README.md)

# Flyweight

O padrão de projeto Flyweight é um padrão estrutural que visa otimizar o uso de objetos compartilhando dados comuns entre várias instâncias. Ele é útil quando temos um grande número de objetos semelhantes que consomem muita memória, e queremos reduzir essa duplicação de dados.

O padrão Flyweight consiste em separar os dados intrínsecos (compartilhados) dos dados extrínsecos (específicos de cada objeto). Os dados intrínsecos são armazenados de forma centralizada e compartilhada entre várias instâncias de objetos, enquanto os dados extrínsecos são passados como parâmetros para os objetos.

Dessa forma, ao invés de criar um novo objeto para cada instância, o Flyweight reutiliza objetos existentes, economizando memória e melhorando o desempenho do sistema.

Principais elementos do padrão Flyweight:

- `Flyweight`: É a interface ou classe abstrata que define a interface comum para os objetos flyweight. Ela declara métodos que operam sobre os dados extrínsecos.
- `Flyweight Concreto`: É a classe que implementa a interface flyweight. Ela armazena os dados intrínsecos e fornece a implementação dos métodos definidos na interface flyweight.
- `Flyweight Factory`: É a classe responsável por criar e gerenciar os objetos flyweight. Ela mantém um cache dos objetos flyweight existentes e os fornece quando solicitados.
  
Vamos ver um exemplo em JavaScript para ilustrar o padrão Flyweight:

```JS
// Flyweight
class Ponto {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  desenhar() {
    console.log(`Desenhando ponto em (${this.x}, ${this.y})`);
  }
}

// Flyweight Factory
class PontoFactory {
  constructor() {
    this.pontos = {};
  }

  criarPonto(x, y) {
    const chave = `${x}-${y}`;

    if (!this.pontos[chave]) {
      this.pontos[chave] = new Ponto(x, y);
    }

    return this.pontos[chave];
  }

  obterQuantidadePontos() {
    return Object.keys(this.pontos).length;
  }
}

// Uso do Flyweight
const pontoFactory = new PontoFactory();
const ponto1 = pontoFactory.criarPonto(1, 2);
const ponto2 = pontoFactory.criarPonto(3, 4);
const ponto3 = pontoFactory.criarPonto(1, 2);

ponto1.desenhar();
ponto2.desenhar();
ponto3.desenhar();
// Desenhando ponto em (1, 2)
// Desenhando ponto em (3, 4)
// Desenhando ponto em (1, 2)

console.log(`Quantidade de pontos criados: ${pontoFactory.obterQuantidadePontos()}`);
// Quantidade de pontos criados: 2

```

Neste exemplo, temos a classe `Ponto`, que é o flyweight concreto. Ela armazena os dados intrínsecos (x e y) e implementa o método `desenhar` para desenhar o ponto em determinadas coordenadas.

Em seguida, temos a classe `PontoFactory`, que é a flyweight factory. Ela mantém um cache dos pontos existentes e fornece uma interface para criar novos pontos. A factory verifica se o ponto já existe no cache antes de criá-lo. Se o ponto já existir, ele é reutilizado; caso contrário, um novo ponto é criado e adicionado ao cache.

No exemplo de uso, criamos uma instância da `PontoFactory` e usamos-a para criar três pontos: `ponto1`, `ponto2` e `ponto3`. Observe que `ponto1` e `ponto3` têm as mesmas coordenadas (1, 2). No entanto, apenas um único objeto `Ponto` é criado para essas coordenadas, pois o Flyweight reutiliza o objeto existente do cache.

Em seguida, chamamos o método `desenhar` em cada ponto para representar graficamente os pontos. E, por fim, exibimos a quantidade de pontos criados usando o método `obterQuantidadePontos` da `PontoFactory`.

A saída resultante será:

    Desenhando ponto em (1, 2)
    Desenhando ponto em (3, 4)
    Desenhando ponto em (1, 2)
    Quantidade de pontos criados: 2

Isso demonstra como o padrão Flyweight reduz a duplicação de objetos, reutilizando os objetos existentes quando possível. Ele economiza memória ao compartilhar dados comuns entre várias instâncias. No exemplo, mesmo que tenhamos criado três pontos com as mesmas coordenadas (1, 2), apenas dois objetos `Ponto` foram criados, resultando em uma redução de consumo de memória.
