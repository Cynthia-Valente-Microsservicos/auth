# Auth

Módulo de contrato compartilhado para o serviço de autenticação. Funciona como uma **biblioteca de API**, definindo as interfaces Feign, DTOs de requisição/resposta e constantes de cookie utilizadas pelo `auth-service` e pelo `gateway-service`.

## Tecnologias

- Java 25
- Spring Boot 4.0.3
- Spring Cloud 2025.1.0 (OpenFeign)
- Lombok

## Estrutura

Este módulo **não é uma aplicação executável**. É empacotado como dependência Maven e consumido pelo `gateway-service` e outros serviços que precisam interagir com autenticação.

```
store:auth:1.0.0
```

## Feign Client

A interface `AuthController` define os endpoints expostos pelo `auth-service`:

| Método | Endpoint | Descrição |
|--------|----------|-----------|
| `POST` | `/auth/login` | Autenticação com email e senha |
| `POST` | `/auth/register` | Registro de novo usuário |
| `GET` | `/auth/whoiam` | Retorna dados do usuário autenticado (header `id-account`) |
| `POST` | `/auth/solve` | Valida e decodifica um token JWT |
| `GET` | `/auth/logout` | Encerra a sessão (limpa o cookie) |
| `GET` | `/auth/health-check` | Health check |

**Constante de cookie:** `__store_jwt_token`

## DTOs

**`LoginIn`** — requisição de login
```
email:    String
password: String
```

**`RegisterIn`** — requisição de registro
```
name:     String
email:    String
password: String
```

**`TokenOut`** — token JWT
```
token: String
```

## Como usar

Adicione ao `pom.xml` do serviço consumidor:

```xml
<dependency>
    <groupId>store</groupId>
    <artifactId>auth</artifactId>
    <version>1.0.0</version>
</dependency>
```

Instale no repositório local antes:

```bash
mvn install -DskipTests
```
