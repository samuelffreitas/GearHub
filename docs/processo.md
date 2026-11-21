# Modelo de processo

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 22 de novembro de 2026

---

## 1. Modelo escolhido

**Iterativo e incremental.**

O desenvolvimento organiza-se em mini-ciclos, cada um com planeamento, análise, design, desenvolvimento e teste, produzindo uma versão parcial do sistema que funciona. O sistema cresce em incrementos e cada iteração melhora o que já existe, com base no que a anterior revelou.

Aplicado a este projeto, em duas iterações:

| Iteração | Quando | Natureza | O que produz |
|---|---|---|---|
| **1** | 4 de janeiro até à aula 11 | Predominantemente **incremental** | Versão 1: o ciclo requisição → levantamento → devolução a funcionar de ponta a ponta, com deteção de atraso e penalização |
| **2** | Da alteração de requisitos até 25 de janeiro | Predominantemente **iterativo** | Versão 2: o que existe é revisto e alterado para absorver a alteração de requisitos, com os testes de regressão a passar |


- A iteração 1 **acrescenta partes**.
- A iteração 2 **repete e melhora**.

O projeto precisa das duas, por isso o modelo é iterativo e incremental e não apenas um dos dois.

---

## 2. Porquê este modelo

A escolha depende de três fatores: a **estabilidade dos requisitos**, o **risco** e a **disponibilidade do cliente**.

### 2.1 Estabilidade dos requisitos: baixa

Os requisitos deste projeto **não são estáveis, e sabe-se antecipadamente que não o serão**, pois está previsto que uma alteração de requisitos seja entregue ao grupo em aula, no início da segunda metade da construção.

Um modelo que trate a especificação como fechada depois do arranque do código fica, por construção, em retrabalho quando essa alteração chegar. O modelo iterativo e incremental é adequado precisamente a ambientes em mudança, porque a alteração é absorvida pela iteração seguinte em vez de obrigar a reabrir uma fase já encerrada.

Parte dos requisitos só se conhece com precisão depois de haver software a funcionar: as fronteiras da regra de penalização, como o que acontece no dia do prazo ou a quem devolve com penalização ativa, são mais fáceis de fixar sobre um incremento executável do que sobre texto. Uma primeira versão serve para validar os requisitos do produto, e não apenas para os implementar.

### 2.2 Risco: concentrado na verificação do código gerado

O risco dominante não é o de requisitos nem o tecnológico de uma stack desconhecida, dado que a linguagem e a stack são livres e escolhidas entre as que o grupo domina. Está em o código ser produzido por uma ferramenta de IA e poder estar errado de formas que não são visíveis à leitura: transições de estado indevidamente permitidas, limites mal calculados, regressões ao regenerar ficheiros. É o que o registo de riscos classifica como R1, R3, R4 e R6.

O modelo iterativo e incremental responde a este perfil de risco de duas maneiras:

- Reduz o risco progressivamente e aumenta a qualidade a cada ciclo
- Dá feedback rápido

O modelo exige um cuidado: **sem atenção à arquitetura, a estrutura degrada-se a cada incremento**.

### 2.3 Disponibilidade do cliente: limitada

O modelo iterativo e incremental **exige um cliente disponível em cada ciclo** para dar feedback. Neste projeto não há um cliente contínuo, há um momento único e com data marcada em que entra informação nova de fora, a alteração de requisitos. Até lá, o grupo trabalha sobre uma especificação que produziu e validou a si mesmo.

O número de iterações é por isso **reduzido a duas**, com a fronteira entre elas no momento exato em que a informação externa chega.

### 2.4 Síntese

| Fator | Situação neste projeto | Implicação |
|---|---|---|
| Estabilidade dos requisitos | Baixa, com alteração garantida a meio da construção | Exclui modelos que fechem a especificação ao arranque do código |
| Risco | Alto e concentrado na verificação do código gerado por IA | Favorece ciclos curtos com verificação a fechar cada um |
| Disponibilidade do cliente | Limitada a um momento único e datado | Limita o número de iterações a duas, alinhadas com esse momento |

---

## 3. Alternativas consideradas

### 3.1 Cascata, e cascata revisto

**Porque foi considerada.** A cascata é adequada quando os requisitos são bem compreendidos e as alterações são limitadas, e em contextos que exigem documentação formal e rastreabilidade. 

**Porque foi rejeitada.** Pelo primeiro critério, que falha por completo. A desvantagem principal da cascata é a dificuldade em acomodar alterações depois de o processo arrancar, e é pouco adequada quando os requisitos mudam com frequência.

**E o cascata revisto?** A realimentação controlada resolveria em parte o problema das alterações, permitindo regressar a uma fase anterior. Mas mantém a estrutura sequencial: continua a haver uma única passagem pelas fases, sem versões parciais do sistema ao longo do caminho, sendo que o projeto exige duas fases de construção, cada uma a terminar com o sistema a funcionar.

### 3.2 Espiral

**Porque foi considerada.** É o modelo que coloca a gestão de riscos no centro, porque cada volta começa por planeamento e objetivos e passa imediatamente a avaliação de riscos, com mitigação proposta antes de desenvolver.

