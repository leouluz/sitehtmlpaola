# SEO e Infraestrutura

## Arquivos de SEO

### robots.txt
- Permite indexação por todos os crawlers (`User-agent: *` / `Allow: /`)
- Referência ao `sitemap.xml`

### sitemap.xml
- Duas URLs mapeadas:
  - `/` (index.html) — prioridade alta
  - `/formulario-de-atendimento.html` — prioridade secundária

## Meta tags (index.html)

| Tag                  | Valor configurado                                     |
|----------------------|-------------------------------------------------------|
| `description`        | Descrição dos serviços de nutrição                    |
| `keywords`           | Nutricionista Ribeirão Preto, nutrição esportiva, etc.|
| `author`             | Paola Fernanda Ribeiro                                |
| `canonical`          | URL canônica do site                                  |
| `robots`             | `index, follow`                                       |
| Open Graph (`og:*`)  | Preview para redes sociais (título, descrição, imagem)|
| Twitter Card         | Metadados para compartilhamento no Twitter/X          |

## Schema.org (JSON-LD)

Implementado com tipo `MedicalBusiness`, incluindo:
- Nome, endereço, telefone, e-mail
- Credenciais profissionais
- Serviços oferecidos
- Área de atendimento

## Performance

| Técnica                   | Implementação                                |
|---------------------------|----------------------------------------------|
| Preload da imagem hero    | `<link rel="preload">` para `nutripaola.jpg` |
| Lazy loading de imagens   | `loading="lazy"` em imagens secundárias      |
| Decodificação assíncrona  | `decoding="async"` nas imagens               |
| Event listeners passivos  | `{ passive: true }` nos listeners de scroll  |
| Fontes via CDN            | Google Fonts com preconnect                  |

## Acessibilidade

- HTML semântico (`<header>`, `<main>`, `<footer>`, `<section>`, `<nav>`, `<article>`)
- ARIA labels e `role` em elementos interativos
- Hierarquia correta de headings (h1 → h2 → h3)
- Labels associados aos inputs do formulário
- Mensagens de erro acessíveis nos campos
- Suporte a navegação por teclado (Escape fecha menus)
- Alt text em todas as imagens
- Estados de foco visíveis nos elementos interativos

## Integração de e-mail — Web3Forms

- **Endpoint:** `https://api.web3forms.com/submit`
- **Método:** `POST`
- **API Key:** `f0e26518-6581-4c96-8416-e34265b35c02`
- **Limite plano gratuito:** 250 envios/mês
- **Destino:** `paola@paolaribeironutricionista.com.br`
- Usado tanto no formulário de contato simples (index.html) quanto no formulário de anamnese completo

## Deploy

O site é **100% estático** — não requer servidor, banco de dados ou build tools. Pode ser hospedado em:
- Netlify, Vercel, GitHub Pages (gratuitos)
- Qualquer hospedagem compartilhada com suporte a HTML estático
- Basta fazer upload da pasta inteira
