# Formulário de Atendimento — formulario-de-atendimento.html

## Visão geral

Formulário de anamnese nutricional com **7 etapas** e barra de progresso visual. Os dados são salvos automaticamente no `sessionStorage` para que o paciente não perca o preenchimento ao navegar.

Ao finalizar, os dados são enviados por e-mail via **Web3Forms API** para `nutri.paolaribeiro@gmail.com`. Se o envio falhar, há um fallback para WhatsApp.

**API Key Web3Forms:** `f0e26518-6581-4c96-8416-e34265b35c02`

---

## Cabeçalho do formulário

- Logo + botão de voltar para `index.html`
- Barra de progresso (porcentagem visual)
- Título da etapa atual: "Formulário · Etapa X de 7"

---

## Etapa 1 — Identificação

| Campo              | Tipo              | Observação                                      |
|--------------------|-------------------|-------------------------------------------------|
| Nome completo      | Texto             |                                                 |
| Data de nascimento | Data              | Calcula a idade automaticamente                 |
| Sexo biológico     | Radio             | Feminino / Masculino                            |
| Cidade             | Texto             |                                                 |
| Estado             | Texto             |                                                 |
| WhatsApp           | Telefone          | Máscara: (00) 00000-0000                        |
| E-mail             | E-mail            |                                                 |
| Como nos encontrou | Select            | Instagram, Indicação, Google, etc.              |
| Quem indicou?      | Texto (condicional) | Aparece só se selecionou "Indicação"          |

---

## Etapa 2 — Seu corpo e sua saúde

| Campo                    | Tipo              | Observação                                  |
|--------------------------|-------------------|---------------------------------------------|
| Peso (kg)                | Número            | Formatado automaticamente                   |
| Altura (cm)              | Número            | Formatado automaticamente                   |
| IMC                      | Calculado         | Exibido automaticamente com indicador visual|
| Circunferência abdominal | Número (cm)       |                                             |
| Condições de saúde       | Checkboxes        | SOP, Hipertensão, Diabetes, Tireoide, etc.  |
| Outras condições         | Texto             | Aparece se "Outra" marcada                  |
| Medicamentos             | Sim/Não + texto   |                                             |
| Alergias alimentares     | Sim/Não + lista   | Checkboxes + campo "Outros"                 |
| Exames recentes          | Textarea          |                                             |

---

## Etapa 3 — Seu objetivo

Seleção visual em grade:

- **Emagrecimento** → campos adicionais: dietas anteriores? prazo (evento)? peso desejado?
- **Hipertrofia** → nível de treino, modalidade, suplementação atual?
- **Performance** → tipo de esporte, frequência de treino, competição?
- **Nutrição Clínica** → foco clínico, objetivos secundários?

Os campos condicionais aparecem/desaparecem com base na seleção.

---

## Etapa 4 — Sua rotina

| Campo                 | Tipo           |
|-----------------------|----------------|
| Profissão             | Texto          |
| Tipo de trabalho      | Radio (3 níveis: sedentário, ativo, muito ativo) |
| Horas de sono         | Número         |
| Qualidade do sono     | Select (Ruim, Regular, Bom, Excelente) |
| Pratica atividade?    | Sim/Não        |
| Se sim: frequência, duração, turno | Condicionais |
| Consumo de álcool     | Select         |
| Fumante               | Sim/Não        |
| Nível de estresse     | Escala 1–10    |

---

## Etapa 5 — Sua alimentação

| Campo                        | Tipo     |
|------------------------------|----------|
| Número de refeições/dia      | Número   |
| Pula refeições?              | Sim/Não + quais |
| Descrição do café da manhã   | Textarea |
| Descrição do lanche da manhã | Textarea |
| Descrição do almoço          | Textarea |
| Descrição do lanche da tarde | Textarea |
| Descrição do jantar          | Textarea |
| Descrição da ceia            | Textarea |
| Come fora? (frequência)      | Select   |
| Ingestão de água/dia         | Número   |
| Consumo de refrigerante      | Select   |
| Mudanças alimentares desejadas | Textarea |

---

## Etapa 6 — Histórico

| Campo                          | Tipo           |
|--------------------------------|----------------|
| Já consultou nutricionista?    | Sim/Não        |
| Se sim: há quanto tempo, o que funcionou, por que parou | Condicionais |
| Restrições alimentares         | Checkboxes (vegetariano, vegano, kosher, etc.) |
| Se restrito: quais alimentos evitar | Textarea (condicional) |
| Relação com comida             | Grade visual (Fácil, Neutra, Difícil, Compulsiva) |
| Compulsão alimentar?           | Sim/Não + observações |
| Observações adicionais         | Textarea       |

---

## Etapa 7 — Finalização

| Campo                             | Tipo           |
|-----------------------------------|----------------|
| Formato preferido                 | Radio (Online, Presencial, Híbrido) |
| Tipo de atendimento               | Radio (Individual, Casal, Familiar) |
| Prazo esperado para resultados    | Select         |
| Data/evento motivador             | Data           |
| Aceite dos Termos de Privacidade  | Checkbox obrigatório |
| Botão de envio                    | Submit com spinner de carregamento |

---

## Funcionalidades técnicas do formulário

| Funcionalidade          | Implementação                                        |
|-------------------------|------------------------------------------------------|
| Persistência de dados   | `sessionStorage` — salvo a cada input               |
| Validação em tempo real | Mensagens de erro campo a campo ao tentar avançar   |
| Campos condicionais     | `show/hide` via JavaScript baseado em seleções      |
| Cálculo de idade        | Calculado do campo data de nascimento               |
| Cálculo de IMC          | `peso / (altura/100)²` — exibido com indicador      |
| Formatação de inputs    | Telefone, peso, altura formatados no `input` event  |
| Barra de progresso      | Porcentagem = `(etapa atual / 7) * 100`             |
| Envio de dados          | `fetch POST` → Web3Forms → e-mail para Paola        |
| Fallback de envio       | Link WhatsApp se o envio por e-mail falhar          |
| Tela de sucesso         | Exibida após envio confirmado                       |

---

## Fluxo de navegação do formulário

```
Etapa 1 → Etapa 2 → Etapa 3 → Etapa 4 → Etapa 5 → Etapa 6 → Etapa 7 → Tela de Sucesso
   ↑___________↑___________↑___________↑___________↑___________↑
                          (botão "Voltar" disponível em cada etapa)
```
