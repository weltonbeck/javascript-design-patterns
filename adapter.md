[voltar](/README.md)

# Adapter

O padrão Adapter é um padrão de projeto estrutural que permite que objetos com interfaces incompatíveis trabalhem juntos. Ele converte a interface de uma classe em outra interface esperada pelos clientes, permitindo que classes com diferentes interfaces colaborem de maneira transparente.

O Adapter é útil quando precisamos utilizar uma classe existente que não possui a interface necessária para ser usada por um cliente específico. Em vez de modificar a classe existente, criamos um adaptador que atua como uma camada intermediária entre o cliente e a classe existente, convertendo as chamadas do cliente na interface adequada para a classe existente.

Aqui está um exemplo em JavaScript que ilustra o padrão Adapter:

```JS
// Classe existente com interface incompatível
class Banco {
  sacar(valor) {
    console.log(`Realizando saque de R$${valor} do banco.`);
  }
}

// Interface esperada pelo cliente
class Conta {
  constructor() {
    this.banco = new Banco();
  }

  realizarSaque(valor) {
    this.banco.sacar(valor);
  }
}

// Adapter que adapta a interface da classe existente
class ContaAdapter {
  constructor() {
    this.conta = new Conta();
  }

  sacarDolar(valor) {
    const valorConvertido = valor * 5; // Simulação de conversão para dólar (cotação 1:5)
    this.conta.realizarSaque(valorConvertido);
  }
}

// Uso do Adapter
const contaAdapter = new ContaAdapter();
contaAdapter.sacarDolar(100); // Saída: Realizando saque de R$500 do banco.

```

Nesse exemplo, temos a classe `Banco` que representa uma classe existente com uma interface incompatível com a interface desejada pelo cliente. Ela possui um método `sacar` que realiza saques em reais.

A classe `Conta` representa a interface esperada pelo cliente. Ela encapsula uma instância da classe `Banco` e possui o método `realizarSaque`, que delega a chamada ao método `sacar` da classe `Banco`.

O `ContaAdapter` é o adaptador que permite que o cliente faça saques em dólar em vez de reais. Ele encapsula uma instância da classe `Conta` e possui o método `sacarDolar`, que recebe um valor em dólar, realiza a conversão para reais e chama o método `realizarSaque` da classe `Conta`.

Ao utilizar o `ContaAdapter`, o cliente pode chamar o método `sacarDolar` passando um valor em dólar. O adaptador se encarrega de realizar a conversão para reais e delegar a chamada corretamente para o método `realizarSaque` da classe `Conta`, que, por sua vez, chama o método `sacar` da classe `Banco`.

Dessa forma, o padrão Adapter permite que o cliente utilize a interface desejada, adaptando-a para a interface da classe existente, sem modificar diretamente a classe existente. Isso promove a reutilização de código e facilita a integração de componentes com interfaces incompatíveis.
