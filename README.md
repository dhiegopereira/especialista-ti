## Conteúdos: 


</details>
<details>
<summary>1. Banco de dados:</summary>
- Índices
    - Vantagens: 
        - Melhora o desempenho das consultas, pois permite a localização rápida dos registros.
        - Reduz a necessidade de percorrer a tabela inteira em busca de dados específicos.
        - Ajuda a manter a integridade dos dados, evitando duplicações e inconsistências.
    - Desvantagens:
        - Ocupa espaço adicional em disco.
        - Pode levar a um aumento no tempo de inserção, atualização e exclusão de registros.
        - Requer manutenção adequada para garantir a eficiência ao longo do tempo.

    > OBS: Para garantir melhor desempenho na manipulação dos dados, é possível utilizar uma cópia do banco em paralelo ou um banco de cache como o `redis`. Dessa forma, as operações são realizadas e sincronizadas posteriormente com o banco de produção, que possui índices.

- Procedures:
    - Vantagens:
        - Permitem agrupar um conjunto de instruções SQL em uma única chamada.
        - Podem ser reutilizadas em diferentes partes do código.
        - Aumentam a segurança, pois podem ser executadas com privilégios específicos.
    - Desvantagens:
        - Podem tornar o código mais complexo e difícil de manter.
        - Podem causar problemas de desempenho se mal utilizadas.


    > OBS: Apenas as instruções `INSERT`, `UPDATE` e `DELETE` devem ser executadas dentro de procedimentos armazenados.

- Functions:
    - Vantagens:
        - Permitem retornar um valor calculado ou processado a partir de um conjunto de parâmetros.
        - Podem ser utilizadas em expressões SQL.
        - Podem ser reutilizadas em diferentes partes do código.
    - Desvantagens:
        - Podem ter um impacto negativo no desempenho se mal otimizadas.
    - Podem ser limitadas em termos de funcionalidades disponíveis.

    > OBS: Utilize apenas a instrução `SELECT` e mantenha a implementação o mais simples possível.

- Triggers:
    - Vantagens:
        - Permitem automatizar a execução de ações em resposta a eventos específicos no banco de dados.
        - Podem ser utilizados para manter a integridade dos dados.
        - Podem ser utilizados para auditar e registrar alterações nos dados.
    - Desvantagens:
        - Podem tornar o código mais complexo e difícil de depurar.
        - Podem causar problemas de desempenho se mal utilizados.

</details>
<details>
<summary>2. Design Patterns:</summary>

### Singleton
**Definição:** O padrão Singleton garante que uma classe tenha apenas uma instância e fornece um ponto global de acesso a essa instância.

**Quando usar:** Use o Singleton quando precisar de exatamente uma instância de uma classe para controlar o acesso a recursos compartilhados, como um arquivo de log, uma conexão de banco de dados ou uma configuração de aplicação.

**Exemplo de implementação em Java:**
```java
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Construtor privado para evitar instanciamento externo
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    public void showMessage() {
        System.out.println("Hello World!");
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Singleton singleton = Singleton.getInstance();
        singleton.showMessage();
    }
}
```

### Factory
**Definição**: O padrão Factory define uma interface para criar um objeto, mas permite que as subclasses decidam qual classe instanciar. O Factory Method permite que uma classe delegue a responsabilidade de criação de objetos para subclasses.

**Quando usar**: Use o Factory Method quando uma classe não pode antecipar a classe de objetos que deve criar ou quando uma classe quer que suas subclasses especifiquem os objetos que criam.

**Exemplo de implementação em Java:**
```java
// Produto
interface Product {
    void use();
}

// Produto Concreto
class ConcreteProductA implements Product {
    public void use() {
        System.out.println("Using Product A");
    }
}

// Produto Concreto
class ConcreteProductB implements Product {
    public void use() {
        System.out.println("Using Product B");
    }
}

// Fábrica
abstract class Creator {
    public abstract Product factoryMethod();

    public void someOperation() {
        Product product = factoryMethod();
        product.use();
    }
}

// Fábrica Concreta
class ConcreteCreatorA extends Creator {
    public Product factoryMethod() {
        return new ConcreteProductA();
    }
}

// Fábrica Concreta
class ConcreteCreatorB extends Creator {
    public Product factoryMethod() {
        return new ConcreteProductB();
    }
}

// Uso
public class Main {
    public static void main(String[] args) {
        Creator creatorA = new ConcreteCreatorA();
        creatorA.someOperation();

        Creator creatorB = new ConcreteCreatorB();
        creatorB.someOperation();
    }
}
```
</details>
<details>
<summary>3. Arquitetura</summary>

