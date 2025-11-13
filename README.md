# Order-Management-System-Sistema-de-Pedidos-
Microserviço em Java (Spring Boot) responsável por receber, validar e persistir pedidos. Usa PostgreSQL para armazenamento relacional e publica eventos em AWS SQS/SNS para integrar-se com serviços downstream (ex.: Payment Service, Notification Service). Projetado para processamento síncrono da API e processamento assíncrono de tarefas via filas.
