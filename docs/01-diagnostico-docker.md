## LAB-002 — Verificação dos containers em execução

**Data:** 27/10/2026  
**Projeto:** Petable  
**Ambiente:** Homologação (`petable-hml`)  
**Branch de referência local:** `feat/producao-operacao`  
**Commit de referência local:** `62bec58`  
**Ferramenta:** Docker Engine 29.7.2  

### Objetivo

Identificar os containers em execução, seus estados e portas de acesso, sem modificar o ambiente.

### Procedimento

Executado o comando:

`docker ps -a --filter "label=com.docker.compose.project=petable-hml" --format "table {{.Names}}\t{{.Status}}\t{{.Ports}}"`

### Resultado observado

| Serviço | Porta no host | Resultado |
|---|---|---|
| Web | 3030 | Up |
| API | 18101 | Up (healthy) |
| MongoDB | 27139 | Up (healthy) |
| MySQL | 13327 | Up (healthy) |
| Mailpit | 18045 | Up (healthy) |

### Ocorrência durante o diagnóstico

A consulta anterior com `docker compose ps` não pôde interpretar o arquivo Compose porque as variáveis `MYSQL_PASSWORD`, `MYSQL_ROOT_PASSWORD` e `JWT_SECRET` não estavam disponíveis no contexto utilizado.

A inspeção direta pelo Docker Engine permitiu consultar os containers existentes sem modificar a configuração.

### Resultado esperado

Identificar os containers existentes, seus estados e suas portas publicadas.

### Resultado obtido

Cinco containers identificados em execução. Quatro apresentam o status `healthy`; o frontend está em execução sem indicador de healthcheck na saída.

### Conclusão

**LAB-002: Aprovado quanto à identificação e ao estado dos containers.**

A acessibilidade HTTP, o funcionamento do frontend e da API e a correspondência entre o código implantado e o commit local ainda precisam ser validados.

**Próxima etapa:** verificar o acesso HTTP ao frontend do Petable.