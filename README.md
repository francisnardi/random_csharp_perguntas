<hr>
Pergunta 1: O que são propriedades automáticas em C#?

Resposta: As propriedades automáticas permitem definir de forma concisa os getters e setters de uma propriedade. O compilador gera automaticamente o código para os acessadores. Aqui está um exemplo:

```csharp
public class Pessoa
{
    public string Nome { get; set; }
    public int Idade { get; set; }
}

// Uso da propriedade automática
Pessoa pessoa = new Pessoa();
pessoa.Nome = "João";
pessoa.Idade = 30;
Console.WriteLine($"Nome: {pessoa.Nome}, Idade: {pessoa.Idade}");
```

<hr>
Pergunta 2: O que é o LINQ (Language Integrated Query) em C#?

Resposta: O LINQ é uma tecnologia que permite consultar coleções de objetos usando uma sintaxe semelhante a consultas SQL. Ele fornece recursos poderosos para filtrar, ordenar e projetar dados. Aqui está um exemplo simples de uso do LINQ:

```csharp
List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };
var numerosPares = numeros.Where(n => n % 2 == 0);
foreach (var numero in numerosPares)
{
    Console.WriteLine(numero);
}
```

<hr>
Pergunta 3: O que são métodos de extensão em C#?

Resposta: Os métodos de extensão permitem adicionar novos métodos a tipos existentes sem modificar sua definição original. Eles são úteis para estender funcionalidades de classes existentes ou adicionar métodos de conveniência. Aqui está um exemplo de método de extensão para a classe `string`:

```csharp
public static class StringExtensions
{
    public static bool IsPalindrome(this string input)
    {
        string reversed = new string(input.Reverse().ToArray());
        return input.Equals(reversed, StringComparison.OrdinalIgnoreCase);
    }
}

// Uso do método de extensão
string palavra = "radar";
bool ehPalindromo = palavra.IsPalindrome();
Console.WriteLine($"A palavra '{palavra}' é um palíndromo?
 {ehPalindromo}");
```

<hr>
Pergunta 4: Como usar threads em C# para executar operações assíncronas?

Resposta: Em C#, você pode usar threads ou tarefas assíncronas para executar operações em paralelo. Aqui está um exemplo de uso de threads:

```csharp
using System.Threading;

public class Program
{
    static void Main()
    {
        Thread thread = new Thread(ExecutarOperacao);
        thread.Start();

        // Continuar com outras tarefas enquanto a operação é executada em paralelo

        thread.Join(); // Aguardar a conclusão da thread

        Console.WriteLine("Operação concluída.");
    }

    static void ExecutarOperacao()
    {
        // Código da operação a ser executada
        Console.WriteLine("Executando operação...");
        Thread.Sleep(3000); // Simulando uma operação demorada
    }
}
```

<hr>
Pergunta 5: O que são expressões lambda em C# e como são usadas?

Resposta: Expressões lambda são funções anônimas que podem ser usadas para criar delegates de forma concisa. Elas são frequentemente usadas em conjunto com métodos como `Where`, `Select` e `OrderBy` do LINQ. Aqui está um exemplo:

```csharp
List<int> numeros = new List<int> { 1, 2, 3, 4, 5 };
var numerosPares = numeros.Where(n => n % 2 == 0);
foreach (var numero in numerosPares)
{
    Console.WriteLine(numero);
}
```

Neste exemplo, a expressão lambda `n => n % 2 == 0` é usada para filtrar os números pares da lista.

<hr>
Pergunta 6: O que é o async/await em C# e qual é o seu propósito?

Resposta: O `async` e `await` são palavras-chave usadas para facilitar a programação assíncrona em C#. Eles permitem que você escreva código assíncrono de forma mais simples e sem bloquear a thread principal. Aqui está um exemplo:

```csharp
public async Task<string> ObterDadosAsync()
{
    await Task.Delay(2000); // Simulando uma operação assíncrona
    return "Dados obtidos";
}

public async Task ExemploAsync()
{
    Console.WriteLine("Iniciando operação assíncrona...");
    string dados = await ObterDadosAsync();
    Console.WriteLine(dados);
    Console.WriteLine("Operação assíncrona concluída");
}

// Chamada do método assíncrono
await ExemploAsync();
```

Nesse exemplo, o método `ObterDadosAsync` é chamado de forma assíncrona usando `await`, permitindo que o fluxo de execução continue sem bloquear a thread principal.

<hr>
Pergunta 7: O que são atributos em C# e como eles são usados?

