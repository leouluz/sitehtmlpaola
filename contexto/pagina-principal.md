# Página Principal — index.html

## Seções da página (ordem de cima para baixo)

### 1. Navbar (fixa/sticky)
- Logo + "Paola Ribeiro / Nutricionista"
- Links: Especialidades, Depoimentos, Contato
- Botão CTA: "Quero agendar" → leva ao formulário
- Menu hambúrguer mobile (drawer com overlay)
- Efeito de scroll: adiciona blur e borda ao rolar

### 2. Hero Section
- Título: "Nutricionista em Ribeirão Preto — Paola Ribeiro."
- Subtítulo sobre estratégias nutricionais baseadas em ciência
- Badge: "Nutricionista Esportiva & Clínica · CRN-3 76261"
- Dois botões: "Quero agendar" (primário) e "Conhecer melhor" (outline)
- Foto grande de Paola (`nutripaola.jpg`)
- Decorações SVG botânicas (folhas) e sobreposições circulares
- Animações de entrada escalonadas (fade-in)

### 3. Sobre mim
- Foto de Paola no consultório (`nutripaolawhite.jpg`)
- Texto sobre abordagem personalizada
- 3 cards de credenciais:
  - Nutrição Esportiva (Especialização FMRP-USP)
  - Nutrição Clínica (Especialização FMRP-USP)
  - CRN-3 76261 (Registro ativo)

### 4. Especialidades — "Três pilares do meu atendimento"
Três cards de serviço:

**Emagrecimento com estratégia**
- Plano personalizado, reeducação alimentar com comida de verdade
- Acompanhamento entre consultas
- CTA: link para WhatsApp

**Performance e hipertrofia**
- Nutrição esportiva feminina
- Periodização nutricional, suplementação inteligente

**Nutrição Clínica**
- SOP, resistência à insulina, condições específicas de saúde
- Manejo clínico especializado

### 5. Como funciona o atendimento
- Visualização passo a passo do processo
- Fundo escuro (seção de contraste)
- Etapas numeradas: contato inicial → plano personalizado → acompanhamento → resultados

### 6. Depoimentos de pacientes
- Avaliações com estrelas
- Fotos/avatares de pacientes
- Comentários sobre resultados e experiência

### 7. Banner CTA
- Banner chamativo incentivando o agendamento
- Botão de ação em destaque

### 8. Contato
**Formulário com campos:**
- Nome, E-mail, WhatsApp (com máscara automática), Assunto, Mensagem

**Informações de contato exibidas:**
- WhatsApp, E-mail, Instagram

### 9. Footer
- Logo + tagline: "Nutrição baseada em ciência. Resultados reais."
- Links de navegação
- Redes sociais (Instagram e WhatsApp)
- Credenciais: "CRN-3 76261 · Paola Fernanda Ribeiro Nutricionista"
- Copyright: "© 2026 Paola Ribeiro Nutricionista"

### 10. Botão flutuante WhatsApp
- Posição fixa na tela
- Atalho rápido para contato via WhatsApp

## Comportamentos JavaScript (index.html)

| Funcionalidade              | Como funciona                                           |
|-----------------------------|---------------------------------------------------------|
| Menu mobile                 | Toggle de classe + overlay; fecha com Escape           |
| Efeito navbar no scroll     | `scroll` event → adiciona classe com blur/borda        |
| Animações de entrada        | `IntersectionObserver` → adiciona classe `visible`     |
| Máscara de telefone         | Input event → formata como `(00) 00000-0000`           |
| Envio do formulário contato | Fetch POST para Web3Forms API                          |
| Scroll suave                | `scroll-behavior: smooth` + `href="#ancora"`           |
