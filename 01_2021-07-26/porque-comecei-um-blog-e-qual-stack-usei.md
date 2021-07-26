---
date: 26-07-2021
---

![Logo NextJS](.\images\01_next-logo.jpeg)

# Porque comecei um blog e qual stack usei

Sempre tive a ideia de ter um espaço na internet onde eu poderia compartilhar meus aprendizados e experiências no mundo de tecnologia. Criar esse blog, está me possibilitando ter esse espaço, onde posso manter todo o meu processo de aprendizado de novas ferramentas e anotações sobre o que estou pensando ou contruindo no momento.

Já trabalho com desenvolvimento Web a quase dois anos e quando olho pra trás, vejo o quanto o tempo passou rápido e o quanto eu evolui como programador. Ter um blog me possibilita documentar o meu processo de evolução com a programação, tanto para eu mesmo poder revisar com o tempo, quanto para outras pessoas poderem ler e se identificarem com problemas que passei ou experiências que tive.

Minha maior inspiração para a criação do blog foi o [Scott Hanselman](https://www.hanselman.com/), as palestras dele são muito inspiradoras e sempre fico feliz de poder assisti-las, mesmo que seja apenas pelo Youtube. Inclusive, caso queiram assistir uma das palestras dele, [essa](https://www.youtube.com/watch?v=V4NJo2Mfvrc) é a minha favorita.

## Quais tecnologias utilizei?

Na escolha das tecnologias da criação do Blog eu já estava bem decidido do que gostaria de usar. A decisão deveria ser feita pensando em alguns fatores como:

- **Velocidade do blog**: Eu gostaria de publicar artigos de forma rápida e queria que o blog em sí fosse bem rápido.
- **Oportunidade de aprendizado**: Eu gostaria de usar uma tecnologia que eu ainda não tinha utilizado, para poder aprender no processo.

Então basicamente utilizei Next JS com Typescript e TailwindCSS para a contrução do blog. Já para manter os posts, utilizei o Ghost CMS.

### Next JS

O [Next JS](https://nextjs.org/) é um framework contruido em cima do React e oferece suporte a geração de sites estatícos, o que é ótimo para um blog, pois o conteúdo não muda com tanta frequência. A documentação é ótima e a experiência de desenvolvimento também foi excelente.

Eu nunca tinha utilizado React, apenas tinha usado Angular para construir minhas SPAs e não sabia se ir direto para o Next JS era uma boa ideia, mas assistindo alguns videos vi que o processo parecia bem simples e de fato foi.

Optei também por utilizar o Typescript no projeto, pois já tinha familiariadade com ele por conta do meu conhecimento em Angular, que por padrão, utiliza o Typescript. Me sinto muito mais seguro sabendo que caso eu cometa algum erro em tempo de desenvolvimento, minha IDE vai acusar o erro e eu poderei corrigir antes.

### Tailwind CSS

Pra quem não conhece, o [Tailwind CSS](https://tailwindcss.com/) é um framework CSS denominado `utility-first`, então ele basicamente provê várias classes já prontas com nomes bem intuitivos, para você poder escrever pouco ou quase nenhum CSS na mão.

Eu já tinha utilizado o Tailwind CSS em um outro projeto e no início foi complicado utilizar tantas classes para estilizar os elementos, mas com o tempo as coisas vão melhorando e você não precisa ficar olhando tanto a documentação, pois você já vai lembrando os nomes das classes. Utilizar o plugin que oferece Intellisense no VS Code também facilita o desenvolvimento.

Uma das coisas que eu ainda não tinha utilizado com o Tailwind, era o plugin `@tailwindcss/typography` que oferece as classes que estilizam os posts do blog. Os posts do blog vem direto do CMS, então eu teria certo trabalho para estilizar tudo e manter o texto de forma legível e agradável, mas o plugin resolveu grande parte do problema.

Conheci o plugin através do próprio canal do Youtube do Tailwind CSS, o [Tailwind Labs](https://www.youtube.com/channel/UCOe-8z68tgw9ioqVvYM4ddQ). Recomendo que deem uma olhada, o conteúdo é muito bom.

### Ghost CMS

Quando comecei a pesquisar as formas de montar um blog com Next JS, vi que eu tinha algumas possibilidades:

1. Criar arquivos Markdown direto no repositório e usar alguma bliblioteca para intepretar esses arquivos e ajustar eles na página do post.
2. Utilizar MDX, que é basicamente Markdown mas permite utilizar o JSX do React dentro dos arquivos e também utilizar os arquivos dentro do próprio repositório.
3. Utilizar um CMS para poder guardar os meus posts e no projeto eu apenas buscá-los de uma API.

As duas primeiras opções, me dariam mais controle sobre o conteúdo do blog, principalmente se eu optasse por utilizar MDX, mas também adicionariam uma camada a mais de complexidade para lidar. Então acabei optando por utilizar um CMS mesmo e ir com a opção mais simples.

Eu nunca tinha utilizado um CMS na vida, então fui pesquisar sobre para ver qual me daria uma boa experiência e me daria suporte a Markdown. Encontrei o [Ghost CMS](https://ghost.org/) logo de cara e criei uma conta lá para ver como funcionava.

O processo de criar e manter os posts, é bem simples e isso me chamou muita atenção na hora de escolher. Ele também tem um ótimo editor, que suporta Markdown e outras inúmeras funcionalidades. Ele possui uma ótima documentação e tem guias de como integrar projetos Next JS com a Content API disponibilizada por eles para podermos buscar o conteúdo do blog, o que também facilitou bastante do processo de criação do blog.

Eu também tinha dado uma olhada no [Graph CMS](https://graphcms.com/) e a experiência também tinha sido muito boa, mas acabei optando por utilizar o Ghost mesmo.

### E onde fazer o deploy?

Bom, para meus últimos projetos front-end, tenho utilizado a [Vercel](https://vercel.com/) (que inclusive, é a criadora do Next JS). A experiência de deploy vem sendo muito boa e simples, toda a integração com o Github torna tudo muito fácil, então desenvolvo na minha branch `dev` e quando quero subir algo, apenas abro um Pull Request para a `main` e faço o merge, a própria Vercel cuida de toda a parte complicada do deploy.

É bom também mencionar que a plataforma já possui todo o suporte a otimização de algumas features do Next JS, como as Serverless Functions. Então caso seu projeto também seja em Next JS, recomendo fortemente que utilize a Vercel.

### Conclusão

Desejo que os posts do blog possam ajudar alguém em sua jornada no mundo de desenvolvimento também. Caso possua algum feedback sobre o post ou sobre o blog em sí, por favor, sinta se a vontade para abrir uma Issue ou um PR no [repositório do Github](https://github.com/LucasRufo/blog).

Caso tenha alguma pergunta, podemos utilizar o meu [Twitter](https://twitter.com/lu_rufo)!

