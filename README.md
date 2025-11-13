# 🧾 Order Management System (Sistema de Pedidos)

## 🧩 Descrição Curta

Sistema desenvolvido em **Java (Spring Boot)** com **PostgreSQL** e **AWS** (RDS, SQS, CloudWatch, Beanstalk) para gerenciar o ciclo completo de pedidos — desde a criação até a atualização do status e comunicação com o sistema de pagamentos.

**Custo estimado:** 💰 R$ 0,00 (dentro do AWS Free Tier)

---

## 🚀 Visão Geral do Projeto

Este projeto implementa um sistema de gerenciamento de pedidos (Order Management System), que permite:

* Criar, atualizar e listar pedidos via API REST.
* Persistir dados em **PostgreSQL (AWS RDS)**.
* Publicar mensagens em **AWS SQS** para comunicação assíncrona com outros serviços (ex: pagamento).
* Monitorar logs e métricas com **AWS CloudWatch**.

### Tecnologias Principais

* **Java 17**
* **Spring Boot 3+ (Web, Data JPA, Validation)**
* **PostgreSQL** (local e AWS RDS)
* **AWS SQS / SNS**
* **AWS CloudWatch**
* **Elastic Beanstalk (deploy)**
* **JUnit / Mockito (testes)**

---

## ⚙️ Arquitetura

```
[Frontend opcional]
      ↓
[API Gateway ou Beanstalk]
      ↓
Spring Boot (Order Service)
├── Controller
├── Service
├── Repository
└── Publisher (envia mensagens SQS)
      ↓
AWS SQS → Payment Service → PostgreSQL
```

---

## 🧰 Configuração Local com Docker e LocalStack

### 1️⃣ Clonar o projeto

```bash
git clone https://github.com/seu-usuario/order-management-system.git
cd order-management-system
```

### 2️⃣ Subir ambiente local (PostgreSQL + LocalStack)

```bash
docker-compose up -d
```

### 3️⃣ Variáveis de Ambiente

Crie um arquivo `.env`:

```bash
DB_URL=jdbc:postgresql://localhost:5432/orders
DB_USER=postgres
DB_PASS=postgres
AWS_REGION=us-east-1
AWS_SQS_URL=http://localhost:4566/000000000000/order-queue
```

### 4️⃣ Rodar a aplicação

```bash
./mvnw spring-boot:run
```

### 5️⃣ Testar API

**POST /orders**

```json
{
  "customerId": 1,
  "items": [
    { "productId": 101, "quantity": 2 },
    { "productId": 305, "quantity": 1 }
  ]
}
```

**Response:**

```json
{
  "orderId": 1,
  "status": "PENDING",
  "createdAt": "2025-11-13T22:14:55Z"
}
```

---

## 🧪 Testes

Executar todos os testes:

```bash
./mvnw test
```

---

## ☁️ Deploy AWS (Elastic Beanstalk)

1. Criar app Elastic Beanstalk (Java 17 + Corretto).
2. Configurar variáveis de ambiente no painel.
3. Fazer deploy via GitHub Actions ou CLI:

```bash
ever beanstalk deploy order-management
```

---

## 📈 Monitoramento (CloudWatch)

* Logs de aplicação e fila (SQS).
* Métricas: mensagens processadas, erros, tempo de resposta.

---

## 🧾 Custos Estimados

| Serviço                       | Custo (Free Tier)         |
| ----------------------------- | ------------------------- |
| AWS RDS (PostgreSQL)          | ✅ Grátis até 750h/mês     |
| AWS SQS                       | ✅ 1 milhão req/mês grátis |
| Elastic Beanstalk (EC2 micro) | ✅ Grátis 750h/mês         |
| CloudWatch                    | ✅ 5GB logs/mês grátis     |
| **Total estimado**            | 💵 **R$ 0,00/mês**        |

---



