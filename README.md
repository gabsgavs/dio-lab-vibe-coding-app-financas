# FinBot 🤖 - Aplicativo de Finanças Pessoais Conversacional

Bem-vindo ao repositório do **FinBot**, um aplicativo de controle financeiro operado inteiramente por meio de uma interface conversacional (chat). Este projeto foi desenvolvido utilizando a abordagem de **Vibe Coding** através da plataforma **Lovable** para um curso de Inteligência Artificial, priorizando rigorosamente os princípios de **Design Universal**, **Acessibilidade** e segurança.

---

## 📝 Resumo do Aplicativo

O **FinBot** foi criado para mitigar a fricção e o abandono histórico associados aos aplicativos tradicionais de controle financeiro (tabelas e planilhas complexas). Ele substitui formulários exaustivos por uma experiência de conversação simples, natural e inclusiva.

### Principais Funcionalidades:
* 💬 **Interface Chat-First:** Toda a interação acontece em uma linha do tempo de mensagens amigável e de alto contraste (padrão WCAG AA), reduzindo barreiras cognitivas de uso.
* 🧠 **Processamento de Linguagem Natural Local:** O aplicativo interpreta comandos informais em português, como `"Gastei R$ 35 no almoço hoje"` ou `"Recebi meu salário de R$ 3000"`, extraindo valores e categorizando-os automaticamente.
* 👥 **Mecanismo Inteligente de "Rachar Conta":** Ao digitar comandos como `"Paguei R$ 60 no Uber para dividir com a Mariana"`, o app reconhece o nome do devedor (tratando artigos em português), calcula sua metade (R$ 30) e gera uma pendência automática.
* ✅ **Painel "Quem me Deve" com Baixa Rápida:** Uma aba lateral dedicada lista quem te deve e permite liquidar o valor instantaneamente com o botão `[Marcar como Pago]`, que já atualiza o saldo e gera uma receita de compensação.
* 💳 **Rastreador de Fatura Nubank:** Funcionalidade inovadora para conciliação bancária. O app agrupa os gastos feitos no "crédito" ou "Nubank", organiza-os dentro do ciclo estimado de fechamento da fatura (fecha dia 2, vence dia 10) e exibe o nome amigável do gasto (ex: "Almoço") para o usuário não se perder com as razões sociais confusas do extrato bancário.

---

## 📄 Prompt Final (PRD Técnico)

Para consolidar o projeto de forma eficiente dentro das limitações de crédito do plano gratuito, o escopo foi injetado de forma incremental e finalizado com a especificação técnica abaixo:

```markdown
# ROLE & CONTEXT
You are an expert Full-Stack Engineer and UI/UX Designer. Your task is to complete the FinBot MVP, a secure, accessible, and beautiful Conversational Personal Finance Web Application based on Universal Design principles.

# UI/UX THEME & UNIVERSAL DESIGN CRITERIA
- **Design System:** Clean, modern, high-contrast (WCAG 2.1 AA compliance). Accessible sans-serif font family (Inter/system-ui), minimum body text 16px.
- **Touch Targets:** All interactive elements, buttons, and inputs must have a minimum interactive area of 44x44px.
- **Cognitive Accessibility:** Clean layout spacing, removing complex accounting jargon. Use meaningful icons accompanied by clear text labels.

# APPLICATION STRUCTURE & TABS
Implement a responsive layout with a Dark Sidebar navigation and a Light Workspace split into three active views controlled by state routing ('chat', 'resumo', 'devedores'):

1. **Chat Workspace ('chat'):**
   - Centered instant-messaging feed displaying interaction bubbles (User aligned right in primary green; Bot aligned left).
   - Parser Engine: Extract values and events from natural language text locally (Expenses, Incomes, Splits).
   - *Regex Debtor Rule:* Ignore optional Portuguese articles ("a", "o", "da", "do") after "com" to capture the dynamic name correctly (e.g., "com a Mariana" -> Debtor: Mariana).

2. **Dashboard View ('resumo'):**
   - Grid cards displaying Total Income, Total Expenses, and Net Balance.
   - Horizontal progress bars acting as a distribution chart for spend categories.
   - **Nubank Credit Card Invoice Tracker:** Section displaying transactions where paymentMethod === 'Cartão Nubank', organizing entries into a simulated billing cycle (closes on Day 2, due on Day 10) matching friendly names recorded via chat.

3. **Reconciliation View ('devedores'):**
   - Map through pending debts displaying Debtor's Name, Amount, and Date.
   - Provide a large target action button: `[Marcar como Pago]` which marks the debt as paid, creates an equivalent income entry, and updates state.

```
## [Resultado Final](https://finbot-chat-shell.lovable.app/)