Resposta: Atributos são marcadores que podem ser aplicados a elementos de código, como classes, métodos, propriedades, etc., para adicionar metadados e informações adicionais. Eles são usados para fornecer instruções ao compilador, ao tempo de execução ou a outras ferramentas. Aqui está um exemplo de uso de atributos:

```csharp
[Serializable]
public class Pessoa
{
    [Required]
    public string Nome { get; set; }

    [Range(18, 65)]
    public int Idade { get; set; }
}
```

Nesse exemplo, os atributos `Serializable`, `Required` e `Range` são usados para fornecer informações adicionais sobre a classe `Pessoa` e suas propriedades. Esses atributos podem ser usados por ferramentas de serialização, validação ou outras bibliotecas.

<hr>
Pergunta 8: O que é injeção de dependência (DI) e como ela é implementada em C#?

Resposta: Injeção de dependência é um padrão de projeto em que as dependências de um objeto são fornecidas externamente, em vez de serem criadas internamente pelo objeto. Isso promove o desacoplamento e a modularidade do código. Em C#, a DI é frequentemente implementada usando frameworks como o Microsoft.Extensions.DependencyInjection. Aqui está um exemplo de uso de DI em C#:

```csharp
public interface IServicoEmail
{
    void EnviarEmail(string destinatario, string mensagem);
}

public class ServicoEmail : IServicoEmail
{
    public void EnviarEmail(string destinatario, string mensagem)
    {
        // Implementação real do envio de e-mail
        Console.WriteLine($"Enviando e-mail para: {destinatario}\nMensagem: {mensagem}");
    }
}

public class ClasseDependente
{
    private readonly IServicoEmail _servicoEmail;

    public ClasseDependente(IServicoEmail servicoEmail)
    {
        _servicoEmail = servicoEmail;
    }

    public void EnviarMensagemPorEmail(string destinatario, string mensagem)
    {
        _servicoEmail.EnviarEmail(destinatario, mensagem);
    }
}

// Configuração da DI
var serviceProvider = new ServiceCollection()
    .AddSingleton<IServicoEmail, ServicoEmail>()
    .BuildServiceProvider();

// Resolução da dependência e uso da classe dependente
var classeDependente = serviceProvider.GetService<ClasseDependente>();
classeDependente.EnviarMensagemPorEmail("exemplo@teste.com", "Olá, mundo!");
```

Nesse exemplo, a classe `ClasseDependente` depende de uma implementação da interface `IServicoEmail`. Por meio da DI, a implementação `ServicoEmail` é injetada na classe `ClasseDependente`, permitindo o envio de e-mails.

<hr>
Pergunta 9: O que é o padrão de projeto Singleton e como ele é implementado em C#?

Resposta: Em C#, o Singleton é um padrão de projeto que garante que uma classe tenha apenas uma instância em toda a aplicação e fornece um ponto de acesso global para essa instância. Isso é útil quando você deseja ter uma única instância compartilhada por várias partes do código, como configurações globais, conexões de banco de dados ou logs.

Aqui está um exemplo de implementação do padrão Singleton em C#:

```csharp
public class Singleton
{
    private static Singleton instance;
    private static readonly object lockObject = new object();

    // Construtor privado para evitar a criação direta de instâncias
    private Singleton()
    {
        // Inicialize os membros necessários
    }

    public static Singleton GetInstance()
    {
        // Verifica se a instância já existe
        if (instance == null)
        {
            // Garante que apenas uma thread possa criar a instância
            lock (lockObject)
            {
                // Verifica novamente se a instância ainda é nula,
                // pois outra thread pode ter criado enquanto estava esperando o lock
                if (instance == null)
                {
                    instance = new Singleton();
                }
            }
        }

        return instance;
    }

    // Métodos de instância
    public void DoSomething()
    {
        // Implemente a lógica desejada
    }
}
```

Nesse exemplo, a classe Singleton possui um construtor privado, impedindo a criação direta de instâncias fora da classe. Em vez disso, a instância única é obtida chamando o método estático `GetInstance()`, que implementa a lógica para criar a instância caso ainda não exista. O uso do bloqueio (`lock`) garante que apenas uma thread possa criar a instância em um ambiente multi-threaded.

Para usar a classe Singleton, você pode chamá-la da seguinte maneira:

```csharp
Singleton instance = Singleton.GetInstance();
instance.DoSomething();
```

Ao chamar `GetInstance()`, você obterá a mesma instância da classe Singleton toda vez que for chamada em qualquer parte do código. Isso permite que você compartilhe informações e recursos entre diferentes componentes da aplicação.