### Arquitetura de software
**Definição:** Domain-Driven Design (DDD) é uma abordagem de design de software que enfatiza a colaboração entre especialistas de domínio e desenvolvedores para criar um modelo de domínio que reflete com precisão os processos e regras de negócios.

**Quando usar:** Use DDD quando estiver desenvolvendo sistemas complexos onde a compreensão e a modelagem do domínio de negócios são cruciais para o sucesso do projeto.

**Exemplos:**
1. Domain-Driven Design (DDD)
2. Microservices Architecture

### Framework de desenvolvimento
**Definição:** Spring Boot é um framework de desenvolvimento Java que facilita a criação de aplicações standalone, de produção, baseadas no Spring Framework, com configuração mínima.

**Quando usar:** Use Spring Boot quando precisar de uma configuração rápida e fácil para criar aplicações Java robustas e escaláveis.

**Exemplos:**
1. Spring Boot (para Java)
2. ASP.NET Core (para .Net)

### Arquitetura de comunicação
**Definição:** RESTful API é um estilo de arquitetura para sistemas distribuídos que utiliza HTTP para comunicação entre clientes e servidores, seguindo os princípios REST (Representational State Transfer).

**Quando usar:** Use RESTful API quando precisar de uma interface de comunicação simples, escalável e baseada em padrões para interagir com serviços web.

**Exemplos:**
1. RESTful API
2. GraphQL

### Padrão de persistência
**Definição:** Object-Relational Mapping (ORM) é uma técnica de programação que permite converter dados entre sistemas incompatíveis usando orientação a objetos. EX ORM refere-se a frameworks específicos que implementam essa técnica.

**Quando usar:** Use ORM quando precisar mapear objetos de uma aplicação para tabelas de um banco de dados relacional, facilitando a manipulação de dados.

**Exemplos:**
1. Hibernate (para Java)
2. Entity Framework (para .NET)

</details>
<details>
<summary>4. Programação concorrente</summary>

### Thread
**Definição:** Uma thread é a menor unidade de processamento que pode ser executada de forma independente por um sistema operacional. Threads são usadas para executar tarefas simultaneamente dentro do mesmo processo.

**Quando usar:** Use threads quando precisar executar múltiplas tarefas simultaneamente dentro de um único processo, como em aplicações que requerem operações de I/O e processamento intensivo ao mesmo tempo.

**Problemas que resolvem:**
- Melhor utilização de recursos do sistema.
- Melhoria na performance de aplicações que realizam múltiplas operações independentes.
- Redução do tempo de resposta em aplicações interativas.

### Sistemas distribuídos
**Definição:** Sistemas distribuídos são sistemas em que componentes localizados em diferentes computadores se comunicam e coordenam suas ações através de uma rede para alcançar um objetivo comum.

**Quando usar:** Use sistemas distribuídos quando precisar de escalabilidade, tolerância a falhas e distribuição de carga em aplicações que requerem processamento em larga escala ou que operam em múltiplas localizações geográficas.

**Problemas que resolvem:**
- Escalabilidade horizontal, permitindo adicionar mais recursos conforme necessário.
- Alta disponibilidade e tolerância a falhas.
- Distribuição de carga e processamento paralelo.

### Serverless
**Definição:** Serverless é um modelo de execução de computação em nuvem onde o provedor de nuvem gerencia automaticamente a infraestrutura necessária para executar o código, permitindo que os desenvolvedores se concentrem apenas na lógica da aplicação.