## 💬 Interações com o Lovable
>Iteração 1: Criação da interface visual base (chat shell) responsiva e de alto contraste utilizando os princípios de Design Universal e acessibilidade.

> Iteração 2: Implementação do motor lógico de processamento de texto (parser) para reconhecer e calcular automaticamente gastos comuns e divisões de contas.

> Iteração 3: Ativação das abas laterais para exibição de gráficos de despesas, do rastreador de fatura Nubank e da lista interativa de devedores.

> Iteração 4: Correção cirúrgica na expressão regular (Regex) para extrair corretamente os nomes próprios em português nas mensagens de divisão de gastos.

## 📸 Demonstração das Interações (Prints / Vídeos)

### 1. Interface Principal do Chat (Design Universal)
<img width="1918" height="870" alt="image" src="https://github.com/user-attachments/assets/b3d4e412-b055-46ff-aa74-774985c51415" />

### 2. Abas de Resumo e Controle de Devedores
<img width="947" height="733" alt="image" src="https://github.com/user-attachments/assets/9e5c9e1b-be6b-4ead-9465-0198d3ea29ab" />
<img width="792" height="562" alt="image" src="https://github.com/user-attachments/assets/41dab6a5-15ba-4194-b4f9-87f61dda2d5d" />

---

## 🧠 Reflexão Sobre o Processo (Human-AI Collaboration)

Desenvolver este ecossistema completo utilizando o conceito de *Vibe Coding* sob a restrição severa de poucas iterações diárias gratuitas trouxe aprendizados profundos de Engenharia de Software.

### O que funcionou bem?
* **Desenvolvimento Modular Sprints:** Dividir o desenvolvimento em "Casca Visual" -> "Lógica do Chat" -> "Dashboards" -> "Autenticação" foi crucial. Evitou que a IA misturasse contextos, reduzindo a taxa de erros de compilação a zero nas primeiras fases.
* **Velocidade do UI Engine:** O Lovable interpretou os comandos de Design Universal de forma surpreendente, gerando layouts responsivos e elegantes usando Tailwind CSS sem necessidade de ajustes manuais.

### O que não funcionou como o esperado?
* **O Bug de Artigo Oculto (Regex):** A IA teve dificuldades iniciais em extrair o nome correto do devedor quando frases naturais continham artigos (ex: `"dividir com a Mariana"` salvava o nome do devedor como `"A"`). Isso exigiu uma intervenção técnica humana direta, onde o prompt teve que fornecer o bloco lógico exato de JavaScript/Regex para corrigir a falha.

### O que aprendi sobre conversar com IAs?
1. **Contexto Técnico em Inglês:** Expressar regras de negócio e arquiteturas em inglês gera resultados infinitamente mais limpos, pois a maior parte do código-fonte e documentações que treinaram os modelos está nessa língua. O português deve ser isolado estritamente para os textos de interface (UI).
2. **Especificidade supera Intencionalidade:** Dizer apenas `"faça o app salvar os dados"` abre espaço para alucinações. Dar instruções detalhadas de arrays de estado, persistência em `localStorage` e lógica condicional garante um código limpo e assertivo de primeira.
3. **Gestão de Escopo Restrito:** Desenvolver com limites estritos de iteração nos força a agir como engenheiros melhores, priorizando o valor central da regra de negócio (Core Value) antes de gastar energia com perfumarias visuais.
