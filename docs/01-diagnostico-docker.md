# Diário de QA — LAB-001 e LAB-002: diagnóstico Docker

**Projeto avaliado:** [Petable](https://github.com/AleksGustavo/Petable)  
**Branch informada pelo Git:** `feat/producao-operacao`  
**Commit abreviado informado pelo Git:** `62bec58`  
**Ambiente:** Windows / PowerShell  
**Data de execução:** 27/10/2026 (data do registro; confirmar se alguma saída foi coletada em outra data)  
**Responsável:** [preencher]  
**Status geral:** Diagnóstico parcial — sem teste funcional da aplicação

## LAB-001 — Verificação de ferramentas e infraestrutura

**Objetivo:** confirmar disponibilidade do Docker e identificar o estado dos serviços.

| Verificação | Comando | Resultado observado | Situação |
|---|---|---|---|
| Cliente Docker | `docker --version` | Docker 29.7.2, build a7dcaa6 | Verificado |
| Docker Compose | `docker compose version` | v5.4.0 | Verificado |
| Docker Engine | `docker info --format '{{.ServerVersion}}'` | 29.7.2 | Verificado |
| Diretório local | `Get-Location` | `C:\Users\Aleksander\Projetos\Mobile - Flutter\PetConnect-Web` | Verificado |
| Arquivos Compose | `Get-ChildItem -Name *compose*.yml,*compose*.yaml,Dockerfile* -ErrorAction SilentlyContinue` | `compose.prod.yaml`, `compose.yaml` | Verificado |
| Origem Git | `git remote -v` | `https://github.com/AleksGustavo/Petable.git` | Verificado |
| Branch | `git branch --show-current` | `feat/producao-operacao` | Verificado |
| Commit abreviado | `git rev-parse --short HEAD` | `62bec58` | Verificado |
| Containers ativos (primeira consulta) | `docker ps ...` | `petable-hml-mysql-1` (healthy), `petable-hml-mongo-1` (healthy), `petable-hml-mailpit-1` (healthy) | Verificado naquele momento |
| Serviços do Compose da pasta | `docker compose ps` | Nenhum serviço listado | A investigar (projeto Compose diferente) |

**Observações:** a saúde dos containers não demonstra que o frontend e o backend estejam íntegros. A listagem é uma fotografia de um momento específico.

## LAB-002 — Identificação do projeto e erros de consulta

**Objetivo:** localizar o projeto Compose de homologação, seus serviços e as condições para inspecioná-lo.

| Comando | Resultado observado | Interpretação/ação |
|---|---|---|
| `docker compose ls -a` | `petable-hml` running(5); `petconnect-web` exited(5); `petconnect-api` exited(1) | Projetos distintos identificados; o status `running(5)` deve ser conferido com inspeção direta. |
| `docker compose -f compose.yaml config --services` | `mongo`, `mysql`, `mailpit`, `api`, `web` | Cinco serviços definidos no arquivo local. |
| `docker inspect petable-hml-mysql-1 --format '{{ index .Config.Labels "com.docker.compose.project" }}'` | `template parsing error ... function "com" not defined` | Erro de interpretação de aspas no PowerShell; não caracteriza falha do serviço. |
| `docker compose -p petable-hml -f C:\wt-petable\compose.yaml ps` | Não executou a consulta: variáveis `MYSQL_PASSWORD`, `MYSQL_ROOT_PASSWORD`, `JWT_SECRET` ausentes durante interpolação | Possível diferença entre diretório de trabalho/arquivo `.env`; não inferir que os containers estejam sem essas variáveis. |

**Mensagem observada (resumo, sem segredos):** `required variable JWT_SECRET is missing a value` e `required variable MYSQL_PASSWORD / MYSQL_ROOT_PASSWORD is missing a value`.

**Próxima verificação (não executada neste relatório):**

```powershell
docker ps -a --filter "label=com.docker.compose.project=petable-hml" --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"
```

**Resultado obtido:** [preencher após executar]  
**Evidência (arquivo/imagem/link):** [preencher]  
**Diagnóstico final:** [preencher]  
**Status LAB-002:** Em investigação

## Lições aprendidas

- `docker ps` consulta containers no Engine; `docker compose ps` depende do projeto/configuração selecionados.
- O `compose.yaml` pode exigir variáveis de ambiente mesmo para comandos de inspeção.
- Falha de diagnóstico/ambiente não deve ser automaticamente registrada como defeito do Petable.
- Resultados esperados, observados e hipóteses devem ser registrados separadamente.

## Registro de revisão

| Data | Alteração | Responsável |
|---|---|---|
| 2026-10-27 | Documentação inicial das saídas compartilhadas | [preencher] |