**Quando usar:** Use serverless quando precisar de uma solução de computação escalável e econômica, onde você paga apenas pelo tempo de execução do código e não precisa se preocupar com a gestão de servidores.

**Problemas que resolvem:**
- Redução de custos operacionais e de infraestrutura.
- Escalabilidade automática baseada na demanda.
- Simplificação do desenvolvimento e implantação de aplicações.

</details>
<details>
<summary>5. DevOps</summary>

### CI/CD
**Definição:** CI/CD (Continuous Integration/Continuous Deployment) é um conjunto de práticas de DevOps que visa automatizar e melhorar o processo de desenvolvimento, integração e entrega de software. CI se refere à integração contínua, onde o código é frequentemente integrado e testado. CD se refere à entrega contínua ou implantação contínua, onde o código é automaticamente implantado em ambientes de produção.

**Quando usar:** Use CI/CD para automatizar o processo de integração e entrega de software, garantindo que o código seja testado e implantado de forma rápida e confiável.

**Problemas que resolvem:**
- Redução do tempo de entrega de novas funcionalidades.
- Detecção precoce de bugs e problemas de integração.
- Melhoria na qualidade do software e na confiabilidade das implantações.

### IaC
**Definição:** Infrastructure as Code (IaC) é a prática de gerenciar e provisionar a infraestrutura de TI através de código, em vez de processos manuais. Isso permite que a infraestrutura seja tratada da mesma forma que o código de aplicação, com versionamento, revisão e automação.

**Quando usar:** Use IaC para automatizar a configuração e o gerenciamento da infraestrutura, garantindo consistência e repetibilidade em diferentes ambientes.

**Problemas que resolvem:**
- Redução de erros de configuração e inconsistências.
- Aumento da velocidade e eficiência na provisão de infraestrutura.
- Facilitação da replicação de ambientes para desenvolvimento, teste e produção.

### Docker e Kubernetes
**Definição:** Docker é uma plataforma de contêinerização que permite empacotar, distribuir e executar aplicações em contêineres leves e portáteis. Kubernetes é um sistema de orquestração de contêineres que automatiza a implantação, escalonamento e gerenciamento de aplicações em contêineres.

**Quando usar:** Use Docker para criar ambientes de aplicação isolados e consistentes. Use Kubernetes para gerenciar e orquestrar esses contêineres em escala, garantindo alta disponibilidade e escalabilidade.

**Problemas que resolvem:**
- Docker:
  - Isolamento de aplicações e dependências.
  - Portabilidade entre diferentes ambientes.
  - Redução de conflitos de ambiente.
- Kubernetes:
  - Automação da implantação e gerenciamento de contêineres.
  - Escalabilidade horizontal de aplicações.
  - Alta disponibilidade e recuperação automática de falhas.

</details>
<details>
<summary>6. Segurança da Informação</summary>

### Criptografia SSL/TLS
**Definição:** SSL (Secure Sockets Layer) e TLS (Transport Layer Security) são protocolos criptográficos que fornecem comunicação segura pela internet. Eles garantem que os dados transmitidos entre o cliente e o servidor sejam criptografados e protegidos contra interceptação e adulteração.

**Quando usar:** Use SSL/TLS para proteger a comunicação entre clientes e servidores, especialmente em transações sensíveis como login, pagamento e transferência de dados pessoais.

**Problemas que resolvem:**
- Proteção contra ataques de interceptação (e.g., Man-in-the-Middle).
- Garantia de integridade e confidencialidade dos dados transmitidos.
- Autenticação de servidores e, opcionalmente, de clientes.

### Autenticação e Autorização JWT
**Definição:** JWT (JSON Web Token) é um padrão aberto para a criação de tokens de acesso que permitem a autenticação e autorização de usuários em aplicações web. Os tokens JWT são compactos, seguros e podem ser transmitidos via URL, parâmetros POST ou em um cabeçalho HTTP.

**Quando usar:** Use JWT para autenticação e autorização em aplicações web e APIs, especialmente quando precisar de um método seguro e eficiente para transmitir informações de identidade entre diferentes partes.

