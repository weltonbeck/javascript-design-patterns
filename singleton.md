[voltar](/README.md)

# Singleton

O padrão Singleton é um padrão de projeto criacional que tem como objetivo garantir que uma classe possua apenas uma única instância e fornecer um ponto global de acesso a essa instância.

O Singleton é útil em situações em que precisamos ter exatamente uma instância de uma classe durante toda a execução do programa, como uma conexão de banco de dados, um gerenciador de log ou um cache de dados.

Aqui está um exemplo em JavaScript que ilustra o padrão Singleton:

```JS
class AppConfig {
  constructor() {
    // Verifica se já existe uma instância e retorna a mesma
    if (AppConfig.instance) {
      return AppConfig.instance;
    }

    // Caso contrário, cria uma nova instância e a armazena como propriedade estática
    AppConfig.instance = this;

    // Inicialização das propriedades de configuração
    this.apiKey = '';
    this.apiUrl = '';
  }

  setApiKey(apiKey) {
    this.apiKey = apiKey;
  }

  setApiUrl(apiUrl) {
    this.apiUrl = apiUrl;
  }

  getApiKey() {
    return this.apiKey;
  }

  getApiUrl() {
    return this.apiUrl;
  }
}

// Uso do Singleton
const config1 = new AppConfig();
const config2 = new AppConfig();

console.log(config1 === config2); // Saída: true

config1.setApiKey('abc123');
config2.setApiUrl('https://api.example.com');

console.log(config1.getApiKey()); // Saída: abc123
console.log(config2.getApiUrl()); // Saída: https://api.example.com

```

Nesse exemplo, a classe `AppConfig` implementa o padrão Singleton para armazenar informações de configuração do aplicativo. No construtor da classe, verificamos se já existe uma instância e retornamos essa mesma instância em vez de criar uma nova. Caso não exista uma instância, criamos uma nova e a armazenamos como propriedade estática `instance` da classe.

As propriedades `apiKey` e `apiUrl` são utilizadas para armazenar as configurações da chave da API e a URL da API, respectivamente. Os métodos `setApiKey`, `setApiUrl`, `getApiKey` e `getApiUrl` permitem definir e obter os valores das configurações.

Ao criar instâncias do `AppConfig`, como `config1` e `config2`, verificamos se elas são idênticas usando o operador `===`, e o resultado será `true`, pois o Singleton garante que apenas uma instância seja criada.

Em seguida, definimos diferentes configurações nas instâncias `config1` e `config2`. Quando chamamos os métodos `getApiKey` e `getApiUrl`, obtemos os valores corretos das configurações definidas em ambas as instâncias.

Assim, o padrão Singleton nos permite ter apenas uma única instância da classe `AppConfig` para armazenar informações de configuração do aplicativo, garantindo consistência e acesso global a essas informações.
