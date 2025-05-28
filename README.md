# 🌩️ Arkstorm – Monitoramento de Apagões por Clima

O Arkstorm é um sistema completo para monitorar condições climáticas adversas e prever riscos de apagão. Ele coleta dados de APIs públicas e permite consultas por cidade, endereço e histórico.

- Julia Marques (RM98680)
- Guilherme Morais (RM551981)
- Matheus Gusmão (RM550826)

## 📦 Funcionalidades

- Previsão do tempo por cidade
- Avaliação de risco de apagão
- Registro de alertas em banco de dados Oracle
- Consulta de histórico de alertas
- Consulta por endereço (com geocodificação)
- Relatório dos últimos X dias
- API documentada com Swagger

## 🚀 Tecnologias Utilizadas

- Java 17+
- Spring Boot
- Spring Data JPA
- Banco de Dados Oracle
- API OpenWeatherMap
- API Nominatim (OpenStreetMap)
- Swagger via Springdoc OpenAPI

## 🛠️ Dependências principais

- spring-boot-starter-web
- spring-boot-starter-data-jpa
- ojdbc11 (Oracle)
- org.json
- springdoc-openapi-ui

## ⚙️ Execução

1. Configure o Oracle e crie um schema com permissão de criação de tabelas.
2. Ajuste o arquivo application.properties com as credenciais.
3. Execute o projeto com:

```bash
./mvnw spring-boot:run
```
4. Acesse o Swagger UI:
[text](http://localhost:8080/swagger-ui.html)

## 📌 Observações

- O sistema cria as tabelas automaticamente se não existirem (ddl-auto=update).
- O endpoint por endereço depende de acesso à internet para a API de geocodificação.

## 🗂️ Diagrama de Entidade-Relacionamento (ER)

```mermaid
erDiagram
    WeatherAlert {
        Long id PK
        String city
        String description
        String riskLevel
        LocalDateTime timestamp
    }
```

## 🔁 Diagrama de Workflow (Fluxo de Uso)

```mermaid
graph TD
    A[Usuário informa cidade ou endereço] --> B[API Controller recebe solicitação]
    B --> C[Service consulta clima via API externa]
    C --> D[Service avalia risco de apagão]
    D --> E[Salva alerta no banco Oracle]
    E --> F[Resposta JSON com status e risco]
    F --> G[Usuário visualiza no app ou front-end]

    B --> H[Histórico por cidade]
    H --> I[Consulta repository e retorna lista]

    B --> J[Relatório por período]
    J --> K[Consulta banco com filtro de data]
    K --> L[Gera resumo com total e riscos]
```
