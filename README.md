# Portfólio Profissional

**Aluno:** Rodrigo Tebaldi
**Curso:** Técnico em Desenvolvimento de Sistemas (Paula Souza, EaD)

## Descrição do portfólio

Página de portfólio pessoal criada para apresentar meu perfil profissional, as tecnologias que estudo e os projetos que desenvolvi ao longo da formação. O site é responsivo (funciona em computador, tablet e celular) e foi construído a partir do projeto feito em aula, com personalização do conteúdo e do visual.

## Link do site publicado

https://rodrigo-siqueira.github.io/portfolio/

Repositório: https://github.com/Rodrigo-Siqueira/portfolio

## Tecnologias utilizadas

- **HTML5**: estrutura da página.
- **CSS3**: ajustes de layout e animações.
- **Bootstrap 5.3.8**: grid, navbar, carousel, cards e botões.
- **Devicon**: ícones das tecnologias.
- **Git e GitHub**: versionamento do código.
- **GitHub Pages**: publicação do site.
- **VS Code**: ambiente de desenvolvimento.

## Como o projeto funciona

O site é uma página única (`index.html`), com o menu fixo no topo levando a cada seção por âncoras:

| Parte | O que faz |
|---|---|
| **Navbar** | Menu fixo no topo (`sticky-top`) com os links Perfil, Trajetória, Projetos e Contato. Em telas pequenas vira um botão que abre e fecha o menu. |
| **Carousel** | Área de destaque com 3 slides, indicadores e botões de avançar e voltar. Cada slide tem título, texto e botão sobre a imagem. |
| **Destaques** | Faixa escura com números do meu projeto principal (3 projetos, 59 testes, PHPStan nível máximo e PSR-4). |
| **Perfil** | Foto, nome, descrição, cards com localização, interesse, formação e objetivo, o bloco "Como eu trabalho" e as tecnologias que uso. |
| **Trajetória** | Linha do tempo da minha evolução: do HTML e CSS ao PHP puro, ao sistema Plataforma Normalize e aos próximos passos (Docker, PostgreSQL e Laravel). |
| **Projetos** | Três cards com imagem, título, etiquetas de tecnologia, descrição e botões para o repositório no GitHub ou para uma janela com mais detalhes. |
| **Contato** | Card central com botões de e-mail e GitHub e a localização. |
| **Rodapé** | Direitos autorais e tecnologias usadas. |

Estrutura de arquivos:

```
portfolio/
├── index.html
├── README.md
├── css/
│   └── style.css
└── imagens/
    ├── slide1.png
    ├── slide2.png
    ├── slide3.png
    ├── p1.png
    ├── p2.png
    ├── p4.png
    └── perfil-foto.jpg
```

## Recurso novo: animação nos cards de projeto

### O que é

Ao passar o mouse sobre um card de projeto, ele **sobe levemente** e ganha uma **sombra mais forte**, com uma transição suave. Isso dá retorno visual ao visitante, mostrando qual projeto está em foco e que o card é clicável. O efeito foi além do que foi feito em aula, que usava apenas a sombra fixa (`shadow-sm`) nos cards.

Também incluí a **rolagem suave** entre as seções ao clicar no menu e nos botões do carousel.

### Como foi implementado

**1. Classe própria no HTML.** Os cards de projeto receberam a classe `hover-lift`, junto com as classes do Bootstrap:

```html
<div class="card hover-lift h-100 shadow-sm border-0 rounded-4 overflow-hidden">
```

**2. Transição no CSS.** A propriedade `transition` faz a mudança acontecer aos poucos, em 0,2 segundo, em vez de instantânea:

```css
.card {
    transition: transform .2s ease, box-shadow .2s ease;
}
```

**3. Efeito no hover.** Quando o mouse está sobre o card, ele é movido 4px para cima com `transform: translateY(-4px)` e a sombra aumenta com `box-shadow`. O `!important` é necessário para prevalecer sobre a classe `shadow-sm` do Bootstrap:

```css
.card.hover-lift:hover {
    transform: translateY(-4px);
    box-shadow: 0 .75rem 1.5rem rgba(0, 0, 0, .12) !important;
}
```

**4. Acessibilidade.** Quem configura o sistema para reduzir animações não vê o movimento:

```css
@media (prefers-reduced-motion: reduce) {
    html { scroll-behavior: auto; }
    .card { transition: none; }
}
```

**5. Rolagem suave.** Com uma linha no CSS, os links do menu deslizam até a seção em vez de pular:

```css
html { scroll-behavior: smooth; }
```

Como a navbar fica fixa no topo, usei `scroll-margin-top: 56px` nas seções para o título não ficar escondido atrás dela.

## Recurso adicional: janelas de detalhes (modal)

Nos projetos Plataforma Normalize e Meu Portal de Entretenimento Digital, o botão **Ver detalhes** abre uma janela sobre a página com mais informações do projeto, sem sair do portfólio.

### Como foi implementado

Usei o componente **Modal** do Bootstrap, que funciona com o script `bootstrap.bundle` já incluído na página, sem JavaScript próprio. O botão aponta para o `id` da janela:

```html
<button type="button" class="btn btn-outline-primary mt-auto"
        data-bs-toggle="modal" data-bs-target="#modalPortal">Ver detalhes</button>
```

E a janela é criada no final do `<body>`, com o mesmo `id`:

```html
<div class="modal fade" id="modalPortal" tabindex="-1" aria-labelledby="tituloPortal" aria-hidden="true">
    <div class="modal-dialog modal-lg modal-dialog-scrollable">
        <div class="modal-content">
            <div class="modal-header">...</div>
            <div class="modal-body">...</div>
            <div class="modal-footer">...</div>
        </div>
    </div>
</div>
```

`modal-dialog-scrollable` permite rolar o conteúdo dentro da janela, e `aria-labelledby` liga a janela ao título para leitores de tela.

## Outras evoluções em relação ao modelo da aula

- Conteúdo personalizado: meus dados, minhas tecnologias (PHP no lugar de Python) e meus projetos reais.
- Texto e botão sobre cada slide do carousel, alinhados à esquerda e com ajuste para celular.
- Etiquetas de tecnologia (badges) nos cards de projeto.
- Nova seção **Trajetória**, com linha do tempo feita em CSS, e faixa de destaques abaixo do carousel.
- Ícone da aba, descrição da página e link "Pular para o conteúdo" para acessibilidade.

## Como executar localmente

Baixe ou clone o repositório e abra o arquivo `index.html` no navegador. É preciso conexão com a internet para carregar o Bootstrap e os ícones, que vêm de CDN.