# 📚 Capítulo 4: Análise e Modelagem de Testes (Syllabus CTFL v4.0)

Este capítulo apresenta as técnicas de teste utilizadas para derivar condições de teste, casos de teste e dados de teste. No Syllabus CTFL 4.0, as técnicas são classificadas em quatro categorias: **Caixa-Preta**, **Caixa-Branca**, **Baseadas na Experiência** e **Baseadas na Colaboração**.

---

## 1. Categorias de Técnicas de Teste

| Categoria | Base Principal | Foco / Abordagem |
| :--- | :--- | :--- |
| **Caixa-Preta (Baseadas na Especificação)** | Requisitos, especificações, estórias de usuário, modelos. | Analisa entradas e saídas sem conhecimento da estrutura interna do código. |
| **Caixa-Branca (Baseadas na Estrutura)** | Código-fonte, arquitetura, fluxo de controle. | Examina a estrutura interna e o fluxo lógico do software. |
| **Baseadas na Experiência** | Conhecimento prévio, intuição e experiência do testador. | Identifica falhas com base em histórico de erros e comportamento humano. |
| **Baseadas na Colaboração** | Comunicação e alinhamento entre o time de desenvolvimento, PO e testador. | Deriva testes a partir de critérios de aceite e estórias de usuário em conjunto. |

---

## 2. Técnicas de Caixa-Preta (*Black-Box*)

### 2.1 Partição de Equivalência (PE - *Equivalence Partitioning*)
Divide os dados de entrada/saída em grupos (partições) que se espera que sejam processados da mesma forma pelo sistema.
* **Partição Válida**: Contém valores aceitos pelo sistema.
* **Partição Inválida**: Contém valores rejeitados pelo sistema.
* **Regra**: Testa-se ao menos **um valor representativo** de cada partição para atingir 100% de Cobertura de PE.

$$\text{Cobertura de PE} = \frac{\text{Número de partições exercitadas}}{\text{Número total de partições identificadas}} \times 100\%$$

---

### 2.2 Análise de Valor Limite (AVL - *Boundary Value Analysis*)
Foca nos limites (fronteiras) das partições de equivalência, onde estatisticamente ocorre a maior concentração de defeitos.

* **AVL de 2 Valores (Padrão)**:
  * Para cada limite, testa-se o próprio **valor de fronteira** e seu **vizinho mais próximo fora da partição**.
  * *Exemplo*: Um campo aceita valores inteiros de $18$ a $60$.
    * Limite Inferior ($18$): Testa-se $18$ (válido) e $17$ (inválido).
    * Limite Superior ($60$): Testa-se $60$ (válido) e $61$ (inválido).
    * **Valores testados**: $\{17, 18, 60, 61\}$.

* **AVL de 3 Valores**:
  * Para cada limite, testa-se o **valor de fronteira**, o **vizinho imediatamente abaixo** e o **vizinho imediatamente acima**.
  * *Exemplo* ($18$ a $60$):
    * Limite Inferior ($18$): $17, 18, 19$.
    * Limite Superior ($60$): $59, 60, 61$.
    * **Valores testados**: $\{17, 18, 19, 59, 60, 61\}$.

---

### 2.3 Tabela de Decisão (*Decision Table Testing*)
Técnica ideal para analisar combinações complexas de condições lógicas (regras de negócio).
* Se houver $N$ condições binárias (Verdadeiro/Falso), a tabela completa possuirá $2^N$ colunas de regras.

| Componente | Descrição |
| :--- | :--- |
| **Condições** | Entradas ou estados do sistema (V / F). |
| **Ações** | Saídas esperadas ou operações a serem executadas. |
| **Regras** | Cada coluna representa uma combinação única de condições e suas ações resultantes. |

---

### 2.4 Teste de Transição de Estados (*State Transition Testing*)
Utilizado quando o comportamento do sistema depende do seu estado atual e de eventos históricos.
* **Elementos**: Estados, Eventos (gatilhos), Ações e Transições.
* **Cobertura de 1-Switch (Transição Única)**: Garante que todas as transições diretas válidas e inválidas entre estados sejam testadas.

---

## 3. Técnicas de Caixa-Branca (*White-Box*)

As técnicas de caixa-branca medem a extensão em que a estrutura do código foi exercitada pela suíte de teste.

### 3.1 Cobertura de Instruções / Sentenças (*Statement Coverage*)
Mede a porcentagem de instruções executáveis exercitadas pelos testes:

$$\text{Cobertura de Sentença} = \frac{\text{Número de instruções executadas}}{\text{Número total de instruções executáveis}} \times 100\%$$

---

### 3.2 Cobertura de Decisões / Ramos (*Decision / Branch Coverage*)
Mede a porcentagem de ramificações de decisão (saídas Verdadeiro e Falso) exercitadas pelos testes:

$$\text{Cobertura de Decisão} = \frac{\text{Número de resultados de decisão exercitados}}{\text{Número total de resultados de decisão possíveis}} \times 100\%$$

---

### 3.3 Relação Fundamental entre Sentença e Decisão

> [!IMPORTANT]
> **100% de Cobertura de Decisão GARANTE 100% de Cobertura de Sentença.**
> O inverso **NÃO** é verdadeiro! Uma suíte que atinge 100% de Sentença pode não cobrir ramificações falsas de blocos `if` sem `else`.

---

## 4. Técnicas Baseadas na Experiência

1. **Suposição de Erro (*Error Guessing*)**: O testador antecipa erros humanos comuns e defeitos com base no seu conhecimento técnico acumulado e histórico de falhas passadas.
2. **Teste Exploratório (*Exploratory Testing*)**: Teste dinâmico onde o projeto, execução e aprendizado ocorrem simultaneamente. É estruturado através de **Cartas de Teste (*Test Charters*)** com limites de tempo definidos (*timeboxing*).
3. **Teste Baseado em Checklists**: Testes executados consultando uma lista consolidada de verificações genéricas ou específicas de domínio.

---

## 5. Técnicas Baseadas na Colaboração (CTFL 4.0)

Em equipes ágeis, a modelagem de teste ocorre via colaboração direta:

### 5.1 Histórias de Usuário e Critérios de Aceite
* **Critério INVEST**: Uma História de Usuário deve ser **I**ndependente, **N**egociável, **V**aliosa, **E**stimável, **S**mall (Pequena) e **T**estável.
* **Critérios de Aceite**: Definem as condições que a estória deve satisfazer para ser aceita pelo Product Owner (frequentemente escritos no formato BDD: *Given / When / Then*).

### 5.2 Desenvolvimento Guiado por Testes de Aceite (ATDD)
Técnica colaborativa onde a equipe (Três Amigos: Dev, Tester, PO) escreve os casos de teste de aceite **antes** que o código seja desenvolvido, garantindo um entendimento compartilhado dos requisitos.
