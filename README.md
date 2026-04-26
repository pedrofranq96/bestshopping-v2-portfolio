# 🛍️ BestShopping V2

Sistema de e-commerce profissional com .NET 10, Clean Architecture, DDD, Next.js, React Native e mensageria assíncrona.

📋 [Ver Backlog no Notion](https://notion.so) · 💼 [LinkedIn](https://linkedin.com/in/pedro-luiz-gutierrez) · 📧 [Email](mailto:pedromattosg26@gmail.com)

---

## 🗂️ Repositórios do Projeto

| Repositório | Descrição | Acesso |
|---|---|---|
| BestShopping.V2 — API | Backend .NET 10 · Clean Architecture · DDD · RabbitMQ | 🔒 Privado |
| BestShopping.V2 — Web | Frontend Next.js 15 · TypeScript · Tailwind CSS · shadcn/ui | 🔒 Privado |

> Este repositório é o portfólio público do projeto. Os repositórios de código-fonte são privados. Para acesso, entre em contato via LinkedIn ou Email.

---

## 💡 O que torna esse projeto diferente

A maioria dos projetos de portfólio faz CRUD com Entity Framework. O BestShopping V2 vai além:

- **Arquitetura real de produção** — Clean Architecture + DDD + Onion Architecture, com separação rígida de camadas e domínio totalmente isolado
- **Mensageria assíncrona** — RabbitMQ com um consumer por evento, retry policy com backoff exponencial e Dead Letter Queue
- **Persistência híbrida** — Dapper para leitura e EF Core para escrita
- **Testes de integração reais** — sem mocks, banco SQL Server persistente e RabbitMQ via Testcontainers (+200 testes)
- **Gateway de pagamento real** — PagSeguro via REST (Cartão, Boleto e Pix)
- **Frontend profissional** — Next.js 15 com App Router, SSR, Design System completo no Figma e integração total com a API
- **CI/CD híbrido** — GitHub Actions + Azure DevOps com deploy no Azure (planejado)

---

## 🧱 Stack Técnica

| Camada | Tecnologia |
|---|---|
| Backend | .NET 10 · ASP.NET Core |
| ORM | EF Core (writes) + Dapper (reads) |
| Banco de dados | SQL Server |
| Mensageria | RabbitMQ · Dead Letter Queue · Retry com backoff exponencial |
| Testes | xUnit · FluentAssertions · NSubstitute · Testcontainers |
| Email | MailKit + Mailtrap (dev) · Gmail SMTP (produção) |
| Gateway de Pagamento | PagSeguro Sandbox (Cartão · Boleto · Pix) |
| Documentação API | Scalar (OpenAPI nativo .NET 10) |
| Observabilidade | Serilog · Seq · CorrelationId propagado · HealthChecks |
| Frontend Web | Next.js 15 · TypeScript · Tailwind CSS · shadcn/ui · TanStack Query · Zustand |
| Mobile | React Native + Expo SDK 52 (planejado) |
| CI/CD | GitHub Actions + Azure DevOps (planejado) |
| Cloud | Azure App Service · Key Vault · Blob Storage · Service Bus (planejado) |

---

## 🏗️ Arquitetura da API

| Camada | Responsabilidade |
|---|---|
| API | Controllers, middlewares e extensions — sem lógica de negócio |
| Application | Services, DTOs, Publishers, Processors |
| Domain | Entidades, Value Objects, Interfaces, Eventos de domínio |
| Infrastructure | Repositórios, Providers (SMTP, Geolocalização, Imagem), EF Core, Dapper |
| BackgroundServices | Consumers RabbitMQ reativos, Hosted Services com timer |

**Decisões técnicas relevantes:**

- Domain totalmente isolado — nenhuma dependência de infraestrutura
- Providers abstraídos via `IXxxProvider` — SMTP, Geolocalização, Imagem e Message Bus substituíveis sem alterar código de negócio
- CorrelationId propagado em logs, filas RabbitMQ e chamadas externas
- Tokens centralizados via `ITokenService` com `RandomNumberGenerator` (crypto-safe)
- Persistência híbrida — Dapper para reads otimizados, EF Core para writes transacionais
- Logs nunca no banco SQL — Serilog + Seq em dev/staging, Application Insights em produção
- IDs tipados como `long` em todas as entidades

---

## ✅ Status do Projeto

### 🚀 Concluído — Backend API

| Onda | Descrição |
|---|---|
| Onda 0 | Foundation · Clean Architecture · DDD · Onion |
| Onda 1 | Setup inicial · estrutura de projetos · padrões base |
| Onda 2 | Autenticação · JWT · Refresh Token · bcrypt |
| Onda 3 | Catálogo de Produtos · upload de imagem · regras de domínio |
| Onda 4 | Controle de Estoque com regras de domínio |
| Onda 5 | Carrinho com validação de estoque e cupons |
| Onda 6 | Cupons de desconto |
| Onda 7 | Checkout com publicação de eventos RabbitMQ |
| Onda 8 | Pedidos com snapshot imutável de dados |
| Onda 9 | Pagamento via Cartão, Boleto e Pix (PagSeguro) |
| Onda 10 | Payment Processor · Worker com retry e Dead Letter Queue |
| Onda 11 | Email System · Mailtrap via MailKit · templates HTML · consumers RabbitMQ |
| Onda 12 | Message Bus · retry policy · DLQ · envelope padronizado · convenção de filas |
| Onda 13 | Testes completos — +200 testes de integração sem mocks |
| Onda 14 | Observabilidade · Serilog · Seq · CorrelationId · HealthChecks |
| Onda 15 | Segurança · Rate Limiting · CORS · headers HTTP · FluentValidation |
| Onda 20.7 | Perfil do Usuário (CustomerProfile) · avatar · histórico de dispositivos |

### ✍️ Em Desenvolvimento

| Onda | Descrição |
|---|---|
| Onda 17 | BestShopping.V2.Web — Frontend Next.js 15 (Blocos 4, 5, 6 e 7 em andamento) |
| Onda 20.1 | Padronização REST na API |
| Onda 20.2 | Refatoração das Services (ApplicationExceptions) |
| Onda 20.3 | Bogus nos testes de integração |
| Onda 20.4 | Polly (Retry + Circuit Breaker) nas chamadas ao PagSeguro |

### 📋 Planejado (backlog completo no Notion)

- Onda 16 — CI/CD + Cloud Migration (GitHub Actions + Azure DevOps + Azure)
- Onda 18 — BestShopping.V2.Mobile (React Native + Expo)
- Onda 19 — Documentação da API (Scalar + OpenAPI)
- Onda 20 — Webhooks PagSeguro (Pix assíncrono, Boleto, Chargeback)
- Onda 20.5 — Perfil Gestor (Gestão de Vendedores, Produtos e Categorias)
- Onda 20.9 — Galeria de Mídia Unificada (ProductMedia)
- Onda 21 — Perfil Vendedor (marketplace)
- Onda 22 — Produtos Favoritos
- Onda 23 — Cálculo de Frete (Melhor Envio)
- Onda 23.1 — Frete Grátis por Threshold de Valor
- Onda 24 — Central de Notificações (in-app + push)
- Onda 25 — Rastreamento de Entrega
- Onda 28 — Sistema de Promoções
- Onda 29 — Dashboard Analytics (Admin)
- Onda 30 — Busca Avançada (Elasticsearch)
- Onda 32 — Recomendações Inteligentes (IA)

---

## 🌐 Frontend Web — BestShopping.V2.Web

Repositório: `github.com/pedrofranq96/best-shopping-web` 🔒

Frontend do cliente (comprador) construído com Next.js 15, TypeScript, Tailwind CSS e shadcn/ui. Integrado 100% com a API .NET via Service Layer tipada com contratos alinhados aos DTOs do backend.

| Bloco | Descrição | Status |
|---|---|---|
| Bloco 1 | Autenticação completa — login, cadastro, confirmação de email, reset de senha, refresh token automático, logout com revogação | ✅ Concluído |
| Bloco 2 | Catálogo de produtos — listagem, filtro por categoria, busca, detalhe do produto com estoque em tempo real | ✅ Concluído |
| Bloco 3 | Carrinho — drawer, adicionar/remover, cupom, resumo do pedido | ✅ Concluído |
| Bloco 4 | Checkout — endereço, pagamento, PagSeguro.js, QR Code Pix, Boleto | ✍️ Em andamento |
| Bloco 5 | Pedidos — histórico, detalhe, status em tempo real com polling | ✍️ Em andamento |
| Bloco 6 | Perfil do usuário — dados cadastrais, senha, histórico de dispositivos, encerrar sessões | ✍️ Em andamento |
| Bloco 7 | UI/UX Base — footer, toasts, skeletons, 404, error boundaries, mobile first | ✍️ Em andamento |

---

## 🎨 Design System — UI/UX

O BestShopping V2 possui um Design System completo desenvolvido no Figma, cobrindo todas as interfaces da plataforma — **32 telas no total**.

### 🛍️ Store (Comprador) — 20 telas

Catálogo, Detalhe do Produto, Carrinho, Checkout (Endereço + Pagamento), Confirmação de Pedido, Meus Pedidos, Detalhe do Pedido, Rastreamento, Perfil, Favoritos, Notificações, Pontos de Fidelidade, Chat, Convite para Vendedores e mais.

### ⚙️ Painel Seller + Admin — 12 telas

Dashboard Seller, Gestão de Produtos (listagem + cadastro), Pedidos com detalhe inline, Financeiro com gráfico de comissões e saques, Avaliações, Promoções, Dashboard Admin com métricas em tempo real, Gestão de Usuários, Vendedores, Cupons e Saques.

### Identidade Visual

| Token | Cor | Uso |
|---|---|---|
| Navy | `#1A1A2E` | Marca / Topbar — fundo principal da navegação |
| Indigo | `#5B6EF5` | Primária — botões, links, badges ativos |
| Vermelho | `#E53E3E` | Ação de compra — carrinho, botão de compra |
| Âmbar | `#F5A623` | Alertas / Estrelas — avaliações, estoque baixo |
| Verde | `#2ECC71` | Sucesso / Trust — pagamento aprovado, status OK |
| Off-white | `#F7F6F3` | Surface Base — background principal |

[🎨 Visualizar Design System completo no Figma →](https://www.figma.com/design/67SfyYQtu5HnSbsUFlEKCz/BestShopping-V2-%E2%80%94-Design-System-WEB-)

> Acesso somente leitura — nenhuma alteração permitida.

---

## ☁️ Infraestrutura Cloud (planejado — Onda 16)

| Serviço | Tecnologia | Custo estimado |
|---|---|---|
| API | Azure App Service (F1) | Gratuito permanente |
| Workers | Azure Container Apps | ~R$ 5-15/mês |
| Banco | Azure SQL Database | Gratuito 12 meses |
| Imagens | Azure Blob Storage | Gratuito 12 meses |
| Secrets | Azure Key Vault | Gratuito permanente |
| Mensageria | Azure Service Bus | ~R$ 2/mês |
| Observabilidade | Azure Application Insights | Gratuito 5 GB/mês |
| CI — Build/Testes | GitHub Actions | Gratuito 2.000 min/mês |
| CD — Deploy | Azure DevOps | Gratuito 5 usuários + 1.800 min/mês |
| Frontend Web | Vercel | Gratuito permanente |
| Mobile Build | EAS Build (Expo) | 30 builds/mês gratuitos |

---

## 📚 Documentação

- 📋 [Backlog completo com 32 ondas no Notion](#)
- 📖 Regras de negócio documentadas em 27 seções
- 🏗️ Decisões arquiteturais registradas com contexto e solução
- 🎨 [Design System WEB no Figma](https://www.figma.com/design/67SfyYQtu5HnSbsUFlEKCz/BestShopping-V2-%E2%80%94-Design-System-WEB-)

---

## 📬 Contato

Sou desenvolvedor fullstack com foco em arquitetura de software e boas práticas de engenharia. Se você é recrutador e deseja acesso aos repositórios privados, entre em contato:

💼 [LinkedIn — Pedro Luiz Gutierrez](https://linkedin.com/in/pedro-luiz-gutierrez)
📧 pedromattosg26@gmail.com