**Problemas que resolvem:**
- Autenticação segura de usuários.
- Autorização baseada em permissões e roles.
- Redução da necessidade de armazenamento de sessões no servidor.

### Firewall e VPN
**Definição:** Um firewall é um sistema de segurança de rede que monitora e controla o tráfego de rede com base em regras de segurança predefinidas. VPN (Virtual Private Network) é uma tecnologia que cria uma conexão segura e criptografada sobre uma rede menos segura, como a internet.

**Quando usar:** Use firewalls para proteger redes internas contra acessos não autorizados e ataques externos. Use VPNs para permitir conexões seguras e privadas entre usuários remotos e a rede corporativa.

**Problemas que resolvem:**
- Firewall:
  - Proteção contra acessos não autorizados e ataques de rede.
  - Controle de tráfego de entrada e saída com base em políticas de segurança.
- VPN:
  - Criação de conexões seguras para usuários remotos.
  - Proteção de dados transmitidos sobre redes públicas.
  - Acesso seguro a recursos internos da empresa.

</details>
<details>
<summary>7. Testes</summary>

### As 3 leis do TDD
**Definição:** As 3 leis do Test-Driven Development (TDD) são princípios que guiam o desenvolvimento orientado a testes. Elas são:
1. **Você não deve escrever código de produção até que tenha escrito um teste de unidade que falhe.**
2. **Você não deve escrever mais de um teste de unidade do que o suficiente para falhar (compilação falha é falha).**
3. **Você não deve escrever mais código de produção do que o suficiente para fazer o teste de unidade atual passar.**

**Quando usar:** Use as 3 leis do TDD para garantir que o desenvolvimento seja guiado por testes, promovendo a criação de código testável e de alta qualidade.

**Problemas que resolvem:**
- Garantia de que o código é testado desde o início.
- Redução de bugs e problemas de integração.
- Melhoria na qualidade e na manutenção do código.

### Uma afirmação por teste
**Definição:** O princípio de "uma afirmação por teste" sugere que cada teste deve verificar apenas uma condição ou comportamento específico do código, mantendo os testes simples e focados.

**Quando usar:** Use uma afirmação por teste para criar testes claros e concisos, facilitando a identificação de falhas e a manutenção dos testes.

**Problemas que resolvem:**
- Facilitação da identificação de falhas específicas.
- Simplificação da manutenção dos testes.
- Melhoria na legibilidade e clareza dos testes.

### Um único conceito por teste
**Definição:** O princípio de "um único conceito por teste" sugere que cada teste deve se concentrar em um único conceito ou unidade de funcionalidade, evitando a verificação de múltiplos comportamentos em um único teste.

**Quando usar:** Use um único conceito por teste para garantir que os testes sejam focados e específicos, facilitando a depuração e a manutenção.

**Problemas que resolvem:**
- Redução da complexidade dos testes.
- Facilitação da depuração e manutenção.
- Melhoria na clareza e na organização dos testes.

### FIRST
**Definição:** FIRST é um acrônimo que descreve as características de bons testes de unidade. Ele significa:
- **Fast (Rápido):** Os testes devem ser rápidos para serem executados frequentemente.
- **Independent (Independentes):** Os testes não devem depender uns dos outros.
- **Repeatable (Repetíveis):** Os testes devem produzir os mesmos resultados em qualquer ambiente.
- **Self-Validating (Auto-Validáveis):** Os testes devem ter uma saída clara de sucesso ou falha.
- **Timely (Oportunos):** Os testes devem ser escritos no momento certo, preferencialmente antes do código de produção.

**Quando usar:** Use o princípio FIRST para garantir que seus testes de unidade sejam eficazes e eficientes, promovendo uma prática de TDD robusta.

**Problemas que resolvem:**
- Garantia de que os testes são rápidos e podem ser executados frequentemente.
- Redução de dependências entre testes.
- Consistência nos resultados dos testes em diferentes ambientes.
- Clareza nos resultados dos testes.
- Escrita de testes no momento apropriado do ciclo de desenvolvimento.

</details>
<details>
<summary>8. POO</summary>

