<div align="center">

# 🌱 EcoFood

**Plataforma de redistribuição de excedentes alimentares**

Conecta estabelecimentos com sobra de alimento a ONGs, abrigos e famílias — reduzindo desperdício e combatendo a fome.

[![.NET](https://img.shields.io/badge/.NET_10-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)](https://dotnet.microsoft.com/)
[![React](https://img.shields.io/badge/React_19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)
[![MySQL](https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com/)
[![Vite](https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vite.dev/)
[![Tailwind](https://img.shields.io/badge/Tailwind-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)

🎯 **ODS 12** — Consumo e Produção Responsáveis &nbsp;·&nbsp; 🍽️ **ODS 2** — Fome Zero

</div>

---
## 💻 Desenvolvedores
 - Caio Cesar - [QA]
 - Caio Menezes - [Dev. Frontend]
 - Caik Lima - [Dev. Backend]
 - Luiz Henrique - [Dev. Backend]
 - Marlon Bartoli - [Dev/Tester]
---

## 📖 Sobre o projeto

O EcoFood resolve um problema simples de enunciar e difícil de operacionalizar: **comida boa sendo descartada enquanto gente passa fome a poucos quarteirões de distância.**

A plataforma tem três atores:

| Ator | O que faz |
|------|-----------|
| 🏪 **Doador** | Estabelecimento com excedente (padaria, mercado, restaurante). Publica o que tem disponível. |
| 🤝 **Receptor** | ONG, abrigo ou família. Navega as doações e reserva o que consegue retirar. |
| 🛡️ **Admin** | Perfil de gestão previsto no modelo de dados. |

### A regra central: confirmação de endereço

Nenhuma reserva é criada sem que o receptor **confirme explicitamente** que viu e aceita o endereço de retirada. Essa regra vive na API — não apenas na tela:

- O campo `enderecoConfirmado` precisa chegar como `true`, senão a API devolve `400 Bad Request`.
- O endereço gravado na reserva (`EnderecoRetiradaSnapshot`) é copiado **do cadastro do doador no servidor**, nunca do que o cliente enviou. Assim o cliente não consegue registrar um endereço diferente do real.
- Marcar a doação como `Reservado` e criar a reserva acontecem dentro de uma **transação** — se um passo falhar, o outro é desfeito.

---

## 🧰 Stack

### Backend

| | Tecnologia | Versão | Papel |
|---|---|---|---|
| 🟣 | **.NET / ASP.NET Core** | 10.0 | API REST |
| 🗃️ | **Entity Framework Core** | 9.0.13 | ORM e migrations |
| 🐬 | **Pomelo.EntityFrameworkCore.MySql** | 9.0.0 | Provider MySQL para o EF |
| 📘 | **Swashbuckle (Swagger)** | 10.3.1 | Documentação interativa da API |
| 🧪 | **xUnit** | 2.9.3 | Testes de unidade e integração |

### Frontend

| | Tecnologia | Versão | Papel |
|---|---|---|---|
| ⚛️ | **React** | 19.3.1 | Interface |
| ⚡ | **Vite** | 8.3.4 | Build e dev server |
| 🔷 | **TypeScript** | 6.0 | Tipagem estática |
| 🎨 | **Tailwind CSS** | 3.4.13 | Estilização |
| 🧭 | **React Router** | 7.18.4 | Navegação entre telas |
| 🔄 | **TanStack Query** | 5.56.2 | Cache e sincronização de dados |
| 📡 | **Axios** | 1.7.7 | Cliente HTTP |
| 🧪 | **Vitest + Testing Library** | 5.0.5 | Testes de componente |

### Banco de dados

| | Tecnologia | Papel |
|---|---|---|
| 🐬 | **MySQL 8** | Persistência (`utf8mb4`, InnoDB) |

---

## 📁 Estrutura do repositório

```
EcoFood/
├── Database/
│   └── init.sql                  # Schema + índices + dados de exemplo
├── Documents/                    # Documentação acadêmica e apresentação
├── EcoFood_Api/
│   ├── EcoFood.Api/
│   │   ├── Controllers/          # Usuarios, Doacoes, Reservas
│   │   ├── Data/AppDbContext.cs  # Mapeamento EF Core
│   │   ├── Dtos/                 # Contratos de entrada e saída
│   │   ├── Models/               # Entidades e enums
│   │   ├── Migrations/           # Migrations do EF Core
│   │   └── Program.cs            # DI, CORS, Swagger, JSON
│   └── EcoFood.Api.Tests/        # Testes xUnit
└── EcoFood.Web/
    └── src/
        ├── api/                  # client.ts (Axios) + recursos.ts
        ├── components/           # StatusChip, DoacaoCard, ConfirmarEnderecoPanel
        ├── context/              # PerfilContext (perfil ativo)
        ├── pages/                # Doacoes, NovaDoacao, MinhasReservas, Pessoas
        └── types/                # Tipos compartilhados
```

---

## ✅ Pré-requisitos

Antes de começar, instale:

| Requisito | Versão mínima | Como verificar |
|---|---|---|
| [.NET SDK](https://dotnet.microsoft.com/download) | **10.0** | `dotnet --version` |
| [Node.js](https://nodejs.org/) | **20 LTS** | `node --version` |
| [MySQL Server](https://dev.mysql.com/downloads/mysql/) | **8.0** | `mysql --version` |
| [Git](https://git-scm.com/) | qualquer | `git --version` |

> 💡 **MySQL Workbench** é opcional, mas ajuda a inspecionar o banco durante a apresentação.

---

## 🚀 Instalação

### 1️⃣ Clone o repositório

```bash
git clone <url-do-repositorio>
cd EcoFood
```

### 2️⃣ Crie o banco de dados

O script `Database/init.sql` cria o schema completo **e já insere dados de exemplo** (3 doadores, 2 receptores, 3 doações) — você consegue demonstrar o sistema imediatamente.

**Pelo terminal:**

```bash
mysql -u root -p < Database/init.sql
```

**Ou pelo MySQL Workbench:** abra o arquivo `Database/init.sql` e execute (⚡ *Execute Script*).

Confirme que funcionou:

```sql
USE ecofood;
SELECT Nome, TipoUsuario FROM Usuarios;
```

### 3️⃣ Configure a senha do banco na API

A string de conexão **não deve ser commitada com a sua senha**. Use o *user secrets* do .NET, que guarda o valor fora do repositório:

```bash
cd EcoFood_Api/EcoFood.Api

dotnet user-secrets set "ConnectionStrings:DefaultConnection" \
  "Server=localhost;Port=3306;Database=ecofood;User=root;Password=SUA_SENHA;"
```

<details>
<summary>💻 No PowerShell (Windows)</summary>

```powershell
cd EcoFood_Api\EcoFood.Api

dotnet user-secrets set "ConnectionStrings:DefaultConnection" "Server=localhost;Port=3306;Database=ecofood;User=root;Password=SUA_SENHA;"
```

</details>

Verifique o que ficou salvo:

```bash
dotnet user-secrets list
```

> ⚠️ O *user secret* tem **prioridade sobre o `appsettings.json`** em ambiente de desenvolvimento. Se a conexão falhar com uma senha que você jurava estar certa, confira o secret antes do `appsettings.json`.

### 4️⃣ Instale as dependências do frontend

```bash
cd EcoFood.Web
npm install
```

---

## ▶️ Rodando o sistema

O EcoFood precisa de **dois terminais rodando ao mesmo tempo** — a API e o frontend são processos separados.

### 🖥️ Terminal 1 — API

```bash
cd EcoFood_Api/EcoFood.Api
dotnet run
```

Aguarde a mensagem:

```
Now listening on: http://localhost:5050
```

### 🖥️ Terminal 2 — Frontend

```bash
cd EcoFood.Web
npm run dev
```

Aguarde:

```
➜  Local:   http://localhost:5173/
```

### 🌐 Acessos

| Serviço | URL |
|---|---|
| 🖼️ **Aplicação web** | http://localhost:5173 |
| 📘 **Swagger (API)** | http://localhost:5050/swagger |
| 🔌 **API base** | http://localhost:5050/api |

> 🔑 **Primeiro passo na interface:** selecione um perfil no seletor do topo (ou cadastre um na aba *Pessoas*). Quase todas as ações dependem de haver um perfil ativo — doar exige um **Doador**, reservar exige um **Receptor**.

### ⚙️ Sobre as portas

A porta da API é definida em `EcoFood_Api/EcoFood.Api/Properties/launchSettings.json` e o frontend espera encontrá-la em `http://localhost:5050/api`.

Se precisar usar outra porta na API, aponte o frontend para ela criando um `.env` **na raiz de `EcoFood.Web/`** (não dentro de `src/` — o Vite só lê da raiz do projeto):

```ini
# EcoFood.Web/.env
VITE_API_BASE_URL=http://localhost:5158/api
```

> 🔁 O Vite só lê variáveis de ambiente **na inicialização**. Depois de criar ou editar o `.env`, reinicie o `npm run dev`.

---

## 🔌 Endpoints da API

### 👤 Usuários

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/usuarios` | Lista usuários. Filtro opcional: `?tipo=Doador\|Receptor\|Admin` |
| `GET` | `/api/usuarios/{id}` | Busca um usuário |
| `POST` | `/api/usuarios` | Cadastra usuário |

```jsonc
// POST /api/usuarios
{
  "nome": "ONG Mesa Solidaria",
  "email": "ong@exemplo.com",
  "telefone": "31999990004",
  "tipoUsuario": "Receptor",
  "endereco": "R. da Esperanca, 50 - Contagem/MG"
}
```

### 🥗 Doações

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/doacoes` | Lista doações. Filtro opcional: `?status=Disponivel` |
| `GET` | `/api/doacoes/{id}` | Busca uma doação |
| `POST` | `/api/doacoes` | Publica uma doação |
| `PUT` | `/api/doacoes/{id}/cancelar` | Cancela a doação |

### 📦 Reservas

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/reservas` | Lista reservas. Filtro opcional: `?receptorId=4` |
| `POST` | `/api/reservas` | Cria reserva — **exige `enderecoConfirmado: true`** |
| `PUT` | `/api/reservas/{id}/concluir` | Marca retirada concluída (doação → `Retirado`) |
| `PUT` | `/api/reservas/{id}/cancelar` | Cancela (doação volta a `Disponivel`) |

---

## 🛡️ Demonstrando a regra de negócio

A validação **não depende da interface**. Chamando a API diretamente com `enderecoConfirmado: false`:

```bash
curl -i -X POST http://localhost:5050/api/reservas \
  -H "Content-Type: application/json" \
  -d '{"doacaoId":2,"receptorId":4,"enderecoConfirmado":false}'
```

<details>
<summary>💻 No PowerShell (Windows)</summary>

```powershell
try {
  Invoke-WebRequest -Uri "http://localhost:5050/api/reservas" -Method Post `
    -ContentType "application/json" `
    -Body '{"doacaoId":2,"receptorId":4,"enderecoConfirmado":false}'
} catch {
  $_.Exception.Response.StatusCode
  $_.ErrorDetails.Message
}
```

</details>

**Resposta esperada — `400 Bad Request`:**

```json
{ "mensagem": "E necessario confirmar o endereco de retirada antes de reservar." }
```

Isso prova que, mesmo contornando a tela, ninguém reserva sem confirmar o endereço.

---

## 🧪 Testes

### Backend (xUnit)

```bash
cd EcoFood_Api
dotnet test
```

Cobre os três controllers, usando `EntityFrameworkCore.InMemory` para os testes de unidade e `Mvc.Testing` para os de integração ponta a ponta.

### Frontend (Vitest)

```bash
cd EcoFood.Web
npm test
```

---

## 🗄️ Modelo de dados

```
┌──────────────┐          ┌──────────────┐          ┌──────────────┐
│   Usuarios   │          │   Doacoes    │          │   Reservas   │
├──────────────┤          ├──────────────┤          ├──────────────┤
│ Id       PK  │◄────┐    │ Id       PK  │◄───1:1──►│ Id       PK  │
│ Nome         │     └────│ DoadorId FK  │          │ DoacaoId FK  │
│ Email     UQ │          │ Descricao    │     ┌────│ ReceptorId FK│
│ Telefone     │          │ Categoria    │     │    │ EnderecoConf.│
│ TipoUsuario  │          │ Quantidade   │     │    │ EnderecoSnap.│
│ Endereco     │          │ UnidadeMedida│     │    │ DataReserva  │
│ DataCadastro │          │ ValidadeAlim.│     │    │ DataRetirada │
└──────────────┘          │ Status       │     │    │ Status       │
        ▲                 │ Observacoes  │     │    └──────────────┘
        └─────────────────┴──────────────┘     │
                                               │
                        Receptor ──────────────┘
```

**Enums:**

| Campo | Valores |
|---|---|
| `TipoUsuario` | `Doador` · `Receptor` · `Admin` |
| `StatusDoacao` | `Disponivel` · `Reservado` · `Retirado` · `Expirado` · `Cancelado` |
| `StatusReserva` | `Pendente` · `Concluida` · `Cancelada` |

> 🔒 A constraint `uq_reserva_doacao` garante **uma reserva por doação** no nível do banco — duas ONGs não conseguem reservar a mesma comida.

---

## 🩺 Solução de problemas

<details>
<summary><b>❌ Swagger ou o frontend retorna 500 ao buscar dados</b></summary>

Quase sempre é conexão com o MySQL. Rode a API pelo terminal (`dotnet run`) e leia o erro:

| Mensagem no log | Causa | Solução |
|---|---|---|
| `Access denied ... (using password: YES)` | Senha incorreta | Refaça o `dotnet user-secrets set` |
| `Access denied ... (using password: NO)` | Senha vazia chegando | Existe um *user secret* sem senha sobrescrevendo o `appsettings.json` — rode `dotnet user-secrets list` |
| `Unable to connect` | MySQL parado | Inicie o serviço MySQL |
| `Table 'ecofood.Usuarios' doesn't exist` | Schema não criado | Execute `Database/init.sql` |

</details>

<details>
<summary><b>❌ "Nao foi possivel falar com a API"</b></summary>

A API não está rodando, ou está em uma porta diferente da que o frontend procura.

1. Confirme que o terminal da API mostra `Now listening on: http://localhost:5050`
2. Se estiver em outra porta, ajuste o `launchSettings.json` **ou** crie `EcoFood.Web/.env` com `VITE_API_BASE_URL`
3. Reinicie o `npm run dev` após mexer no `.env`

</details>

<details>
<summary><b>❌ O seletor de perfil aparece vazio</b></summary>

A chamada a `GET /api/usuarios` está falhando silenciosamente. Teste direto no navegador: http://localhost:5050/api/usuarios

- Retornou `[]` → o banco está vazio, execute `Database/init.sql`
- Deu erro → veja o bloco de erro 500 acima

</details>

<details>
<summary><b>❌ "Failed to bind to address ... address already in use"</b></summary>

Já existe uma API rodando nessa porta.

```powershell
# Windows — descobre e encerra o processo
Get-NetTCPConnection -LocalPort 5050 | Select-Object -First 1 -ExpandProperty OwningProcess | Stop-Process -Force
```

```bash
# Linux / macOS
lsof -ti:5050 | xargs kill -9
```

</details>

<details>
<summary><b>❌ "Could not find the global property 'UserSecretsId'"</b></summary>

O `EcoFood.Api.csproj` precisa da propriedade abaixo dentro do `<PropertyGroup>`:

```xml
<UserSecretsId>ecofood-api</UserSecretsId>
```

</details>

<details>
<summary><b>❌ "O caminho do arquivo fornecido não existe" ao usar --project</b></summary>

O caminho em `--project` é relativo ao diretório atual. Rode a partir da raiz do repositório, ou omita o `--project` se já estiver dentro de `EcoFood_Api/EcoFood.Api`.

</details>

---

## 🔐 Segurança e configuração local

- Credenciais de banco ficam em **user secrets**, nunca no código versionado.
- `appsettings.json`, `.env*` e artefatos de build (`bin/`, `obj/`, `node_modules/`) estão no `.gitignore`.
- O CORS libera apenas `http://localhost:5173` por padrão, configurável via `Cors:AllowedOrigin`.

---

<div align="center">

**Projeto acadêmico A3** · Desenvolvido com foco nos Objetivos de Desenvolvimento Sustentável da ONU

🌱 *Menos desperdício. Mais pratos cheios.*

</div>