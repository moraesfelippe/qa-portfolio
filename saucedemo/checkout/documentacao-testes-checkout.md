# 🛡️ Documentação de Testes: Módulo de Checkout
**Projeto:** E-commerce SauceDemo (Prática Profissional)
**Responsável:** Felipe M. - Estudante de ADS
**Metodologia:** Ágil (Scrum/Jira)

---

## 1. Estratégia de Teste
O objetivo é validar a integridade do fluxo de compra, garantindo que o usuário consiga finalizar o pedido com dados válidos e que o sistema bloqueie ações inconsistentes.

* **Ambiente:** Google Chrome 124.0 (Desktop) - Windows 11
* **Ferramentas:** Jira Software, Manual Testing, DevTools
* **Tipo de Teste:** Funcional (Caixa Preta) e Negativo

---

## 2. Casos de Teste (Test Cases)

### CT-001: Compra com Sucesso (Caminho Feliz)
**Objetivo:** Verificar se um usuário logado finaliza a compra com dados válidos.
* **Pré-condição:** Estar logado; Ter pelo menos 1 item no carrinho.
* **Passos:**
    1. Clicar no ícone do Carrinho.
    2. Clicar no botão "Checkout".
    3. Preencher: First Name = Joao, Last Name = Silva, Zip = 12345
    4. Clicar em "Continue".
    5. Clicar em "Finish".
* **Resultado Esperado:** Exibição da mensagem "Thank you for your order!" URL "https://www.saucedemo.com/checkout-complete.html", carrinho zerar, aparecer botao "Back Home".
* **STATUS FINAL:** ✅ PASSOU.
* **Evidência:** [print da tela "Thank you for your order!"]

---

### CT-002: Checkout com Carrinho Vazio (Caminho Negativo)
**Objetivo:** Validar se o sistema impede o checkout sem produtos.
* **Pré-condição:** Estar logado; Carrinho com 0 itens.
* **Passos:**
    1. Clicar no ícone do Carrinho.
    2. Clicar no botão "Checkout".
* **Resultado Esperado:** O sistema deve impedir o avanço para a tela de dados (ex: botão desabilitado ou alerta).
* **STATUS FINAL:** ❌ FALHOU (Gerou o BUG-001).
* **Evidência:** Print anexado no card SCRUM-8 (Jira)

---

### CT-003: Remoção de todos os itens do carrinho
**Objetivo:** Verificar se o carrinho zera corretamente ao remover todos os itens.
* **Pré-condição:** Estar logado; Ter pelo menos 1 item no carrinho.
* **Passos:**
    1. Adicionar 1 produto ao carrinho.
    2. Clicar no ícone do carrinho.
    3. Clicar em "Remove" no produto.
* **Resultado Esperado:** O produto é removido, a lista do carrinho fica vazia e o contador do ícone some.
* **STATUS FINAL:** ✅ PASSOU.
* **Evidência:** [print do carrinho vazio]

---

### CT-004: Persistência do carrinho após logout
**Objetivo:** Verificar o comportamento do carrinho após logout e novo login.
* **Pré-condição:** Estar logado; Ter pelo menos 1 item no carrinho.
* **Passos:**
    1. Adicionar 1 produto ao carrinho.
    2. Clicar no menu hambúrguer.
    3. Clicar em "Logout".
    4. Logar novamente com as mesmas credenciais.
    5. Clicar no ícone do carrinho.
* **Resultado Esperado:** O item adicionado antes do logout ainda está no carrinho.
* **STATUS FINAL:** ✅ PASSOU.
* **Evidência:** [print do carrinho com o item após novo login]

---

### CT-005: Checkout sem First Name
**Objetivo:** Validar se o sistema bloqueia o avanço sem o First Name.
* **Pré-condição:** Estar logado; Ter pelo menos 1 item no carrinho.
* **Passos:**
    1. Clicar no ícone do Carrinho.
    2. Clicar em "Checkout".
    3. Deixar First Name em branco.
    4. Preencher Last Name = Silva, Zip = 12345.
    5. Clicar em "Continue".
* **Resultado Esperado:** Sistema bloqueia o avanço e exibe mensagem de erro indicando campo obrigatório.
* **STATUS FINAL:** ✅ PASSOU.
* **Evidência:** [print da mensagem de erro]

---

### CT-006: Checkout sem Last Name
**Objetivo:** Validar se o sistema bloqueia o avanço sem o Last Name.
* **Pré-condição:** Estar logado; Ter pelo menos 1 item no carrinho.
* **Passos:**
    1. Clicar no ícone do Carrinho.
    2. Clicar em "Checkout".
    3. Preencher First Name = Joao, deixar Last Name em branco, Zip = 12345.
    4. Clicar em "Continue".
* **Resultado Esperado:** Sistema bloqueia o avanço e exibe mensagem de erro indicando campo obrigatório.
* **STATUS FINAL:** ✅ PASSOU.
* **Evidência:** [print da mensagem de erro]

---

### CT-007: Checkout sem Zip
**Objetivo:** Validar se o sistema bloqueia o avanço sem o Zip.
* **Pré-condição:** Estar logado; Ter pelo menos 1 item no carrinho.
* **Passos:**
    1. Clicar no ícone do Carrinho.
    2. Clicar em "Checkout".
    3. Preencher First Name = Joao, Last Name = Silva, deixar Zip em branco.
    4. Clicar em "Continue".
* **Resultado Esperado:** Sistema bloqueia o avanço e exibe mensagem de erro indicando campo obrigatório.
* **STATUS FINAL:** ✅ PASSOU.
* **Evidência:** [print da mensagem de erro]

---

## 3. Relatório de Defeitos (Bug Report)

### BUG-001: Checkout permitido com carrinho vazio
* **ID no Jira:** SCRUM-8
* **Severidade:** Média (Lógica de Negócio)
* **Prioridade:** Alta
* **Descrição:** O sistema permite que o usuário avance para a tela de informações de checkout (`checkout-step-one.html`) mesmo quando o carrinho possui 0 itens.
* **Passos para reproduzir:** 1. Logar > 2. Carrinho Vazio > 3. Clicar em Checkout.
* **Resultado Atual:** O sistema redireciona para a página de dados do cliente.
* **Resultado Esperado:** O botão "Checkout" deve estar desabilitado ou exibir um alerta de "Carrinho Vazio".
* **Observação:** Comportamento confirmado também após remoção manual 
de todos os itens pelo carrinho, não apenas com carrinho nunca preenchido
* **Evidência:** Print anexado no card SCRUM-8 (Jira)