### Encapsulamento
**Definição:** Encapsulamento é o princípio de esconder os detalhes internos de um objeto e expor apenas o que é necessário através de métodos públicos. Isso protege o estado interno do objeto contra modificações não controladas.

**Exemplo de uso:**
```java
public class Pessoa {
    private String nome;
    private int idade;

    public String getNome() {
        return nome;
    }

    public void setNome(String nome) {
        this.nome = nome;
    }

    public int getIdade() {
        return idade;
    }

    public void setIdade(int idade) {
        this.idade = idade;
    }
}

```

### Classe Abstrata e Interfaces
**Definição:** Classes abstratas são classes que não podem ser instanciadas e podem conter métodos abstratos (sem implementação) e métodos concretos. Interfaces são contratos que definem métodos que uma classe deve implementar, mas não fornecem implementação.

**Exemplo de uso:**
```java
// Classe Abstrata
public abstract class Animal {
    public abstract void fazerSom();
}

// Interface
public interface Voar {
    void voar();
}

// Implementação
public class Passaro extends Animal implements Voar {
    @Override
    public void fazerSom() {
        System.out.println("Piu Piu");
    }

    @Override
    public void voar() {
        System.out.println("O pássaro está voando");
    }
}
```

### Polimorfismo
**Definição:** Polimorfismo é a capacidade de um objeto assumir muitas formas. Em POO, isso permite que uma classe pai seja usada para referenciar objetos de classes filhas.

**Exemplo de uso:**
```java
public class Animal {
    public void fazerSom() {
        System.out.println("Som genérico de animal");
    }
}

public class Cachorro extends Animal {
    @Override
    public void fazerSom() {
        System.out.println("Latido");
    }
}

public class Gato extends Animal {
    @Override
    public void fazerSom() {
        System.out.println("Miau");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal meuAnimal = new Cachorro();
        meuAnimal.fazerSom(); // Latido

        meuAnimal = new Gato();
        meuAnimal.fazerSom(); // Miau
    }
}
```

### Composição
**Definição:** Composição é um princípio onde uma classe é composta de uma ou mais instâncias de outras classes, permitindo a criação de objetos complexos a partir de objetos mais simples.

**Exemplo de uso:**
```java
public class Motor {
    public void ligar() {
        System.out.println("Motor ligado");
    }
}

public class Carro {
    private Motor motor;

    public Carro() {
        this.motor = new Motor();
    }

    public void ligarCarro() {
        motor.ligar();
    }
}
```

### Injeção de Dependência
**Definição:** Injeção de dependência é um padrão de design onde as dependências de uma classe são fornecidas externamente, geralmente através de um framework, em vez de serem criadas internamente.

**Exemplo de uso com Spring Boot:**
```java
@Service
public class MeuServico {
    private final MeuRepositorio repositorio;

    @Autowired
    public MeuServico(MeuRepositorio repositorio) {
        this.repositorio = repositorio;
    }

    public void executarServico() {
        repositorio.salvar();
    }
}
```

### Anotações do Framework (Spring Boot)
**Definição:** Anotações são metadados que fornecem informações sobre o código e são usadas pelo framework para configurar e gerenciar componentes.

**Exemplo de uso:**
```java
@RestController
public class MeuControlador {
    @GetMapping("/saudacao")
    public String saudacao() {
        return "Olá, mundo!";
    }
}
```

### Concurrency e Multithreading
**Definição:** Concurrency é a capacidade de um sistema lidar com múltiplas tarefas ao mesmo tempo. Multithreading é a técnica de executar múltiplas threads simultaneamente dentro de um processo.

**Exemplo de uso:**
```java
public class MinhaThread extends Thread {
    @Override
    public void run() {
        System.out.println("Thread em execução");
    }

    public static void main(String[] args) {
        MinhaThread thread = new MinhaThread();
        thread.start();
    }
}
```

### public, static, private e partial
**Definição:**
- public: O membro é acessível de qualquer lugar.
- private: O membro é acessível apenas dentro da classe onde foi declarado.
- static: O membro pertence à classe, não a instâncias individuais.
</details>
