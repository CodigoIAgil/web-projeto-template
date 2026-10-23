# web-projeto-template

Modelo para projetos web (HTML, CSS e JS) com o processo de desenvolvimento seguro já pronto:
lint, formatação, varredura de segredos, CI obrigatório e deploy no GitHub Pages.

## Criar um projeto novo a partir deste modelo

```bash
cd /c/dev
gh repo create CodigoIAgil/NOME-DO-PROJETO --public --template CodigoIAgil/web-projeto-template --clone
cd NOME-DO-PROJETO
npm ci
pre-commit install
bash scripts/proteger-repo.sh CodigoIAgil/NOME-DO-PROJETO
```

Depois, troque o `name` no `package.json` e o título no `README.md` e no `index.html`.

O site só vai para o GitHub Pages a partir do primeiro merge na `main`. No commit que cria o repositório,
o deploy é pulado de propósito, porque o Pages ainda não existe nesse momento.

## Cache de CSS e JS

Chame seus arquivos de CSS e JS com `?v=dev` no fim, em todas as páginas:

```html
<link rel="stylesheet" href="css/style.css?v=dev" />
<script src="js/app.js?v=dev" defer></script>
```

No deploy, `dev` vira o commit publicado (ex.: `?v=3c5c766`), e o navegador baixa a versão nova
a cada publicação, em vez de usar a antiga do cache. Se sobrar algum `?v=dev`, o deploy falha.

Para ícones SVG no HTML, coloque `width` e `height` no próprio `<svg>`: assim eles não ficam
gigantes mesmo se o CSS falhar.

## Comandos

| Comando             | O que faz                                                      |
| ------------------- | -------------------------------------------------------------- |
| `npm run check`     | roda o lint de HTML e CSS e confere a formatação (igual ao CI) |
| `npm run format`    | formata todos os arquivos com o Prettier                       |
| `pre-commit run -a` | roda todos os hooks locais em todos os arquivos                |

## O processo

O passo a passo do dia a dia está em [docs/PROCESSO.md](docs/PROCESSO.md).
