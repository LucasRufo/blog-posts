---
date: 12-08-2021
---

![MDX Logo](.\images\01_markdown.png)

# Migrei o contéudo do blog para MDX

No meu [primeiro post desse blog](https://lucasrufo.com/blog/porque-comecei-um-blog-e-qual-stack-usei), contei um pouco da experiência e das tecnologias que utilizei para montá-lo, mas agora tomei a decisão de migrar o conteúdo dele do Ghost CMS para arquivos MDX que ficam dentro do projeto. Mas por que iniciei o projeto com o Ghost CMS e não direto com o MDX? É simples, quando pensei em montar o blog, senti que usar o CMS seria a melhor opção e que arcar com os custos dele seriam tranquilos, mas percebi que o serviço como um todo não estava valendo os 11 doláres mensais.

Bom, antes de continuar, acho bom oferecer uma pequena introdução sobre o que é MDX e porque vários blogs atuais utilizam ele. O [MDX](https://mdxjs.com/) é um formato que oferece todos os benefícios do Markdown e ainda permite que possamos importar componentes JSX dentro dos arquivos. Isso abre várias possibilidades para o conteúdo do arquivo, como por exemplo animações e gráficos personalizados. Para quem quiser uma introdução com um pouco mais de prática, recomendo [esse vídeo](https://www.youtube.com/watch?v=d2sQiI5NFAM&list=PLV5CVI1eNcJgCrPH_e6d57KRUTiDZgs0u) do [Kent C. Dodds](https://kentcdodds.com/) em que ele mostra o MDX funcionando em um projeto.

## Como realizei a migração?

Eu já sabia que era possível utilizar o MDX com Next JS pois a equipe por trás do framework conta com alguns repositórios de exemplo, que inclusive já oferecem soluções bem sólidas para projetos pequenos como um blog. Então quebrei o problema em alguns pequenos passos que poderiam me guiar melhor na jornada de migração:

1. Eu deveria criar uma pasta na raíz do meu projeto para armazenar os arquivos dos posts.

2. Deveria ler os arquivos dessa pasta.

3. Deveria ler alguns metadados dos posts, como título, descrição, data de publicação e coisas do tipo.

4. Deveria conseguir converter o contéudo do arquivo MDX para HTML.

Seguindo esses 4 passos, eu conseguiria exibir os posts utilizando os metadados que eles me ofereciam e conseguiria montar o contéudo da página do post em sí. Então comecei criando a pasta com o nome `posts` e já coloquei alguns arquivos MDX lá para usar como teste. Ler os arquivos da pasta também não era um problema já que no Next JS podemos acessar módulos do Node no método `GetStatisProps()`, então apenas utilizei funções nativas do módulo **fs** e um pacote chamado [Glob](https://www.npmjs.com/package/glob) para montar os caminhos que eu teria que acessar.

O passo 3 era uma possibilidade que eu tinha visto em outros repositórios de blogs, que era utilizar uma sintaxe no início do arquivo MDX que armazenaria metadados como pares de chave-valor e depois ler esse bloco de metadados utilizando alguma biblioteca, a sintaxe dentro do MDX ficaria algo assim:

```mdx
---
title: "Porque comecei um blog e qual stack usei"
publishedAt: "2021-07-26"
description: "Entenda minha motivação na criação deste blog e quais tecnologias tornaram ele possível."
slug: "porque-comecei-um-blog-e-qual-stack-usei"
image: "/blog/01/01_next-logo.jpeg"
---
```

A biblioteca que utilizei para recuperar esses dados foi a [gray-matter](https://github.com/jonschlinkert/gray-matter), ela é bem simples de ser utilizada, apenas passamos o contéudo lido do arquivo para a função `matter()` e recuperamos a propriedade `data`.

```ts
const data = matter(source).data as MetaPost
```

O passo final seria conseguir converter o contéudo MDX para HTML e para isso eu tive que fazer uma boa pesquisa para entender quais opções eu poderia utilizar. [Esse post](https://www.joshwcomeau.com/blog/how-i-built-my-blog/) do [Josh Comeau](https://www.joshwcomeau.com) conta como ele montou o blog dele utilizando Next JS e MDX e ele mostra algumas opções de bibliotecas que podem ser utilizadas para fazer essa conversão para HTML. No final optei por utilizar a biblioteca [mdx-bundler](https://github.com/kentcdodds/mdx-bundler) que também é do [Kent C. Dodds](https://kentcdodds.com/), a chamada da função que converte o conteúdo fica assim:

```ts
const { code } = await bundleMDX(source)
```

Com essa variável `code`, apenas precisaria passar ela para dentro da função `getMDXComponent()`, também da biblioteca **mdx-bundler**, utilizando o *hook* `useMemo()`, para não precisarmos recriar esse componente em todo *render*, como a [própria documentação diz](https://github.com/kentcdodds/mdx-bundler#usage).

```tsx
const Component = React.useMemo(() => getMDXComponent(code), [code])

return (
  <>
    <Component />
  </>
)
```

E pronto, eu já teria o conteúdo do MDX sendo renderizado em tela. Toda a estrutura que existia em volta da estilização do conteúdo do posts ficou da mesma maneira, utilizando o Tailwind CSS, apenas precisei mudar a fonte do contéudo. Demorei cerca de umas 3 horas pra conseguir finalizar tudo e manter do jeito que eu queria, mas no fim foi um processo bem interessante.

O código fonte está todo disponível no Github [nesse reposítório](https://github.com/LucasRufo/blog).



