# Auditoria — Site Paola Ribeiro Nutricionista
**Data:** 21/06/2026 · **Escopo:** index.html, blog.html, formulario-de-atendimento.html, robots.txt, sitemap.xml
**Método:** leitura direta do código-fonte (não apenas o print), checklist Web Interface Guidelines (Vercel) e framework de SEO técnico/on-page.

---

## Resumo executivo

O site está bem construído na superfície — paleta consistente, tipografia com hierarquia clara, HTML semântico, boa parte da acessibilidade básica resolvida. O problema não é "feio", é que tem **furos que destroem confiança e indexação antes mesmo de chegar no design**: número de pacientes contraditório dentro da própria página, seção de vídeo vazia em produção, blog com 6 artigos fantasmas, imagem de social share quebrada, e uma resolução do CFN que entra em vigor em ~1 mês e pode tornar ilegal o jeito como os depoimentos estão escritos hoje.

Prioridade de ataque, nessa ordem:
1. Corrigir as inconsistências e seções falsas (credibilidade) — custo zero, impacto alto.
2. Resolver o risco regulatório dos depoimentos antes de 24/07/2026.
3. Resolver o que está quebrando indexação/compartilhamento (og:image, sitemap).
4. Só depois, otimizar performance e SEO de conteúdo (blog).

---

## Parte 1 — Design, UX e Conversão

### Críticos (resolvem ou destroem confiança/conversão)

**1. Números contraditórios na mesma página.**
Hero diz "500+ Pacientes" (`index.html:2184`). A seção de contador, três rolagens abaixo, diz "200+ Pacientes atendidas" (`index.html:2347`). Qualquer visitante que rola a página rápido percebe. Em um site de saúde, isso lê como "número inventado", o que mina justamente o que devia vender: confiança técnica. Escolha um número real e use em todo lugar.

**2. Seção "Paola em 60 segundos" está vazia em produção.**
`index.html:2872-2876` — o embed do Instagram depende de `data-instagram-url="INSTAGRAM_URL"`, um placeholder que nunca foi preenchido. Isso é uma seção morta ocupando espaço e tempo de carregamento sem mostrar nada. Ou populam com um Reel real, ou removem a seção até ter conteúdo.

**3. Depoimentos com números específicos de resultado — risco regulatório iminente, não só estético.**
"Perdi 12kg em 5 meses" (`:2694`), "ganhei 4kg de massa em 3 meses" (`:2745`), "Perdi 8kg" (`:2845`) — atribuídos a pacientes nomeadas com idade e cidade. A **Resolução CFN nº 856/2026** (publicada em 25/04/2026) amplia a proibição de divulgar "antes e depois", incluindo dados de composição corporal e resultados de acompanhamento nutricional — **mesmo com autorização do paciente**. Entra em vigor 90 dias após publicação, ou seja, **por volta de 24/07/2026**, daqui a um mês. Esses depoimentos, como estão escritos, ficam fora da norma a partir dessa data. Reescrever para foco em experiência/processo ("o acompanhamento me ajudou a entender minha relação com a comida"), sem números de peso, fotos de corpo ou exames. Vale conversar com o CRN-3 dela ou um advogado antes de publicar qualquer coisa nova nesse formato.

**4. Texto dourado (label-tag) ilegível — falha de contraste em todas as seções.**
O pequeno texto em maiúsculas acima de cada título de seção ("Resultados reais", "Sobre mim", "Dúvidas" etc., classe `.label-tag`) usa `--accent: #C9A84C` sobre fundo claro. Calculei o contraste real: **2.15:1** contra o creme de fundo e **2.29:1** contra branco — bem abaixo do mínimo de acessibilidade (4.5:1 para texto pequeno). Não é só "acessibilidade chata", é legibilidade real para qualquer pessoa em tela de sol ou com visão reduzida — e essa faixa de texto aparece em praticamente toda seção do site. Escurecer o dourado ou usar `--primary-dark` nesses rótulos.

**5. Confirme se o WhatsApp é o número real.**
`+55 16 99999-0000` está hardcoded em todos os CTAs (hero, banner, footer, drawer, JSON-LD) — repetido umas 8+ vezes no código. O padrão "99999-0000" é exatamente o tipo de número de exemplo/placeholder. Se por acaso esse não for o número real, **todo botão principal do site leva a lugar nenhum** — não tem erro mais caro que esse. Confirme, e idealmente centralize numa única constante JS em vez de repetir a string em 3 arquivos (hoje, se o número mudar, é find-and-replace manual em tudo).

### Importantes (não travam venda, mas custam conversão)

