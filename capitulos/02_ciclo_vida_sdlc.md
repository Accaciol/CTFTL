# 📚 Capítulo 2: Testes ao Longo do Ciclo de Vida (SDLC) (Syllabus CTFL v4.0)

Este capítulo aborda como as atividades de teste se integram aos diferentes modelos de desenvolvimento (Sequenciais, Iterativos/Ágeis e DevOps), detalhando os **Níveis de Teste**, **Tipos de Teste** e modelos conceituais modernos como a **Pirâmide de Testes** e os **Quadrantes de Teste**.

---

## 1. Testes no Contexto do SDLC

Para cada atividade de desenvolvimento de software, deve haver uma atividade de teste correspondente. A forma como os testes são organizados varia de acordo com o modelo de SDLC adotado.

### 1.1 Modelos Sequenciais vs. Iterativos/Ágeis
* **Modelos Sequenciais (Ex.: Modelo V, Cascata)**:
  * Desenvolvimento em fases bem definidas e cascateadas.
  * Testes dinâmicos ocorrem principalmente em fases posteriores.
  * O **Modelo V** associa diretamente cada fase de desenvolvimento ao seu nível de teste correspondente (ex.: Requisitos de Usuário $\leftrightarrow$ Teste de Aceite; Código $\leftrightarrow$ Teste de Componente).
* **Modelos Iterativos/Ágeis (Ex.: Scrum, Kanban)**:
  * O software é construído em pequenas iterações (Sprints de 1 a 4 semanas).
  * As atividades de teste são contínuas e integradas diariamente à equipe (*Whole-Team Approach*).
  * Ênfase em **Automação de Testes de Regressão** e integração contínua (CI/CD).

### 1.2 DevOps, CI/CD e Shift-Left / Shift-Right
* **CI/CD (Integração e Entrega Contínuas)**: Permite que testes automatizados sejam executados a cada *commit* ou *pull request*, fornecendo feedback imediato aos desenvolvedores.
* **Shift-Left**: Antecipa testes para as fases de requisitos e arquitetura.
* **Shift-Right**: Estende as práticas de qualidade para o ambiente de **Produção** (ex.: testes A/B, monitoramento de saúde do sistema, engenharias de caos e testes de observabilidade).

---

## 2. Modelos Conceituais de Teste (CTFL 4.0)

### 2.1 Pirâmide de Testes (*Test Pyramid*)
A Pirâmide de Testes visualiza a proporção ideal de diferentes níveis de testes automatizados:

```mermaid
pyramid
  top: Testes de UI / E2E (Poucos, mais lentos, custo alto)
  middle: Testes de Integração / API (Quantidade moderada)
  base: Testes de Componente / Unitários (Muitos, rápidos, baixo custo)
```

* **Base (Testes Unitários/Componente)**: Maior volume de testes. Execução ultrarrápida, alta isolamento e baixo custo de manutenção.
* **Meio (Testes de Integração/Serviços/API)**: Valida a comunicação entre módulos ou serviços.
* **Topo (Testes End-to-End / UI)**: Menor quantidade de testes. Valida fluxos completos de negócio, porém são mais lentos e sujeitos a instabilidades (*flaky tests*).

### 2.2 Quadrantes de Teste (*Testing Quadrants*)
Propostos por Brian Marick, os 4 Quadrantes ajudam a organizar os tipos de teste segundo o **foco** (Apoio à Equipe vs. Critica ao Produto) e a **perspectiva** (Negócio vs. Tecnologia):

| | **Apoio à Equipe (Guiam o Dev)** | **Crítica ao Produto (Avaliam o Produto)** |
| :--- | :--- | :--- |
| **Guiados pelo Negócio** | **Q2**: Histórias de Usuário, Protótipos, Exemplos, ATDD/BDD. | **Q3**: Teste de Aceite do Usuário (UAT), Usabilidade, Testes Exploratórios. |
| **Guiados pela Tecnologia** | **Q1**: Testes Unitários, Testes de Componente, TDD, Análise Estática. | **Q4**: Testes Não-Funcionais (Desempenho, Carga, Segurança, Confiabilidade). |