**Porque foi rejeitada.** Por duas desvantagens:

- É **pouco eficaz em projetos pequenos, por ter demasiada estrutura**. Com 3 a 5 casos de uso, o custo de uma análise de risco formal em cada volta consumiria o tempo que o projeto precisa de pôr na verificação do código.
- Exige gestão de riscos experiente e equipas com maturidade técnica e de gestão para análise de risco formal, o que não é o caso de um grupo que está a fazer isto pela primeira vez.

### 3.3 Modelos descartados sem análise longa

| Modelo | Porque não se aplica aqui |
|---|---|
| **Evolutivo exploratório** | Parte de uma especificação inicial resumida e evolui acrescentando o que o cliente propõe. Aqui a especificação tem de estar detalhada antes da construção, porque é ela o contexto que a ferramenta de IA recebe. O processo é também pouco visível e difícil de medir, incompatível com a rastreabilidade exigida. |
| **Prototipagem** | Serve para compreender requisitos mal compreendidos, começando pelo que não se sabe. Neste domínio o que o sistema faz está definido desde o início, e a dificuldade está em garantir que os estados, os atrasos e as penalizações estão corretos. O problema é de verificação, não de descoberta. |
| **RAD** | Dá prioridade à rapidez de entrega e exige utilizadores disponíveis e comprometidos, workshops e equipa experiente, condições que não existem. A pressa prejudica ainda a qualidade da documentação, que é aqui o produto avaliado. |

### 3.4 O que se retém dos métodos ágeis

O vocabulário do Scrum já está imposto pelo enunciado: a construção faz-se em dois sprints e o backlog é entregável do E1. Os **eventos** do Scrum, porém, não se transpõem — não há Daily Scrum num grupo de dois sem trabalho diário em comum, nem Sprint Review sem cliente para inspecionar o incremento, que é o mesmo obstáculo do fator 2.3. Retêm-se os três artefactos, que sobrevivem sem os eventos: o Product Backlog priorizado e o Product Goal, em [`backlog.md`](backlog.md), e a Definition of Done, em [`dod.md`](dod.md). Do XP retêm-se duas práticas técnicas, por responderem ao risco dominante deste projeto: os testes escritos antes do código, que é a resposta já registada ao risco R3, e o par humano–IA, em que a ferramenta escreve e um elemento do grupo revê e decide, que é a resposta a R1 e R4.

---

## 4. Como o modelo se concretiza

### 4.1 Antes da construção

As fases de especificação ocorrem uma vez e por ordem, e nenhuma produz código: visão e plano, depois requisitos com critérios de aceitação e rastreabilidade, depois arquitetura, diagramas e plano de testes. É o cuidado com a arquitetura que o modelo iterativo exige, feito antes do primeiro incremento em vez de durante.

### 4.2 Dentro de cada iteração

Cada iteração passa pelas cinco atividades do ciclo:

1. **Planeamento** — seleção das histórias do backlog que entram nesta iteração, por ordem de prioridade.
2. **Análise** — confirmação dos critérios de aceitação de cada história selecionada.
3. **Design** — verificação de que a história cabe na arquitetura e nos diagramas existentes; se não cabe, a arquitetura é revista antes de se gerar código.
4. **Desenvolvimento** — geração do código com a ferramenta de IA, tendo como contexto os requisitos, os diagramas e os casos de teste já escritos.
5. **Teste** — execução dos casos de teste desenhados antes do código. Uma história só está concluída quando passa.

### 4.3 Regras que atravessam todas as iterações

- Os casos de teste são desenhados a partir dos requisitos **antes** de existir código. Não se pede à ferramenta que decida o que testar.
- Todo o código entra por pull request revisto por outro elemento do grupo.
- Cada requisito mantém-se ligado ao elemento de design, ao código e ao teste que lhe correspondem. A ligação é atualizada no momento da alteração, não depois.
- O que a ferramenta produz e o grupo entrega é do grupo.

### 4.4 Transição entre iterações

A iteração 1 fecha com o sistema a funcionar e os seus testes a passar. A iteração 2 abre com a alteração de requisitos e a sua **análise de impacto feita antes de alterar qualquer código**: identifica-se que requisitos mudam, que elementos de design são afetados e que casos de teste deixam de ser válidos. Só depois se altera. Fecha com os testes de regressão a passar, demonstrando que o que funcionava antes continua a funcionar.

---

## 5. Limitações assumidas

Três limitações:

1. **Não há cliente disponível em cada ciclo**, ao contrário do que o modelo pressupõe. Mitigado por reduzir a duas iterações e alinhar a fronteira com a única entrada externa de requisitos.
2. **É difícil estimar o custo e o prazo total no início** de um processo iterativo. Aqui o prazo não é estimado, é fixo, dado pelo calendário. O que varia é o âmbito, e é por isso que o backlog está priorizado: se o tempo faltar, corta-se pela prioridade, não pela qualidade da verificação.
3. **A estrutura pode degradar-se entre incrementos.** Mitigado por fixar a arquitetura antes da construção e por rever, em cada história, se ela cabe no design existente antes de gerar código.