- **Foto da seção "Sobre mim" (escritório) pesa 2MB** e está sem otimização real (mais abaixo, no SEO/performance).
- **Prova social é só texto.** Sem foto real de paciente (mesmo que genérica/com permissão), sem link para Google Reviews/Doctoralia, sem contador de seguidores do Instagram. Hoje quem decide entre nutricionistas compara reviews do Google antes de entrar em contato — e o site não direciona pra lá em nenhum momento.
- **Zero menção a valor/investimento.** Entendo que é estratégia comum não publicar preço, mas isso empurra a pessoa pro WhatsApp só para descobrir o valor — e ela pode preferir abandonar do que perguntar. Pelo menos uma faixa de preço ("a partir de R$X") reduz o atrito de quem está só pesquisando.
- **O formulário de anamnese tem 7 etapas e dezenas de campos** (peso, exames, relação com comida, etc.) — ótimo para o atendimento, mas é fricção alta se for pedido *antes* de qualquer contato humano. Verifique se ele é enviado só depois de a consulta já estar agendada/paga, ou se é a primeira coisa que a pessoa vê — se for a segunda, é provável que esteja perdendo lead ali.
- **Botão "fechar" ausente dentro do menu mobile aberto** — só existe o hamburger que vira X (`index.html:2055-2062`), sem ação dedicada visível dentro do drawer. Funciona, mas não é o padrão esperado pelo usuário.
- **Animações sem `prefers-reduced-motion`.** Todo o efeito de entrada (`fadeUp`, `IntersectionObserver`) ignora quem configurou redução de movimento no sistema — afeta pessoas com sensibilidade vestibular.
- `transition: all 350ms` nos cards de especialidade (`index.html:824`) — funciona, mas é prática desencorajada (lista as propriedades específicas em vez de `all`).

### O que já está bem feito (vale reconhecer)

Hierarquia de heading correta (um único `<h1>`, `<h2>`/`<h3>` em ordem — não é raridade ver isso errado). Alt text bem aplicado e imagens decorativas corretamente marcadas com `alt=""` + `aria-hidden`. Imagem do hero em WebP com preload e `fetchpriority="high"` — feito do jeito certo. FAQ visível casa exatamente com o schema FAQPage. Formulário de contato rápido usa `type="email"`, `type="tel"` e `autocomplete` corretos.

---

## Parte 2 — SEO

### Crítico (afeta indexação ou compartilhamento agora)

**1. `og:image` e `twitter:image` apontam para um arquivo que não existe.**
`index.html:39,50,73` referenciam `https://www.nutripaolaribeiro.com.br/og-image.jpg` — esse arquivo não está em `/assets` nem em lugar nenhum do projeto. Resultado: **toda vez que alguém compartilha o link no WhatsApp, Instagram ou Facebook, o preview vem quebrado ou sem imagem.** Para um negócio que vive de indicação boca a boca via WhatsApp, esse é provavelmente o bug de maior custo real no projeto. Crie o arquivo `og-image.jpg` (1200x630px) e coloque na raiz, ou aponte para uma imagem que já existe.

**2. Sitemap referencia URLs que não existem como arquivo.**
`sitemap.xml` lista `/formulario-de-atendimento` e `/blog` (sem `.html`), mas os arquivos reais são `formulario-de-atendimento.html` e `blog.html`. Não encontrei nenhum `_redirects`, `netlify.toml`, `vercel.json` ou `.htaccess` no projeto que faça o rewrite de URL limpa. Sem isso, dependendo de onde for hospedado, **o Google pode indexar URLs do próprio sitemap que retornam 404.** Padronize: ou ajusta o sitemap para `.html`, ou configura rewrite na hospedagem — não os dois meio-feitos.

**3. O blog não tem nenhum artigo — são 6 cards decorativos.**
Todos os 6 "posts" em `blog.html` (`href="#"`, linhas 293-365) levam a lugar nenhum. O sitemap declara `/blog` com prioridade 0.8 e `changefreq: weekly`, prometendo ao Google um conteúdo que não existe. Isso é uma página de conteúdo raso (thin content) por definição — e cards de "Ler artigo" que não vão a lugar nenhum também são uma péssima experiência para quem clica.

### Alto impacto (performance / Core Web Vitals)

**4. A foto "Sobre mim/escritório" pesa 2MB e carrega como prioridade alta.**
`./assets/nutrioffice.png` tem 2.0MB (contra 96-272KB das outras fotos do site). Em `index.html:2195-2206` ela carrega com `loading="eager"`, `decoding="sync"` e `fetchpriority="high"` — ou seja, é tratada como a imagem mais importante da primeira tela (LCP) e é a mais pesada do projeto. Pior: a tag `<source srcset="./assets/nutrioffice.png" type="image/webp">` está declarando tipo WebP para um arquivo que é PNG — não existe um `nutrioffice.webp` real. Converter essa imagem para WebP (deve cair para ~150-250KB) é a melhoria de performance de maior retorno isolado no projeto.

**5. Tailwind CDN carregado nas 3 páginas sem necessidade real.**
`<script src="https://cdn.tailwindcss.com"></script>` está em `index.html`, `blog.html` e `formulario-de-atendimento.html`. Contei as classes usadas no `<body>`: **zero são utilitários Tailwind** — o site é 100% CSS customizado (1838 linhas de `<style>` só no index). O script da CDN do Tailwind gera o CSS em tempo real no navegador e a própria documentação do Tailwind avisa que ele **não deve ser usado em produção**. Aqui ele está sendo carregado de graça, sem uso. Remover.

