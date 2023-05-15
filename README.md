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
