[voltar](/README.md)

# Composite

O padrão Composite é um padrão de projeto estrutural que permite tratar objetos individuais e coleções de objetos de maneira uniforme. Ele organiza os objetos em uma estrutura de árvore hierárquica, permitindo que os clientes tratem objetos individuais e grupos de objetos de forma polimórfica.

O padrão Composite é composto por três elementos principais: o componente base, as folhas e os nós compostos. O componente base define a interface comum para todos os elementos da estrutura. As folhas representam os objetos individuais, enquanto os nós compostos representam as coleções de objetos.

Os nós compostos possuem uma lista de referências para os componentes filhos, que podem ser tanto folhas como outros nós compostos. Eles delegam as operações para os componentes filhos, permitindo que as operações sejam aplicadas recursivamente em toda a estrutura.

Aqui está um exemplo em JavaScript que ilustra o padrão Composite:

```JS
// Componente base
class Categoria {
  constructor(nome) {
    this.nome = nome;
    this.subcategorias = [];
  }

  adicionarSubcategoria(subcategoria) {
    this.subcategorias.push(subcategoria);
  }

  removerSubcategoria(subcategoria) {
    const indice = this.subcategorias.indexOf(subcategoria);
    if (indice !== -1) {
      this.subcategorias.splice(indice, 1);
    }
  }

  exibirCategorias() {
    console.log(`Categoria: ${this.nome}`);
    for (const subcategoria of this.subcategorias) {
      subcategoria.exibirCategorias();
    }
  }
}

// Uso do Composite
const categoriaPrincipal = new Categoria('Tecnologia');

const subcategoria1 = new Categoria('Programação');
const subcategoria2 = new Categoria('Design');

const subsubcategoria1 = new Categoria('JavaScript');
const subsubcategoria2 = new Categoria('Python');

subcategoria1.adicionarSubcategoria(subsubcategoria1);
subcategoria1.adicionarSubcategoria(subsubcategoria2);

categoriaPrincipal.adicionarSubcategoria(subcategoria1);
categoriaPrincipal.adicionarSubcategoria(subcategoria2);

const subcategoria3 = new Categoria('UI/UX');

subcategoria2.adicionarSubcategoria(subcategoria3);

categoriaPrincipal.exibirCategorias();
// Categoria: Tecnologia
// Categoria: Programação
// Categoria: JavaScript
// Categoria: Python
// Categoria: Design
// Categoria: UI/UX
```

Neste exemplo, temos a classe `Categoria` como o componente base. Cada instância de `Categoria` possui um nome e uma lista de subcategorias. O método `adicionarSubcategoria()` permite adicionar uma subcategoria à lista, enquanto o método `removerSubcategoria()` permite remover uma subcategoria da lista. O método `exibirCategorias()` percorre recursivamente a estrutura hierárquica e exibe o nome de cada categoria.

No uso do Composite, criamos uma categoria principal chamada 'Tecnologia'. Em seguida, criamos várias subcategorias, como 'Programação', 'Design' e 'UI/UX'. Além disso, definimos subcategorias para 'Programação', como 'JavaScript' e 'Python'.

Ao chamar o método `exibirCategorias()` na categoria principal, toda a estrutura hierárquica de categorias é percorrida e exibida, resultando na seguinte saída:

    Categoria: Tecnologia
    Categoria: Programação
    Categoria: JavaScript
    Categoria: Python
    Categoria: Design
    Categoria: UI/UX

Isso mostra como o padrão Composite permite tratar tanto as categorias individuais como as hierarquias de subcategorias de forma consistente. É possível adicionar, remover e exibir categorias independentemente de serem categorias principais ou subcategorias, fornecendo uma estrutura flexível e escalável para gerenciar categorias em um sistema.