**6. CSS duplicado e 100% inline em cada página — zero cache entre navegações.**
Cada uma das 3 páginas tem seu próprio bloco `<style>` gigante (1838 linhas no index, ~230 no blog, ~800+ no formulário), repetindo as mesmas variáveis e boa parte das mesmas regras. Como não existe um arquivo `.css` externo, **toda vez que alguém navega de uma página para outra, o navegador baixa e reprocessa o CSS do zero** — não há cache de stylesheet entre páginas. Extrair para um `styles.css` compartilhado resolve isso e ainda reduz duplicação de manutenção.

### Médio (on-page e dados estruturados)

**7. Title com 82 caracteres** (`index.html:6-9`) — o recomendado é 50-60. O Google deve truncar no resultado de busca. Sugestão mais direta: *"Nutricionista em Ribeirão Preto | Paola Ribeiro — CRN-3"* (ajustar para caber a palavra-chave principal antes do corte).

**8. Meta description com 190 caracteres** — ideal é 150-160. Não é grave, mas está sendo cortada na maioria das exibições.

**9. Schema.org incompleto para SEO local.** O `MedicalBusiness` em `index.html:64-104` não tem `streetAddress` nem `postalCode` (só cidade/UF/país) — isso é o que ajuda o Google a posicionar no mapa/local pack. Também falta `AggregateRating`/`Review` (cuidado: só implementar com avaliações reais, schema de review falso viola as políticas do Google) e um schema de `Service` para cada um dos 3 pilares (emagrecimento, performance, clínica), o que ajuda a aparecer em buscas mais específicas.

**10. `formulario-de-atendimento.html` está indexável** (`robots: index, follow`) e listado no sitemap. É uma página de utilidade (formulário vazio), sem valor de busca único — ideal é `noindex, follow` para não diluir a qualidade percebida do site pelo Google.

### Oportunidade perdida (a maior do projeto)

Os 6 títulos já escritos no blog são pauta de SEO muito boa — *"SOP e alimentação: o que ajuda de verdade"*, *"Resistência à insulina: sintomas, causas..."* são buscas reais e específicas que pacientes em potencial fazem no Google, exatamente o público que esse site quer atrair. Hoje isso existe só como título e resumo, sem artigo nenhum atrás. É a maior alavanca de tráfego orgânico do projeto e está zero implementada — antes de qualquer ajuste fino de meta tag, esse é o investimento que move agulha de verdade.

---

## Parte 3 — Risco legal/compliance (fora do pedido, mas relevante)

**Dados de saúde sensíveis coletados sem consentimento LGPD visível.** O formulário de anamnese pergunta sobre diabetes, SOP, hipertensão, uso de medicamentos, compulsão alimentar e relação com a comida — dados classificados como sensíveis pela LGPD (Art. 5º, XIII). Busquei no código por "termos", "privacidade", "LGPD", "consentimento" nas 3 páginas: **não existe checkbox de consentimento nem página de política de privacidade no projeto.** Isso é exposição real, não só boa prática — vale resolver antes de receber mais submissões.

**Depoimentos com resultado numérico, ver item 3 da Parte 1** — Resolução CFN nº 856/2026, em vigor a partir de ~24/07/2026.

---

## Plano de ação priorizado

**Esta semana (custo zero ou quase, impacto alto):**
1. Resolver o número de pacientes contraditório (500+ vs 200+).
2. Remover ou popular a seção do Instagram vazia.
3. Confirmar se o número de WhatsApp é real.
4. Criar e referenciar um `og-image.jpg` real.
5. Adicionar checkbox de consentimento LGPD + página de política de privacidade básica.

**Próximas 2-3 semanas (antes de 24/07/2026):**
6. Reescrever os depoimentos sem números de peso/composição corporal — checar com CRN-3 ou jurídico.
7. Corrigir contraste do `.label-tag` dourado.
8. Alinhar sitemap com as URLs reais (ou configurar rewrite na hospedagem).
9. Converter `nutrioffice.png` para WebP otimizado.
10. Remover o script do Tailwind CDN das 3 páginas.

**Médio prazo:**
11. Extrair CSS para arquivo externo compartilhado.
12. Ajustar title/description para os limites de caracteres recomendados.
13. Completar o schema.org local (endereço completo, Service por especialidade).
14. `noindex` no formulário de atendimento.
15. Escrever (de verdade) os 6 artigos do blog — maior retorno de SEO orgânico do projeto.

---

**Fontes consultadas para o ponto regulatório (Parte 1, item 3 / Parte 3):**
- [Nutricionistas não podem mais postar antes e depois nas redes. Entenda — Metrópoles](https://www.metropoles.com/saude/cfn-codigo-de-etica-nutricionistas)
- Resolução CFN nº 856/2026 (texto oficial em sisnormas.cfn.org.br)