<hr>
Pergunta 10: Qual a diferença entre classes abstratas e interfaces? Exemplifique com código.

Resposta: Claro! Vou exemplificar a diferença entre classes abstratas e interfaces em C# com código. Primeiro, vamos começar com uma classe abstrata:

```csharp
public abstract class Animal
{
    public abstract void EmitSound(); // Método abstrato sem implementação

    public void Sleep()
    {
        Console.WriteLine("Animal is sleeping."); // Método com implementação
    }
}

public class Dog : Animal
{
    public override void EmitSound()
    {
        Console.WriteLine("Woof!"); // Implementação do método abstrato
    }
}
```

Neste exemplo, a classe `Animal` é uma classe abstrata que define um método abstrato `EmitSound()` sem fornecer uma implementação. A classe também tem um método concreto `Sleep()` que fornece uma implementação padrão.

A classe `Dog` herda da classe `Animal` e implementa o método abstrato `EmitSound()` definido pela classe base.

Agora, vamos ver um exemplo de interface:

```csharp
public interface IShape
{
    double CalculateArea(); // Método sem implementação
    void Draw();
}

public class Circle : IShape
{
    private double radius;

    public Circle(double radius)
    {
        this.radius = radius;
    }

    public double CalculateArea()
    {
        return Math.PI * radius * radius; // Implementação do método da interface
    }

    public void Draw()
    {
        Console.WriteLine("Drawing a circle."); // Implementação do método da interface
    }
}
```

Neste exemplo, a interface `IShape` define dois métodos, `CalculateArea()` e `Draw()`, mas não fornece implementações. A classe `Circle` implementa a interface `IShape` e fornece implementações para ambos os métodos da interface.

Resumindo, uma classe abstrata pode ter implementações de métodos, enquanto uma interface só pode ter definições de métodos. Uma classe pode herdar apenas de uma classe abstrata, mas pode implementar várias interfaces. As classes abstratas são úteis quando você quer fornecer uma implementação padrão e também exigir que as classes derivadas forneçam sua própria implementação para certos métodos. As interfaces são úteis quando você deseja definir um conjunto de métodos e propriedades que as classes devem implementar, independentemente de sua hierarquia de herança.

<hr>
Pergunta 11: Mostrar implementações de padrões de projetos em C# com uso do SOLID.

Resposta: Vou mostrar exemplos de implementações de alguns padrões de projeto com o uso dos princípios SOLID em C#.

- Padrão de Projeto: Singleton (Creational)

    O padrão Singleton permite que você garanta que uma classe tenha apenas uma instância e fornece um ponto de acesso global para essa instância. Aqui está um exemplo de implementação em C#:

```csharp
public class Singleton
{
    private static Singleton instance;
    private static readonly object lockObject = new object();

    private Singleton()
    {
        // Construtor privado para evitar instanciação direta.
    }

    public static Singleton Instance
    {
        get
        {
            if (instance == null)
            {
                lock (lockObject)
                {
                    if (instance == null)
                    {
                        instance = new Singleton();
                    }
                }
            }
            return instance;
        }
    }

    // Outros membros da classe...
}

```

- Padrão de Projeto: Factory Method (Creational)

    O padrão Factory Method define um método que delega a criação de objetos para as subclasses, permitindo que a classe base defina a interface, mas deixe as subclasses decidirem quais objetos concretos criar. Aqui está um exemplo de implementação em C#:

```csharp
public abstract class Creator
{
    public abstract IProduct FactoryMethod();

    public void SomeOperation()
    {
        // Lógica antes ou depois da criação do produto
        IProduct product = FactoryMethod();
        // Lógica com o produto criado
    }
}

public interface IProduct
{
    // Interface do produto
}

public class ConcreteCreator : Creator
{
    public override IProduct FactoryMethod()
    {
        return new ConcreteProduct();
    }
}

public class ConcreteProduct : IProduct
{
    // Implementação do produto
}
```

- Padrão de Projeto: Strategy (Behavioral)

    O padrão Strategy define uma família de algoritmos encapsulados e os torna intercambiáveis. Isso permite que o algoritmo varie independentemente dos clientes que o utilizam. Aqui está um exemplo de implementação em C#:

```csharp
public interface IStrategy
{
    void Execute();
}

public class ConcreteStrategyA : IStrategy
{
    public void Execute()
    {
        // Lógica específica para a estratégia A
    }
}

public class ConcreteStrategyB : IStrategy
{
    public void Execute()
    {
        // Lógica específica para a estratégia B
    }
}

public class Context
{
    private IStrategy strategy;

    public Context(IStrategy strategy)
    {
        this.strategy = strategy;
    }

    public void ExecuteStrategy()
    {
        strategy.Execute();
    }
}
```