---

## 3. Níveis de Teste

Um Nível de Teste é um conjunto de atividades de teste gerenciadas e executadas como um grupo. No Syllabus v4.0, destacam-se:

### 3.1 Teste de Componente (Unitário)
* **Foco**: Módulos individuais, classes, funções ou métodos isolados.
* **Base de Teste**: Código-fonte, design detalhado, modelos de dados.
* **Objetivo**: Reduzir risco de erros lógicos nos blocos básicos de código.
* **Responsável**: Desenvolvedores (frequentemente usando TDD - *Test-Driven Development*).

### 3.2 Teste de Integração
* **Foco**: Interações e interfaces entre componentes ou sistemas.
* **Tipos**:
  * **Integração de Componentes**: Valida a comunicação entre módulos internos.
  * **Integração de Sistemas**: Valida a comunicação entre sistemas heterogêneos, APIs REST, microserviços e bancos de dados externos.
* **Objetivo**: Detectar defeitos nas interfaces e protocolos de troca de dados.

### 3.3 Teste de Sistema
* **Foco**: O comportamento do produto de software completo e integrado como um todo.
* **Base de Teste**: Especificações de requisitos de sistema, casos de uso, arquitetura de software.
* **Objetivo**: Verificar o cumprimento dos requisitos funcionais e não-funcionais globais em ambiente similar ao de produção.

### 3.4 Teste de Aceite
* **Foco**: Avaliar se o sistema está pronto para implantação e se atende às necessidades de negócio.
* **Subtipos**:
  * **Teste de Aceite do Usuário (UAT)**: Realizado por usuários finais para validar requisitos de negócio.
  * **Teste de Aceite Operacional (OAT)**: Realizado por administradores de sistemas/DevOps (focado em backup/restauração, recuperação de desastres, instalação, segurança).
  * **Teste de Aceite Contratual e Regulatório**: Valida conformidade com normas legais ou cláusulas contratuais.
  * **Testes Alfa e Beta**: Alfa (na organização por usuários/clientes) e Beta (em ambiente externo por clientes reais).

---

## 4. Tipos de Testes

### 4.1 Testes Funcionais
* Avaliam **o que** o software faz. Baseados em requisitos funcionais e regras de negócio.
* Aplicáveis a todos os níveis de teste.

### 4.2 Testes Não-Funcionais
* Avaliam **como** o software se comporta (qualidade de serviço).
* Incluem: Desempenho, Carga, Estresse, Segurança, Usabilidade, Acessibilidade, Portabilidade e Mantibilidade.

### 4.3 Testes de Caixa-Branca (*White-Box*)
* Baseiam-se na estrutura interna do código, arquitetura ou fluxo de controle.
* Medidos por métricas de cobertura (instruções/sentenças e decisões/ramos).

### 4.4 Teste de Confirmação (Re-teste) vs. Teste de Regressão
* **Teste de Confirmação (Re-teste)**: Executado para verificar se um defeito específico reportado anteriormente foi corrigido com sucesso.
* **Teste de Regressão**: Executado em partes **não alteradas** do sistema para garantir que modificações, melhorias ou correções recentes não introduziram novos defeitos secundários.

---

## 5. Teste de Manutenção

O teste de manutenção é realizado em sistemas existentes em produção quando ocorrem mudanças.

### Gatilhos para Testes de Manutenção
1. **Modificações**: Correções de bugs, melhorias funcionais, patches de segurança.
2. **Migração**: Mudança de plataforma, banco de dados, sistema operacional ou infraestrutura de nuvem.
3. **Aposentadoria (Desativação)**: Retirada de circulação de um sistema ou arquivamento de dados históricos.

* **Análise de Impacto**: Avaliação necessária para identificar quais partes do sistema podem ser afetadas por uma mudança e determinar o escopo dos testes de regressão necessários.
