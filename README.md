# Academic Tracker

Sistema pessoal de gerenciamento acadêmico focado no acompanhamento de presença e faltas durante o semestre.

O objetivo do projeto é fornecer uma visão simples e objetiva da situação acadêmica atual, permitindo acompanhar o risco de reprovação por faltas e tomar decisões com base nos dados atuais das disciplinas.

## ✨ Objetivo

O Academic Tracker nasceu de uma necessidade real: acompanhar a quantidade de faltas acumuladas nas disciplinas e entender rapidamente quais matérias possuem maior risco.

O sistema não tem como objetivo substituir sistemas acadêmicos institucionais ou armazenar um histórico completo da vida acadêmica. Ele funciona como um painel pessoal de acompanhamento do semestre vigente.

## 🎯 Funcionalidades

* Cadastro de disciplinas atuais
* Controle da quantidade de faltas por disciplina
* Atualização de faltas com incremento e decremento
* Alteração de informações das disciplinas
* Exclusão de disciplinas
* Visualização das disciplinas ordenadas por risco
* Estatísticas gerais do semestre:

  * Total de aulas
  * Total de faltas
  * Percentual geral de faltas

## 🏗️ Arquitetura

O projeto segue uma arquitetura organizada por domínio, separando responsabilidades entre as camadas da aplicação.

Estrutura conceitual:

```
Frontend
    |
    ↓
API
    |
    ↓
Service
    |
    ↓
Repository
    |
    ↓
Banco de dados
```

### Responsabilidades

**Repository**

* Responsável pela comunicação com o banco de dados.
* Executa consultas e alterações nos dados.
* Não possui regras de negócio.

**Service**

* Responsável pelas regras da aplicação.
* Realiza validações.
* Calcula informações derivadas, como percentual de faltas e nível de risco.

**API**

* Responsável pela comunicação entre frontend e backend.
* Expõe as funcionalidades do sistema.

## 🗄️ Modelo de dados

A versão inicial utiliza uma estrutura simples, contendo apenas os dados necessários para o objetivo do sistema.

### Disciplines

| Campo         | Descrição                             |
| ------------- | ------------------------------------- |
| id            | Identificador da disciplina           |
| name          | Nome da disciplina                    |
| total_classes | Quantidade total de aulas no semestre |
| absences      | Quantidade acumulada de faltas        |

A escolha de armazenar a quantidade de aulas, em vez da carga horária em horas, foi feita porque a unidade utilizada no controle diário de presença é a quantidade de aulas perdidas.

## 📐 Decisões de arquitetura

Algumas decisões importantes do projeto:

* O sistema não mantém histórico de disciplinas concluídas.
* Apenas disciplinas do semestre vigente são armazenadas.
* Dados derivados não são persistidos, sendo calculados quando necessários.
* O controle é baseado em quantidade de aulas, não em carga horária.

## 🚧 Status do projeto

Em desenvolvimento.

## 🔮 Possíveis evoluções

Funcionalidades que podem ser adicionadas futuramente:

* Calendário acadêmico
* Controle de avaliações e notas
* Registro de atividades pendentes
* Alertas de risco
* Dashboard mais detalhado

Essas funcionalidades serão avaliadas conforme a necessidade real do projeto, evitando adicionar complexidade sem benefício prático.
