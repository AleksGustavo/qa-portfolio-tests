# Portfólio de QA — Testes de Software

Repositório independente para planejar, executar e documentar testes manuais, testes de API e automação em aplicações reais.

## Projeto 01 — Petable

- **Repositório da aplicação:** https://github.com/AleksGustavo/Petable
- **Branch de referência (checkout local):** `feat/producao-operacao`
- **Commit de referência inicial (abreviado):** `62bec58`
- **Ambiente:** Windows PowerShell, Docker Engine 29.7.2, Docker Compose 5.4.0
- **Situação atual:** diagnóstico de infraestrutura em andamento; testes funcionais ainda não iniciados.

### Documentos

- [Diário de execução / LAB-001 e LAB-002](docs/01-diagnostico-docker.md)
- [Modelo de caso de teste](templates/modelo-caso-de-teste.md)
- [Modelo de relatório de defeito](templates/modelo-bug.md)
- [Plano dos 10 casos](docs/02-plano-de-testes.md)

## Método de trabalho

1. Preparar ambiente isolado e identificar o commit alvo.
2. Definir pré-condições, passos e resultado esperado antes da execução.
3. Executar, registrar resultado real e evidências sem expor segredos.
4. Classificar como **Aprovado**, **Reprovado**, **Bloqueado** ou **Não executado**.
5. Abrir defeitos reproduzíveis e executar retestes após correção.

> Os registros abaixo representam observações do ambiente, não comprovação de qualidade da aplicação. Não publicar arquivos `.env`, tokens, senhas, dados reais de clientes ou logs com credenciais.
