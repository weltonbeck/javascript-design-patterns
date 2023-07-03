[voltar](/README.md)

# Prototype

O padrão Prototype (ou Protótipo) é um padrão de projeto que permite a criação de novos objetos através da clonagem de um objeto existente, chamado de protótipo. O objetivo principal desse padrão é evitar a criação de objetos repetidos a partir do zero, economizando recursos computacionais.

O Prototype é útil quando a criação de um objeto é custosa ou complexa, e desejamos criar novas instâncias com base em um objeto já existente, evitando a sobrecarga de criação. Ele também é útil quando precisamos criar objetos com configurações iniciais semelhantes, mas que podem ser personalizadas posteriormente.

A linguagem JavaScript já possui suporte nativo ao padrão Prototype através do uso do protótipo do objeto. Veja um exemplo em JavaScript que ilustra o padrão Prototype:

```JS
// Classe de exemplo: Pessoa
class Pessoa {
  constructor(nome, idade) {
    this.nome = nome;
    this.idade = idade;
  }

  apresentar() {
    console.log(`Olá, meu nome é ${this.nome} e tenho ${this.idade} anos.`);
  }

  clone() {
    return Object.assign(Object.create(Object.getPrototypeOf(this)), this);
  }
}

// Criação do protótipo
const prototipoPessoa = new Pessoa("João", 30);

// Clonagem do protótipo
const pessoa1 = prototipoPessoa.clone();
pessoa1.apresentar(); // Saída: Olá, meu nome é João e tenho 30 anos.

// Modificação da propriedade clonada
pessoa1.nome = "Maria";
pessoa1.apresentar(); // Saída: Olá, meu nome é Maria e tenho 30 anos.

// Criação de outra instância clonando o protótipo
const pessoa2 = prototipoPessoa.clone();
pessoa2.apresentar(); // Saída: Olá, meu nome é João e tenho 30 anos.
```

Nesse exemplo, temos a classe `Pessoa` que possui propriedades como `nome` e `idade`, bem como métodos como `apresentar()`. A classe também possui um método `clone()` que realiza a clonagem do objeto usando a função `Object.assign()` para criar uma nova instância com o mesmo protótipo.

Ao criar uma instância do protótipo `Pessoa` chamada `prototipoPessoa`, podemos cloná-la para criar novas instâncias, como `pessoa1` e `pessoa2`. A clonagem permite que as propriedades do protótipo sejam copiadas para as instâncias clonadas, e então cada instância pode ser personalizada individualmente sem afetar o protótipo ou outras instâncias.

Dessa forma, o padrão Prototype permite a criação eficiente de novos objetos através da clonagem de um objeto protótipo, economizando recursos computacionais e fornecendo flexibilidade para personalizar as instâncias conforme necessário.