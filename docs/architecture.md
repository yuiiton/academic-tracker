# Arquitetura do Academic Tracker

## 1. Visão geral

O Academic Tracker é uma aplicação pessoal para acompanhamento de frequência acadêmica.

O sistema foi projetado para controlar apenas o estado atual das disciplinas do semestre vigente, evitando o armazenamento de dados históricos que não possuem valor para o objetivo principal da aplicação.

---

## 2. Princípios arquiteturais

As principais decisões que guiam o projeto são:

- Resolver apenas o problema necessário atualmente.
- Evitar complexidade sem benefício real.
- Separar responsabilidades entre as camadas da aplicação.
- Manter regras de negócio independentes da persistência.
- Armazenar apenas os dados essenciais para o funcionamento do sistema.

---

## 3. Arquitetura em camadas

O projeto segue uma arquitetura baseada na separação de responsabilidades:

```text
Frontend
   |
   ↓
API Layer
   |
   ↓
Service Layer
   |
   ↓
Repository Layer
   |
   ↓
Database
```

### API Layer

Responsável por:

- Receber requisições.
- Validar dados de entrada.
- Retornar respostas ao cliente.

Não deve conter regras de negócio.

---

### Service Layer

Responsável por:

- Regras de negócio da aplicação.
- Validações.
- Cálculos derivados.
- Definição de status e métricas.

Exemplos:

- Cálculo do percentual de faltas.
- Classificação de risco das disciplinas.
- Validação de alterações nos dados.

---

### Repository Layer

Responsável por:

- Comunicação com o banco de dados.
- Consultas.
- Inserções.
- Atualizações.
- Exclusões.

O Repository não possui regras de negócio, sendo responsável apenas pela persistência dos dados.

---

# 4. Organização por domínio

O projeto utiliza uma organização baseada em domínio (*feature-based architecture*).

Estrutura esperada:

```text
app/

├── disciplines/
│   ├── router.py
│   ├── service.py
│   ├── repository.py
│   ├── schemas.py
│   └── models.py
│
├── dashboard/
│   ├── service.py
│   └── schemas.py
│
├── core/
│   ├── database.py
│   └── config.py
│
└── main.py
```

A escolha dessa organização foi feita porque o sistema é estruturado por contextos de negócio, permitindo que todas as responsabilidades relacionadas a uma funcionalidade fiquem próximas.

Essa abordagem evita grandes pastas globais contendo arquivos separados apenas por tipo (`repositories`, `services`, `models`, etc.).

---

# 5. Modelo de dados

O sistema possui como principal entidade a disciplina.

## Discipline

Representa uma disciplina do semestre vigente.

| Campo | Tipo | Descrição |
|---|---|---|
| id | integer | Identificador único |
| name | string | Nome da disciplina |
| total_classes | integer | Quantidade total de aulas no semestre |
| absences | integer | Quantidade acumulada de faltas |

A quantidade de aulas foi escolhida como unidade principal do sistema, pois o acompanhamento de presença é realizado em número de aulas perdidas, e não em carga horária.

---

# 6. Fluxo de dados

Exemplo de atualização de faltas:

```text
Usuário
  |
  ↓
Frontend envia alteração (+1 ou -1)
  |
  ↓
API recebe solicitação
  |
  ↓
Service valida operação
  |
  ↓
Repository altera banco de dados
  |
  ↓
Resposta retorna ao frontend
```

---

# 7. Decisões arquiteturais

As decisões importantes do projeto são documentadas utilizando ADRs (*Architecture Decision Records*).

Localização:

```text
docs/
└── adr/
```

Exemplos de decisões documentadas:

- Motivo para não armazenar histórico acadêmico.
- Escolha do SQLite como banco local.
- Organização do Repository com métodos específicos.
- Separação entre regras de negócio e persistência.

---

# 8. Evolução da arquitetura

A arquitetura deve evoluir conforme as necessidades reais do projeto.

Novas funcionalidades devem ser adicionadas somente quando houver uma necessidade concreta, evitando complexidade antecipada (*overengineering*).

O objetivo é manter um sistema simples, organizado e fácil de evoluir.