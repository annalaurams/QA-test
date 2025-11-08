# Projeto CRUD com Testes e Docker

Este projeto implementa um CRUD completo de usuários com **backend, frontend, PostgreSQL, Docker e testes com Jest, Cypress e Playwright.**

---

## 📄 Slides e Exemplos de Testes

O repositório inclui:
- Uma **apresentação em PDF** com um resumo da área de **QA (Quality Assurance)** e comparações entre as ferramentas **Jest** e **Cypress**: [`QA.pdf`](./QA.pdf)
- Uma amostra de testes com **Jest**, localizada na pasta `server/__tests__`
- Uma amostra de testes com **Cypress**, localizada na pasta `client/cypress`
- Uma amostra de testes com **Playwright**, localizada na pasta `tests`
- Arquivos **docker**, localizados na pasta `server`

---

## 🗄️ Banco de Dados
O projeto utiliza PostgreSQL como banco de dados, gerenciado pelo Prisma.

Crie um arquivo `.env` dentro da pasta `server` com a URL de conexão do PostgreSQL:

**Para desenvolvimento local (sem Docker no backend):**
```env
DATABASE_URL="postgresql://qa_user:<suasenha>@localhost:5433/<banco>?schema=qa"
```

**Para uso com Docker Compose (backend + banco):**
```env
DATABASE_URL="postgresql://usuario:<sua_senha>@postgres:5432/nome_banco?schema=qa"
```
### 🔧 Comandos do Prisma

Após configurar o `.env`, execute os seguintes comandos:

```bash
# Gerar o Prisma Client
npx prisma generate

# Criar e aplicar migrations
npx prisma migrate dev --name init-postgres

# Alternativa: sincronizar schema sem criar migration
npx prisma db push
```

---

## 🐳 Docker

O projeto está configurado para rodar com **Docker** e **Docker Compose**, facilitando a configuração do ambiente.

### 🚀 Como Rodar o Projeto

Você pode rodar o projeto de duas formas:

#### **A) Rodar Localmente (sem Docker para o backend)**

Suba apenas o PostgreSQL via Docker Compose:

```bash
cd server
docker compose up -d postgres
```

O banco ficará acessível em `localhost:5433`.

Configure o `.env` local (veja seção acima) e instale as dependências:

```bash
cd server
npm install
npx prisma generate
npx prisma migrate dev --name init-postgres
npm run dev
```

Acesse o backend em: **http://localhost:3000**

---

#### **B) Rodar Tudo com Docker Compose (backend + banco)**

Configure o `.env` para Docker (veja seção acima) e suba os serviços:

```bash
cd server
docker compose up --build -d
```

Acesse:
- **Backend:** http://localhost:4000 (mapeado de 4000:3000)
- **Banco de dados:** `localhost:5433` (opcional, para conexões externas)

Para visualizar os logs:

```bash
docker compose logs -f
```

---

## 📝 Observações

- O backend está configurado para executar automaticamente `prisma generate` e `prisma migrate deploy` ao iniciar no Docker
- A porta `5433` é usada para evitar conflitos com instalações locais do PostgreSQL (porta padrão 5432)
- O mapeamento de portas `4000:3000` permite rodar o backend na porta 4000 do host, enquanto o container usa a porta 3000

---

## 🧪 Testes

Os exemplos de testes estão disponíveis nas pastas mencionadas no início deste documento. Consulte o PDF incluído para mais informações sobre QA e as ferramentas de teste utilizadas.

### Backend com jest

| Etapa                 | Comando          |
|----------------------|------------------|
| Acessar              | `cd server`      |
| Instalar dependências| `npm install`    |
| Iniciar backend      | `npm run dev`    |
| Rodar testes com Jest| `npm test`       |

---

### Frontend com cypress

| Etapa                    | Comando             |
|--------------------------|---------------------|
| Acessar                  | `cd client`         |
| Instalar dependências    | `npm install`       |
| Iniciar frontend         | `npm run dev`       |
| Rodar testes com Cypress | `npx cypress open`  |
| Acessar no navegador     | [http://localhost:5173/](http://localhost:5173/) |


---

### Teste com Playwright

| Etapa                          | Comando                                        |
| ------------------------------ | ---------------------------------------------- |
| Acessar a pasta de testes      | `cd tests`                                     |
| Rodar os testes automatizados  | `npx playwright test`                          |
| Ver relatório em HTML          | `npx playwright show-report`                   |
| Acessar relatório no navegador | [http://localhost:9323](http://localhost:9323) |


## 📫 Contato

Criado por Anna Laura Moura  
📧 [nalauramoura@gmail.com](mailto:nalauramoura@gmail.com)
