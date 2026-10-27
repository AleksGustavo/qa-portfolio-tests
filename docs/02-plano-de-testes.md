# Plano de testes — Petable

**Sistema sob teste (SUT):** [Petable](https://github.com/AleksGustavo/Petable)  
**Branch de referência:** `feat/producao-operacao`  
**Commit abreviado inicial:** `62bec58`  
**Critério de entrada:** aplicação acessível; ambiente isolado; dados e credenciais de teste autorizados.  
**Critério de saída:** resultado real documentado com evidência e status para cada caso aplicável.

> Casos candidatos: não presumem que todos os módulos ou integrações já estejam disponíveis. Regras e APIs devem ser validadas antes da execução. Testes que envolvam pagamento real devem ser feitos somente em sandbox/mock.

| ID | Caso de teste | Tipo | Prioridade | Situação |
|---|---|---|---|---|
| CT-001 | Login obrigatório na primeira abertura | Funcional | Alta | Não executado |
| CT-002 | Credenciais inválidas | Funcional | Alta | Não executado |
| CT-003 | Permissões de usuário | Segurança/API | Crítica | Não executado |
| CT-004 | Venda com caixa fechado | Funcional | Alta | Não executado |
| CT-005 | Abertura de caixa e saldo inicial | Funcional | Alta | Não executado |
| CT-006 | Venda e conferência financeira | Integração | Crítica | Não executado |
| CT-007 | Cancelamento e retorno ao estoque | Integração | Crítica | Não executado |
| CT-008 | Vendas concorrentes e estoque | Concorrência | Crítica | Não executado |
| CT-009 | Pagamento duplicado / idempotência | Integração | Crítica | Não executado |
| CT-010 | Logout e sessão inválida | Segurança | Alta | Não executado |

**Próxima ação:** concluir LAB-002, obter acesso à aplicação e detalhar/executar CT-001 antes de avançar.
