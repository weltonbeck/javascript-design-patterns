[voltar](/README.md)

# Iterator

O padrão Iterator é um padrão comportamental que fornece uma maneira de acessar os elementos de uma coleção sequencial sem expor a sua representação subjacente. Ele permite percorrer os elementos de uma coleção de forma transparente, sem conhecer os detalhes de implementação da coleção.

O padrão Iterator possui dois principais elementos: o Iterador e a Coleção.

- `Iterador`: É uma interface ou classe abstrata que define os métodos para percorrer os elementos da coleção. Geralmente, possui métodos como next para obter o próximo elemento, hasNext para verificar se há mais elementos e possivelmente métodos adicionais para operações como remoção de elementos.
- `Coleção`: É a classe que contém os elementos a serem percorridos. Ela fornece um método para obter um iterador, que permite percorrer seus elementos de forma sequencial.

Aqui está um exemplo em JavaScript que ilustra o padrão Iterator:

```js
// Iterador
class Iterator {
  constructor(collection) {
    this.collection = collection;
    this.index = 0;
  }

  next() {
    if (this.hasNext()) {
      return this.collection[this.index++];
    }
    return null;
  }

  hasNext() {
    return this.index < this.collection.length;
  }
}

// Coleção
class ListaDeNomes {
  constructor() {
    this.nomes = [];
  }

  adicionar(nome) {
    this.nomes.push(nome);
  }

  criarIterador() {
    return new Iterator(this.nomes);
  }
}

// Uso
const lista = new ListaDeNomes();
lista.adicionar("João");
lista.adicionar("Maria");
lista.adicionar("Pedro");

const iterador = lista.criarIterador();

while (iterador.hasNext()) {
  console.log(iterador.next());
}
// João
// Maria
// Pedro

```

Neste exemplo, temos a classe `Iterator` que implementa a iteração sequencial sobre uma coleção. Ele mantém uma referência para a coleção e um índice que indica a posição atual durante o percurso. Os métodos `next` e `hasNext` permitem obter o próximo elemento e verificar se existem mais elementos, respectivamente.

A classe `ListaDeNomes` é a coleção que contém os elementos a serem percorridos. Ela possui um array `nomes` onde os nomes são armazenados. O método `adicionar` permite adicionar nomes à lista. O método `criarIterador` retorna uma instância do iterador associado à lista, permitindo percorrer os nomes.

No exemplo de uso, criamos uma instância da classe `ListaDeNomes` e adicionamos alguns nomes à lista. Em seguida, chamamos o método `criarIterador` para obter um iterador associado à lista. Usamos um loop `while` para percorrer os elementos usando o iterador, imprimindo cada nome.

A saída resultante será:

    João
    Maria
    Pedro

Isso demonstra como o padrão Iterator permite percorrer os elementos de uma coleção sem expor a sua estrutura interna. O iterador encapsula a lógica de iteração, permitindo que os elementos sejam acessados sequencialmente de maneira uniforme, independentemente da implementação específica da coleção. Isso promove a modularidade e reutilização de código.
