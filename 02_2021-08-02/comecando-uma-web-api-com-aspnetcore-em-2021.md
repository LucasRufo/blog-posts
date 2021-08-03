---
date: 02-08-2021
---

![API](.\images\01_api.jpg)

# Começando uma API com .NET Core em 2021

Sou entusiasta de algumas tecnologias da Microsoft e o ASP .NET Core é uma delas, atualmente você pode criar diversas aplicações para a Web utilizando o framework, desde APIs a UIs com Blazor. Já trabalho com ASP .NET há cerca de 2 anos e digo com certeza, **esse é o melhor momento para aprender .NET**, a Microsoft vem fazendo um trabalho incrível com as novas versões do framework e sinto que ele está indo para um caminho bem favorável para a comunidade e para nós, desenvolvedores.

Caso queiram entender um pouco das motivações por trás do uso do .NET atualmente, tem um ótimo post do [André Baltieri](https://www.youtube.com/channel/UCgnACLvM9O5lfm9ZBh_d3cg) explicando porque aprender .NET ainda em 2021: [Link do post](https://balta.io/blog/microsoft-net-5-motivos-para-aprender-ainda-em-2021).

Mostrando um pouco da minha opinião, curto muito trabalhar com o ambiente .NET por conta do C#, a linguagem é muito boa, expressiva e está evoluindo muito com as novas versões. Outro ponto que acho importante, é que a comunidade é bem ativa, isso é bom pois geralmente conseguimos achar bastante conteúdo para aprender sobre e conseguimos achar resoluções de problemas que outros desenvolvedores já passaram utilzando a linguagem.

Nesse post que mostrar e explicar a estrutura base de uma API na versão 5.0 do ASP .NET Core.

## Instalação

O primeiro passo é fazer a instalação do SDK do .NET na versão atual, que é a 5.0, ele pode ser feito utilizando [esse link](https://dotnet.microsoft.com/download/dotnet?WT.mc_id=dotnet-35129-website).

Após a instalação verifique se tudo ocorreu corretamente abrindo um terminal de sua preferência e digitando o comando:

```bash
dotnet --version
```

Deve aparecer a versão 5.0 do framework:

![Print do Terminal com o comando dotnet --version](.\images\03_dotnet-version.png)

Agora antes de partir para a criação da API de fato, caso ainda não tenha um editor de texto, esse é o momento de baixar um, para esse post utilizarei o [Visual Studio Code](https://code.visualstudio.com/).

## Iniciando

Agora precisamos criar uma pasta para armazenar o código fonte do nosso projeto. Geralmente para guardar meus projetos, tenho uma pasta chamada "source" na raiz do disco, sinto que fica mais simples depois para navegar nas pastas e a responsabilidade de manter os projetos fica apenas para essa pasta.

Dentro da pasta desejada, execute o comando abaixo para criar sua primeira Web API:

```bash
dotnet new webapi -n PrimeiraAPI
```

1. `dotnet new` chama a .NET CLI e indica que queremos criar um novo projeto
2. `webapi` indica qual template queremos utilizar para o projeto. [Lista com todos os templates](https://docs.microsoft.com/pt-br/dotnet/core/tools/dotnet-new)
3. `-n` ou `--name` indica qual o nome do nosso projeto

Após a criação do projeto podemos utilizar o comando `code .` no terminal, para abrirmos o projeto no Visual Studio Code.

É bem provável que apareça um prompt do Visual Studio Code pedindo para adicionar alguns arquivos de build e debug no projeto, devemos sempre adicioná-los.

Essa deve ser sua visualização no Explorer do Visual Studio Code:

<p align="center">
  <img src=".\images\04_estrutura-basica.png" alt="Print do file explorer do Visual Studio Code" />
</p>

- `.vscode` é uma pasta gerada pelo próprio editor com alguns arquivos para fazermos *debug* da nossa aplicação e configurações para a CLI.
- `bin` e `obj` são pastas que contém os arquivos compilados do nosso projeto.
- `Controllers`, como o nome já diz, é a pasta que mantém nossas Controllers. Contém uma controller chamada `WeatherForecastController.cs` que foi gerada junto com o template, podemos deletar esse arquivo por agora.
- `Properties` é a pasta que contem o `launchSettings.json`, arquivo de configuração de como nossa aplicação deve inicializar
- `appsettings.json` e `appsettings.Development.json` são os nossos arquivos de configuração, que também podem ser criados por ambiente, como por exemplo: `appsettings.Production.json`.
- `PrimeiraAPI.csproj` é um arquivo de configuração do projeto .NET, ele contém a versão *target* do framework, descrição e versão de bibliotecas externas. Pode ter configurações adicionais.
- `Program.cs` principal arquivo de inicialização do projeto. Contém a chamada que inicia nossa aplicação.
- `Startup.cs` arquivo de configuração da API, então é nele que configuramos middlewares e serviços que nossa API irá utilizar.
- `WeatherForecast.cs` arquivo de exemplo gerado pelo template da criação do projeto, podemos deletar esse arquivo por agora.

## As classes Program e Startup

<p align="center">
  <img src=".\images\05_programcs.png" alt="Print da classe Program.cs" />
</p>

A classe Program é resposável por definir a inicialização da nossa aplicação e algumas configurações iniciais, ela por padrão vem configurada como a imagem acima. O método `Main()` é o metódo chamado assim que nossa aplicação começa a rodar com o comando `dotnet run`.

O método `CreateDefaultBuilder()` já faz algumas configurações relacionadas ao ambiente da nossa aplicação:

- Carrega todas as variáveis de ambiente que estão nos arquivos `appsettings.json` ou que estão nas variáveis de ambiente da máquina.
- Adiciona provedores de log.
- Define que a raíz do nosso conteúdo é o caminho retornado pelo método `GetCurrentDirectory`.

O método `ConfigureWebHostDefaults()` também realiza algumas configurações, mas essas, relacionadas ao Host Web da aplicação:

- Defini o Kestrel como servidor Web padrão. Para quem quiser saber mais sobre o Kestrel, recomendo a [própria documentação da Microsoft](https://docs.microsoft.com/pt-br/aspnet/core/fundamentals/servers/kestrel?view=aspnetcore-5.0).
- Adicionar alguns middlewares padrões de aplicações Web.
- Adicionar integração com o IIS.

Uma coisa que podemos notar, é que no corpo do método `ConfigureWebHostDefaults()`, temos a chamada `webBuilder.UseStartup<Startup>()`, é aqui que definimos que a classe Startup será utilizada para configuração dos middlewares e serviços, como citei mais acima no artigo.

<p align="center">
  <img src=".\images\06_startupcs.png" alt="Print da classe Startup.cs" />
</p>

Essa é a classe Startup, responsável pela configuração da nossa API, ela já vem com bastante coisa configurada por padrão para a gente. Um exemplo disso é o [Swagger](https://swagger.io/), que a partir do .NET 5.0, já vem habilitado nas APIs.

Utilizamos o método `ConfigureServices()` para configurar serviços que nossa API irá utilizar como dependência, um exemplo de serviço que pode ser utilizado por sua API, é o Contexto do banco de dados do [Entity Framework Core](https://docs.microsoft.com/en-us/ef/core/). Ele deve ser configurado através desse método e ficará disponível para ser usado em qualquer lugar da sua aplicação.

Exemplo de chamada adicionando um contexto na nossa aplicação.

```c#
services.AddDbContext<SeuDBContext>(options => options.UseSqlServer(Configuration.GetConnectionString("KeyDaSuaConnectionString")));
```

Já o método `Configure()` serve para a configuração dos Middlewares. Um Middleware é um componente que será adicionado o pipeline HTTP da nossa aplicação, ele vai executar alguma lógica com a Request ou a Response e vai chamar o próximo middleware para continuar o pipeline. A [documentação da Microsoft](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-5.0) tem ótimos exemplos sobre os middlewares, desde como usar a como criar seu próprio middleware personalizado.

Entender cada um dos middlewares disponíveis não é uma tarefa fácil e geralmente sinto que é melhor ir "aprendendo sob demanda", então quando precisar de um middleware novo, é interessante sim ler sua documentação e tentar entender o comportamento interno dele.

## Rodando a aplicação

Após entender os componentes da nossa aplicação, podemos rodar ela. Para rodar sua API, precisamos estar no terminal e precisamos estar na pasta que contém o arquivo `.csproj`. Caso esteja no Visual Studio Code, aperte `Ctrl + '` para abrir um terminal integrado já no diretório da API.

Execute o comando abaixo para entrar na pasta da API, onde temos o arquivo `.csproj`:

```bash
cd PrimeiraAPI
```

Após entrar na pasta da API, execute o comando abaixo para rodar a aplicação:

```bash
dotnet run
```

Após a CLI do .NET compilar e subir nosso projeto, abra o navegador na URL https://localhost:5001/swagger para ver a página inicial do Swagger.

<p align="center">
  <img src=".\images\07_swagger.png" alt="Print do navegador no Swagger" />
</p>

Não temos nada definido no Swagger, pois apagamos os arquivos de exemplo que já vem no template da API, então o comportamento esperado é esse mesmo. Para os próximos passos, sugiro que tente implementar um controller sozinho e veja ele funcionando no Swagger, com algumas chamadas simples de GET e POST.

## Conclusão

Caso tenha alguma sugestão ou encontre algum problema, sinta-se à vontade em me chamar no [Twitter](https://twitter.com/lu_rufo).

## Referências

[Própria documentação da Microsoft](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/?view=aspnetcore-5.0&tabs=windows)
