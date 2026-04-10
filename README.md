<div align="center">
  <h1>🛍️ BestShopping V2</h1>
  <p>
    <strong>Sistema de e-commerce profissional com .NET 10, Clean Architecture, DDD e mensageria assíncrona</strong>
  </p>
  <p>
    <a href="https://www.notion.so/Planejamento-BestShopping-V2-e6808fc8333d83dbb8fa0140834772be">📋 Ver Backlog no Notion</a>
    ·
    <a href="https://www.linkedin.com/in/pedro-luiz-gutierrez/">💼 LinkedIn</a>
    ·
    <a href="mailto:pedromattosg26@gmail.com">📧 Email</a>
  </p>
</div>

---

## 💡 O que torna esse projeto diferente

A maioria dos projetos de portfólio faz CRUD com Entity Framework.
O BestShopping V2 vai além:

- **Arquitetura real de produção** — Clean Architecture + DDD + Onion,
  com separação rígida de camadas e domínio totalmente isolado
- **Mensageria assíncrona** — RabbitMQ com um consumer por evento,
  retry policy com backoff exponencial e Dead Letter Queue
- **Persistência híbrida** — Dapper para leitura e EF Core para escrita
- **Testes de integração reais** — sem mocks, banco SQL Server
  persistente e RabbitMQ via Testcontainers
- **Gateway de pagamento real** — PagSeguro via REST
  (Cartão, Boleto e Pix)

---

## 🧱 Stack Técnica

| Camada | Tecnologia |
|---|---|
| Backend | .NET 10 · ASP.NET Core |
| ORM | EF Core (writes) + Dapper (reads) |
| Banco de dados | SQL Server |
| Mensageria | RabbitMQ |
| Testes | xUnit · FluentAssertions · Testcontainers |
| Email | MailKit + Mailtrap |
| Gateway de Pagamento | PagSeguro Sandbox |
| Documentação API | Scalar (OpenAPI nativo .NET 10) |
| Frontend Web | Next.js 15 + TypeScript + Tailwind CSS *(planejado)* |
| Mobile | React Native + Expo SDK 52 *(planejado)* |
| Painel Vendedor | Angular 19 *(planejado)* |
| CI/CD | Azure DevOps *(planejado)* |
| Cloud | Azure App Service · Key Vault · Blob Storage *(planejado)* |

---

## 🏗️ Arquitetura da API

| Camada | Definição |
|---|---|
| API | Controllers, middlewares e extensions |
| Application | Services, DTOs, Publishers |
| Domain | Entidades, VOs, Interfaces, Eventos |
| Infrastructure | Repositórios, Providers, EF Core |
| BackgroundServices | Consumers RabbitMQ, Hosted Services |

---

## ✅ Status do Projeto

### Implementado
- [x] Catálogo de produtos com upload de imagem
- [x] Controle de estoque com regras de domínio
- [x] Carrinho com validação de estoque e cupons
- [x] Checkout com publicação de eventos RabbitMQ
- [x] Pedidos com snapshot imutável de dados
- [x] Pagamento via Cartão, Boleto e Pix (PagSeguro)
- [x] Worker de processamento com retry e Dead Letter Queue
- [x] +200 testes de integração sem mocks

### Em desenvolvimento
- [ ] Sistema de email transacional completo (Onda 11)
  - Confirmação de conta e reset de senha
  - Detecção de novo dispositivo (IP + localização)
  - Notificações de pagamento e pedido

### Planejado (32 ondas no backlog)
- [ ] Perfil Vendedor — marketplace style (Angular 19)
- [ ] Produtos Favoritos
- [ ] Webhooks PagSeguro (Pix assíncrono, Boleto, Chargeback)
- [ ] Frontend Web (Next.js 15)
- [ ] App Mobile (React Native + Expo)
- [ ] Avaliações e Reviews
- [ ] Sistema de Promoções
- [ ] Busca Avançada com Elasticsearch
- [ ] Cloud Migration (Azure)

---

## 📐 Decisões técnicas relevantes

- **Domain totalmente isolado** — nenhuma dependência de infraestrutura
- **Providers abstraídos** — SMTP, Geolocalização e Imagem substituíveis
  sem alterar código de negócio
- **CorrelationId** propagado em logs, filas e chamadas externas
- **Tokens centralizados** via `ITokenService` com `RandomNumberGenerator`
- **Logs nunca no banco SQL** — Serilog + Seq
- **Feature flags por ambiente** — local em dev, cloud em produção

---

## 🎨 Design System — UI/UX

O BestShopping V2 possui um **Design System completo** desenvolvido no Figma, cobrindo todas as interfaces da plataforma — **32 telas no total**.

### 🛍️ Store (Comprador) — 20 telas
Catálogo, Detalhe do Produto, Carrinho, Checkout (Endereço + Pagamento), Confirmação de Pedido, Meus Pedidos, Detalhe do Pedido, Rastreamento, Perfil, Favoritos, Notificações, Pontos de Fidelidade, Chat, Convite para Vendedores e mais.

### ⚙️ Painel Seller + Admin — 12 telas
Dashboard Seller, Gestão de Produtos (listagem + cadastro), Pedidos com detalhe inline, Financeiro com gráfico de comissões e saques, Avaliações, Promoções, Dashboard Admin com métricas em tempo real, Gestão de Usuários, Vendedores, Cupons e Saques.

### Identidade Visual

| Token | Cor | Uso |
|---|---|---|
| Navy `#1A1A2E` | Marca / Topbar | Fundo principal da navegação |
| Indigo `#5B6EF5` | Primária | Botões, links, badges ativos |
| Vermelho `#E53E3E` | Ação de compra | Carrinho, botão de compra |
| Âmbar `#F5A623` | Alertas / Estrelas | Avaliações, estoque baixo |
| Verde `#2ECC71` | Sucesso / Trust | Pagamento aprovado, status OK |

> 🎨 **[Visualizar Design System completo no Figma →](https://www.figma.com/design/67SfyYQtu5HnSbsUFlEKCz/BestShopping-V2-%E2%80%94-Design-System-WEB-?node-id=5-2&t=4t6jtfRc8qapkLfW-1)**
>
> Acesso somente leitura — nenhuma alteração permitida.

---

## 📚 Documentação

- 📋 [Backlog completo com 32 ondas no Notion](https://www.notion.so/Planejamento-BestShopping-V2-e6808fc8333d83dbb8fa0140834772be)
- 📖 Regras de negócio documentadas em 27 seções
- 🏗️ Decisões arquiteturais registradas com contexto e solução
- 🎨 [Design System WEB no Figma](https://www.figma.com/design/67SfyYQtu5HnSbsUFlEKCz/BestShopping-V2-%E2%80%94-Design-System-WEB-?node-id=5-2&t=4t6jtfRc8qapkLfW-1)

---

## 📬 Contato

Sou desenvolvedor .NET com foco em arquitetura de software e boas práticas de engenharia.
Se você é recrutador e deseja acesso ao repositório privado, entre em contato:

- 💼 [LinkedIn — Pedro Luiz Gutierrez](https://www.linkedin.com/in/pedro-luiz-gutierrez/)
- 📧 [pedromattosg26@gmail.com](mailto:pedromattosg26@gmail.com)
