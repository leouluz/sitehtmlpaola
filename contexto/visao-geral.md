# Visão Geral do Projeto — Paola Ribeiro Nutricionista

## O que é este projeto

Site profissional estático para a nutricionista **Paola Fernanda Ribeiro** (CRN-3 76261), com sede em Ribeirão Preto/SP. Atende presencialmente em Ribeirão Preto e online para todo o Brasil.

## Arquivos principais

```
sitehtmlpaola/
├── index.html                      → Página principal do site
├── formulario-de-atendimento.html  → Formulário de anamnese (7 etapas)
├── robots.txt                      → Configuração para motores de busca
├── sitemap.xml                     → Mapa do site (SEO)
└── assets/
    ├── logo.png                    → Logo principal
    ├── nutripaola.jpg              → Foto da nutricionista (hero)
    ├── nutripaolawhite.jpg         → Foto alternativa (branco)
    ├── png/                        → Ícones em PNG (estrelas, músculos, chapéu, etc.)
    └── svg/                        → Ícones SVG decorativos (frutas, alimentos, etc.)
```

## Tecnologias utilizadas

- **HTML5 / CSS3 / JavaScript puro** — sem frameworks ou build tools
- **Tailwind CSS** — via CDN, para utilitários de estilo
- **Google Fonts** — Cormorant Garamond, Montserrat, Lato
- **Web3Forms API** — envio de e-mails via formulário (plano gratuito: 250/mês)
- **IntersectionObserver API** — animações ao rolar a página
- **SessionStorage** — persistência de dados no formulário multi-etapas

## Paleta de cores (CSS variables)

| Variável            | Valor      | Uso                     |
|---------------------|------------|-------------------------|
| `--primary`         | `#1B5E3B`  | Verde escuro principal  |
| `--primary-light`   | `#2E7D52`  | Verde médio             |
| `--primary-dark`    | `#0F3D24`  | Verde muito escuro      |
| `--accent`          | `#C9A84C`  | Dourado (destaque)      |
| `--bg`              | `#FAF8F4`  | Creme claro (fundo)     |

## Informações de contato configuradas no site

- **WhatsApp:** +55 (16) 99999-0000
- **E-mail:** paola@paolaribeironutricionista.com.br
- **Instagram:** @nutri.paolaribeiro
- **Horário:** Seg–Sex 8h–18h · Sáb 8h–12h
