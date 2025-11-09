# Heimdall - Sprint 4 (Parte B) - Automação de Testes (Postman)

**Integrantes do Grupo**

- RM557541 - Leonardo Santos
- RM558243 - Pedro Santos
- RM558244 - Vitor Martins

**Repositório:** `heimdall-java` (branch `develop`)
**Collection:** `sprint4-compliance/Heimdall-Sprint4-Tests.postman_collection.json`
**Environment:** `sprint4-compliance/heimdall-local.postman_environment.json`

## AZURE BOARDS

[Link Board para HEIMDALL] - (https://dev.azure.com/MontClio/Heimdall%20Sprint%204)

## Objetivo

Esta pasta contém a Collection Postman e o Environment necessários para executar 4 testes automatizados da API HEIMDALL:

1. **POST /motorcycles** - Criar motocicleta (id controlado)
2. **GET /motorcycles/{{motoId}}** - Consultar motocicleta criada
3. **PUT /vagas/{{vagaId}}/ocupar** - Ocupar vaga pela motocicleta
4. **POST /historico** - Registrar movimentação da motocicleta

> Evidência entregue: `newman-report.html` — relatório de execução dos testes.

---

## Pré-requisitos

- API Heimdall rodando em: `http://localhost:8080`
- Java 21 + Maven (para rodar a API)
- Postman instalado ou Node.js + Newman (para rodar via CLI)

## Instruções Rápidas (Postman GUI)

1. Clone o repositório e acesse a branch `develop`:

```bash
git clone https://github.com/Leonardo-dev-br/heimdall-java.git
cd heimdall-java
git checkout develop || git switch develop
```

2. Configure o banco de dados de teste (apontar o `application.properties` para um Oracle/XE de teste).

3. Rode a aplicação:

```bash
mvn clean install
mvn spring-boot:run
```

4. No Postman:

- Import → selecione `sprint4-compliance/Heimdall-Sprint4-Tests.postman_collection.json`
- Import → selecione `sprint4-compliance/heimdall-local.postman_environment.json`
- Ative o Environment `heimdall-local`
- Abra a Collection e clique em **Run** → Execute a collection. Todos os testes devem passar.

## Rodar com Newman (CLI)

Se preferir executar via CLI (gera relatório HTML):

1. Instale newman e reporter HTML (se necessário):

```bash
npm install -g newman newman-reporter-html
```

2. Execute o comando (na pasta `sprint4-compliance`):

```bash
newman run Heimdall-Sprint4-Tests.postman_collection.json -e heimdall-local.postman_environment.json -r cli,html --reporter-html-export newman-report.html
```

3. Abra `newman-report.html` no navegador para ver o relatório (ou anexe-o na entrega).

## Observações sobre idempotência

- A Collection inclui um _pre-request script_ para o POST que tenta excluir a motocicleta antes de criar, evitando falhas por duplicidade.
- Se houver conflito de IDs, atualize a variável `motoId` no Environment para um valor não utilizado.

## Como o professor deve validar (passo-a-passo)

1. Garantir que a API esteja rodando em `http://localhost:8080` (conforme README do projeto).
2. Importar a Collection e o Environment para o Postman.
3. Executar a Collection (Run).
4. Verificar que os 4 testes passam.
5. (Opcional) Rodar com Newman e abrir o `newman-report.html` gerado.

---

## Arquivos desta pasta

- `Heimdall-Sprint4-Tests.postman_collection.json` — Collection com 4 requests e scripts de teste.
- `heimdall-local.postman_environment.json` — Environment com variáveis `baseUrl`, `motoId`, `vagaId`.
- `newman-report.html` — Relatório de execução dos testes.
- `README.md` — instruções e comandos.