- Padrão de Projeto: Dependency Injection (DI) (Creational)

    O padrão Dependency Injection permite que você injete as dependências de uma classe em vez de criá-las internamente. Isso ajuda a promover a modularidade e a facilitar a substituição de implementações. Aqui está um exemplo de implementação em C# usando o contêiner de injeção de dependência do ASP.NET Core:

```csharp
public interface IService
{
    void DoSomething();
}

public class Service : IService
{
    public void DoSomething()
    {
        // Implementação do serviço
    }
}

public class Client
{
    private readonly IService service;

    public Client(IService service)
    {
        this.service = service;
    }

    public void UseService()
    {
        // Utilização do serviço
        service.DoSomething();
    }
}

// Configuração do contêiner de injeção de dependência (exemplo usando ASP.NET Core)
services.AddScoped<IService, Service>();
services.AddScoped<Client>();
```

- Padrão de Projeto: Decorator (Structural)

    O padrão Decorator permite que você adicione comportamentos adicionais a um objeto dinamicamente, envolvendo-o em um objeto decorador. Isso evita a necessidade de criar subclasses para cada combinação de comportamentos. Aqui está um exemplo de implementação em C#:

```csharp
public interface IComponent
{
    void Operation();
}

public class ConcreteComponent : IComponent
{
    public void Operation()
    {
        // Implementação do componente concreto
    }
}

public abstract class Decorator : IComponent
{
    private readonly IComponent component;

    public Decorator(IComponent component)
    {
        this.component = component;
    }

    public virtual void Operation()
    {
        component.Operation();
    }
}

public class ConcreteDecoratorA : Decorator
{
    public ConcreteDecoratorA(IComponent component) : base(component)
    {
    }

    public override void Operation()
    {
        // Lógica adicional do decorador A
        base.Operation();
    }
}

public class ConcreteDecoratorB : Decorator
{
    public ConcreteDecoratorB(IComponent component) : base(component)
    {
    }

    public override void Operation()
    {
        // Lógica adicional do decorador B
        base.Operation();
    }
}
```

<hr>
Pergunta 12: Qual a importância das interfaces para o C#?

Resposta: As interfaces desempenham um papel fundamental em C# e têm várias importâncias na linguagem. Aqui estão algumas razões pelas quais as interfaces são importantes em C#:

- Abstração e Polimorfismo: As interfaces fornecem um mecanismo para a abstração de comportamentos. Elas permitem definir contratos que as classes devem seguir, especificando os métodos e propriedades que devem ser implementados. Isso permite que você trabalhe com objetos de diferentes classes de forma polimórfica, tratando-os como instâncias da interface comum. Isso promove a flexibilidade e a modularidade do código.

- Separação de Responsabilidades: Ao usar interfaces, você pode separar as responsabilidades em seu código. Uma classe pode implementar várias interfaces, cada uma representando um conjunto específico de comportamentos. Isso permite que você agrupe funcionalidades relacionadas e as distribua em várias classes, mantendo um código mais organizado e coeso.

- Contratos e Contratos Implícitos: As interfaces definem contratos entre as classes e o código que as utiliza. Esses contratos especificam quais comportamentos são esperados de uma classe que implementa uma determinada interface. Isso facilita a comunicação e a colaboração entre diferentes partes do código, pois todas as classes que implementam uma interface têm a garantia de fornecer a funcionalidade especificada pela interface.

- Facilita a Testabilidade: O uso de interfaces facilita a criação de testes unitários e a realização de testes de isolamento. Ao utilizar interfaces, você pode criar implementações de teste que simulam o comportamento esperado das classes que implementam as interfaces. Isso permite que você teste cada componente do sistema de forma independente, substituindo as implementações reais por implementações de teste.

- Acoplamento Fraco: O uso de interfaces promove um acoplamento fraco entre os componentes do código. Uma classe que depende de uma interface não está vinculada a uma implementação específica, mas sim ao contrato definido pela interface. Isso facilita a substituição de implementações, tornando o código mais flexível e extensível.

- Em resumo, as interfaces são importantes em C# porque fornecem uma forma de definir contratos, promovem a abstração e o polimorfismo, separam responsabilidades, facilitam a testabilidade e permitem um acoplamento fraco entre os componentes do código. Elas desempenham um papel crucial na construção de um código modular, flexível e de fácil manutenção.