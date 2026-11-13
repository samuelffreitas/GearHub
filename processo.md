# Modelo de processo

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 13 de novembro de 2026

---

## 1. Modelo escolhido

**Iterativo e incremental.**

O desenvolvimento organiza-se em mini-ciclos, cada um com planeamento, análise, design, desenvolvimento e teste, produzindo uma versão parcial do sistema que funciona. O sistema cresce em incrementos e cada iteração melhora o que já existe, com base no que a anterior revelou.

Aplicado a este projeto, em duas iterações:

| Iteração | Quando | Natureza | O que produz |
|---|---|---|---|
| **1** | 4 de janeiro até à aula 11 | Predominantemente **incremental** | Versão 1: o ciclo requisição → levantamento → devolução a funcionar de ponta a ponta, com deteção de atraso e penalização |
| **2** | Da alteração de requisitos até 25 de janeiro | Predominantemente **iterativo** | Versão 2: o que existe é revisto e alterado para absorver a alteração de requisitos, com os testes de regressão a passar |

A distinção entre as duas palavras é operativa aqui, não decorativa. A iteração 1 **acrescenta partes**: cada história entrega funcionalidade nova sobre o que já está feito. A iteração 2 **repete e melhora**: o mesmo trabalho é revisitado porque chega informação nova de fora. O projeto precisa das duas coisas, e é por isso que o modelo é o iterativo e incremental e não apenas um dos dois.

---

## 2. Porquê este modelo

A escolha de um modelo de processo depende de três fatores: a **estabilidade dos requisitos**, o **risco** e a **disponibilidade do cliente**. Não existe um modelo melhor em abstrato. O que segue é a avaliação deste projeto em cada um dos três.

### 2.1 Estabilidade dos requisitos: baixa, e por garantia

Este é o fator decisivo. Os requisitos deste projeto **não são estáveis, e sabe-se antecipadamente que não o serão**: está previsto que uma alteração de requisitos seja entregue ao grupo em aula, no início da segunda metade da construção. Não é uma hipótese de planeamento, é um facto do calendário.

Um modelo que trate a especificação como fechada depois do arranque do código fica, por construção, em retrabalho quando essa alteração chegar. O modelo iterativo e incremental é adequado precisamente a ambientes em mudança, porque a alteração é absorvida pela iteração seguinte em vez de obrigar a reabrir uma fase já encerrada.

Há um segundo aspeto da instabilidade, menos óbvio. Parte dos requisitos deste sistema só se conhece com precisão depois de haver software a funcionar: a regra de penalização tem fronteiras — o que acontece exatamente no dia do prazo, o que acontece a quem devolve com penalização ativa — que são mais fáceis de fixar sobre um incremento executável do que sobre texto. Uma primeira versão serve para validar os requisitos do produto, e não apenas para os implementar.

### 2.2 Risco: concentrado na verificação do código gerado

O risco dominante deste projeto não é o risco de requisitos, nem o risco tecnológico de uma stack desconhecida — a linguagem e a stack são livres e escolhem-se entre as que o grupo domina. O risco dominante está em o código ser produzido por uma ferramenta de IA e poder estar errado de formas que não são visíveis à leitura: transições de estado indevidamente permitidas, limites mal calculados, regressões ao regenerar ficheiros. É o que o registo de riscos classifica como R1, R3, R4 e R6, todos de nível alto.

O modelo iterativo e incremental responde a este perfil de risco de duas maneiras. Primeira, reduz o risco progressivamente e aumenta a qualidade a cada ciclo: cada iteração fecha com um conjunto de produtos finais verificados, de modo que o erro é encontrado sobre um incremento pequeno e localizável, em vez de sobre o sistema inteiro no fim. Segunda, o feedback é rápido: um defeito de geração detetado na iteração 1 muda a forma como a iteração 2 é especificada e como os prompts são escritos.

O contraponto honesto é o cuidado que o próprio modelo exige: **sem atenção à arquitetura, a estrutura degrada-se a cada incremento**. Neste projeto esse cuidado está satisfeito por via externa, porque a arquitetura é decidida, justificada e documentada antes de a construção começar, e não durante os incrementos.

### 2.3 Disponibilidade do cliente: limitada, e é aqui que o modelo precisa de ajuste

Este é o fator em que o modelo escolhido não assenta perfeitamente, e o documento diz isso em vez de o esconder.

O modelo iterativo e incremental **exige um cliente disponível em cada ciclo** para dar feedback. Neste projeto não há um cliente contínuo: há um momento único e com data marcada em que entra informação nova de fora — a alteração de requisitos. Entre esse momento e o arranque da construção, o grupo trabalha sobre uma especificação que produziu e validou a si mesmo.

A consequência prática é que o número de iterações é **deliberadamente reduzido a duas**, e a fronteira entre elas é posta exatamente no momento em que a informação externa chega. Em vez de muitas iterações curtas à espera de feedback que não existiria, o projeto tem duas iterações alinhadas com a única entrada real de feedback disponível. O que noutro contexto seria um defeito do plano é, aqui, o que o torna executável.

### 2.4 Síntese

| Fator | Situação neste projeto | Implicação |
|---|---|---|
| Estabilidade dos requisitos | Baixa, com alteração garantida a meio da construção | Exclui modelos que fechem a especificação ao arranque do código |
| Risco | Alto e concentrado na verificação do código gerado por IA | Favorece ciclos curtos com verificação a fechar cada um |
| Disponibilidade do cliente | Limitada a um momento único e datado | Limita o número de iterações a duas, alinhadas com esse momento |

---

## 3. Alternativas consideradas

### 3.1 Cascata, e cascata revisto

**Porque foi considerada.** A cascata é adequada quando os requisitos são bem compreendidos e as alterações são limitadas, e em contextos que exigem documentação formal e rastreabilidade. O segundo critério aplica-se a este projeto de forma evidente: há documentação obrigatória em cada fase e a rastreabilidade entre requisito, design, código e teste é um requisito do próprio projeto. Fases e entregáveis claros, fáceis de planear e controlar, descrevem bem o calendário que o projeto tem.

**Porque foi rejeitada.** Pelo primeiro critério, que falha por completo. A desvantagem principal da cascata é a dificuldade em acomodar alterações depois de o processo arrancar, e é pouco adequada quando os requisitos mudam com frequência. Neste projeto a alteração de requisitos não é um acidente a evitar: é uma entrega do calendário, com data. Adotar cascata seria escolher o modelo cuja fraqueza principal coincide exatamente com a característica garantida do projeto.

Acresce uma segunda razão. Na cascata, o cliente só vê software a funcionar no fim, e a integração e os testes de sistema são uma fase própria, depois da implementação. Neste projeto os testes são o critério de conclusão de cada funcionalidade — uma funcionalidade só está concluída quando passa nos testes desenhados a partir dos requisitos. A verificação não é uma fase terminal, é uma condição permanente.

**E o cascata revisto?** A realimentação controlada resolveria em parte o problema das alterações, permitindo regressar a uma fase anterior. Mas mantém a estrutura sequencial: continua a haver uma única passagem pelas fases, sem versões parciais do sistema ao longo do caminho. O projeto exige duas fases de construção, cada uma a terminar com o sistema a funcionar. Além disso, o próprio modelo alerta que, sem uma gestão de alterações bem definida, o projeto entra num ciclo sem fim de retornos — e um grupo de 2 a 4 pessoas, com quatro semanas de construção interrompidas por férias, não tem margem para esse ciclo.

### 3.2 Espiral

**Porque foi considerada.** É o modelo que coloca a gestão de riscos no centro: cada volta começa por planeamento e objetivos e passa imediatamente a avaliação de riscos, com mitigação proposta antes de desenvolver. Dado que o risco é, neste projeto, o fator mais pesado dos três — e que o registo de riscos tem cinco entradas de nível alto — a espiral era a candidata mais séria depois da escolhida.

**Porque foi rejeitada.** Por duas desvantagens que se aplicam diretamente. A primeira: a espiral é **pouco eficaz em projetos pequenos, por ter demasiada estrutura**. Este projeto é propositadamente pequeno, com 3 a 5 casos de uso, e o custo de uma análise de risco formal em cada volta consumiria tempo que o projeto precisa de pôr na verificação do código. A segunda: exige gestão de riscos experiente e equipas com maturidade técnica e de gestão para análise de risco formal, o que não é o caso de um grupo que está a fazer isto pela primeira vez.

O que se retém da espiral, sem adotar o modelo: a análise de risco deixa de ser um documento entregue uma vez e passa a ser revista no arranque de cada iteração, como está definido na secção 5 do registo de riscos.

### 3.3 Modelos descartados sem análise longa

| Modelo | Porque não se aplica aqui |
|---|---|
| **Evolutivo exploratório** | Parte de uma especificação inicial resumida e evolui acrescentando o que o cliente propõe. Aqui a especificação tem de estar detalhada antes da construção, porque é ela o contexto que a ferramenta de IA recebe. Acresce que o processo é pouco visível e difícil de medir, e que as mudanças sucessivas tendem a degradar a estrutura — incompatível com a rastreabilidade exigida. |
| **Prototipagem** | Serve para compreender requisitos mal compreendidos, começando pelo que não se sabe. Neste domínio o que o sistema faz está definido desde o início — requisição, levantamento e devolução — e a dificuldade não está em descobrir o que o utilizador quer, está em garantir que os estados, os atrasos e as penalizações estão corretos. O problema é de verificação, não de descoberta. |
| **RAD** | Dá prioridade à rapidez de entrega e exige utilizadores disponíveis e comprometidos, workshops e equipa experiente. Nenhuma dessas condições existe. E a desvantagem central — a pressa prejudicar a qualidade e a documentação — colide com o facto de a documentação ser, aqui, o produto avaliado. |

---

## 4. Como o modelo se concretiza

### 4.1 Antes da construção

As fases de especificação ocorrem uma vez e por ordem, e nenhuma produz código: visão e plano, depois requisitos com critérios de aceitação e rastreabilidade, depois arquitetura, diagramas e plano de testes. Isto não contradiz a escolha do modelo — é o cuidado com a arquitetura que o modelo iterativo exige para que a estrutura não se degrade a cada incremento, feito antes do primeiro incremento em vez de durante.

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

Três, registadas por escrito para que não sejam descobertas como surpresa:

1. **Não há cliente disponível em cada ciclo**, ao contrário do que o modelo pressupõe. Mitigado por reduzir a duas iterações e alinhar a fronteira com a única entrada externa de requisitos.
2. **É difícil estimar o custo e o prazo total no início** de um processo iterativo. Neste caso o problema não se põe da forma habitual, porque o prazo não é estimado: é fixo, dado pelo calendário. O que varia é o âmbito, e é por isso que o backlog está priorizado — se o tempo faltar, corta-se pela prioridade, não pela qualidade da verificação.
3. **A estrutura pode degradar-se entre incrementos.** Mitigado por fixar a arquitetura antes da construção e por rever, em cada história, se ela cabe no design existente antes de gerar código.
