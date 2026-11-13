# Registo de riscos

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 13 de novembro de 2026

Um risco é um acontecimento incerto que, se ocorrer, tem efeito negativo no projeto ou no produto. Distingue-se de um problema: o problema já aconteceu, o risco ainda pode ser evitado.

---

## 1. Escalas usadas

**Probabilidade:** baixa · média · alta
**Impacto:** insignificante · moderado · catastrófico

O **nível** não é atribuído por opinião: é derivado da matriz probabilidade × impacto.

|  | Impacto insignificante | Impacto moderado | Impacto catastrófico |
|---|---|---|---|
| **Prob. alta** | Média | Alta | Alta |
| **Prob. média** | Baixa | Média | Alta |
| **Prob. baixa** | Baixa | Baixa | Média |

**Respostas possíveis:** evitar (mudar o plano para eliminar o risco) · mitigar (reduzir a probabilidade ou o impacto) · transferir (passar o impacto a terceiros) · aceitar (assumir o risco com plano de contingência).

Os riscos de nível **alto** têm obrigatoriamente plano de mitigação detalhado na secção 3. Os de nível baixo são apenas monitorizados.

---

## 2. Registo

> Nota: os nomes indicados na coluna **Dono** representam papéis fictícios atribuídos dentro da equipa de projeto para efeitos de rastreabilidade documental.

| ID | Risco | Tipo | Prob. | Imp. | Nível | Resposta | Dono |
|---|---|---|---|---|---|---|---|
| **R1** | O código gerado pela IA aceita transições de estado impossíveis: devolver equipamento que nunca foi levantado, levantar equipamento em manutenção, requisitar equipamento já emprestado | Tecnológico | Alta | Catastrófico | **Alta** | Mitigar: diagrama de estados dado à IA como contexto, com as transições proibidas escritas; um teste negativo por cada transição proibida | Diogo Martins |
| **R2** | A IA propõe requisitos ambíguos ("validação rápida", "fácil de usar") ou fora do âmbito (notificações, pagamento da multa, reserva por calendário) e esse texto entra no documento de requisitos sem revisão | Requisitos ambíguos | Alta | Moderado | **Alta** | Mitigar: nenhum requisito proposto pela IA entra sem reescrita por um elemento do grupo; cada rejeição é registada com a razão | Sofia Carvalho |
| **R3** | Testes pedidos à IA a partir do código já gerado confirmam o comportamento implementado, defeitos incluídos — um erro de limite na regra de atraso passa porque o teste copia o limite errado | Tecnológico | Média | Catastrófico | **Alta** | Evitar: os casos de teste são desenhados pelo grupo a partir dos requisitos, antes de existir código; a IA traduz esses casos para código de teste, não os define | Diogo Martins |
| **R4** | Regenerar um ficheiro para corrigir um defeito faz a IA reescrever código vizinho que já passava, introduzindo regressões silenciosas no cálculo de penalização, que toca na devolução e na requisição seguinte | Tecnológico | Média | Moderado | **Média** | Mitigar: toda a alteração entra por pull request revisto por outro elemento, com o diff lido; a suite completa corre antes de integrar | Diogo Martins |
| **R5** | Os parâmetros da regra de atraso e penalização chegam à construção por decidir, e a IA preenche-os por omissão com valores plausíveis mas arbitrários | Requisitos ambíguos | Alta | Catastrófico | **Alta** | Evitar: os seis parâmetros da secção 4 são fixados com o cliente antes de qualquer geração de código, cada um com critério de aceitação e casos de teste de valor-limite | Sofia Carvalho |
| **R6** | A máquina de estados do equipamento é revista a meio da construção, por aparecer um estado não previsto, e obriga a refazer requisição, levantamento e devolução ao mesmo tempo | Mudança de requisitos | Média | Catastrófico | **Alta** | Mitigar: estados e transições fechados antes da construção; nenhuma história é dada como concluída sem declarar em que estado deixa o equipamento | Sofia Carvalho |
| **R7** | O conflito entre o técnico de balcão, que quer discricionariedade no atendimento, e o gestor do parque, que quer a regra sem exceções, bloqueia a especificação da penalização | Conflito de stakeholders | Média | Moderado | **Média** | Mitigar: decisão de mediação já registada em `stakeholders.md` secção 5, com a limitação assumida por escrito; a equipa age como mediadora e a decisão não é reaberta sem novo registo | Sofia Carvalho |
| **R8** | A ferramenta de IA usada fica indisponível ou esgota o limite de utilização a meio de um sprint | Dependência externa | Média | Insignificante | **Baixa** | Aceitar: contingência é a segunda ferramenta já identificada no README; a troca custa tempo de adaptação, não trabalho perdido, porque a especificação é independente da ferramenta | Diogo Martins |

Oito riscos, dos quais **quatro (R1 a R4) ligados ao uso de IA**.

### Distribuição na matriz

|  | Impacto insignificante | Impacto moderado | Impacto catastrófico |
|---|---|---|---|
| **Prob. alta** | — | R2 | R1, R5 |
| **Prob. média** | R8 | R4, R7 | R3, R6 |
| **Prob. baixa** | — | — | — |

---

## 3. Planeamento da mitigação dos riscos de nível alto

### R1 · Transições de estado impossíveis

A causa é conhecida: um prompt que descreve o caminho normal deixa a IA preencher o resto por omissão, e o que ela preenche é permissivo. A ação preventiva tem três partes. Primeira, o conjunto de estados do equipamento e as transições legítimas entre eles ficam escritos antes de se gerar código, e a lista das transições **proibidas** é escrita de forma igualmente explícita — é esta segunda lista que costuma faltar. Segunda, ambas as listas são dadas à ferramenta como contexto, não resumidas. Terceira, existe um caso de teste negativo por cada transição proibida, desenhado pelo grupo. O plano de contingência, se a transição indevida for detetada já em execução, é bloquear a operação na camada de validação de estado antes de corrigir o resto.

### R2 · Requisitos ambíguos ou fora do âmbito propostos pela IA

A ação preventiva é processual: nenhum texto de requisito produzido por uma ferramenta é aceite como está. Cada proposta é confrontada com duas perguntas — é verificável por um teste? está dentro da lista de exclusões da visão? — e o resultado da confrontação é registado, tanto nas aceitações como nas rejeições. A secção 3 de `visao.md` é o critério de corte do âmbito e é consultada explicitamente em cada decisão.

### R3 · Testes que confirmam o defeito

Este risco é **evitado**, não mitigado: a ordem de trabalho é alterada para o eliminar. Os casos de teste são derivados dos requisitos por partições de equivalência e valores-limite, e ficam escritos antes de existir código para testar. A IA pode traduzir um caso de teste já desenhado para a sintaxe da ferramenta de teste; não lhe é pedido que decida o que testar nem que valores usar nos limites.

### R5 · Parâmetros da regra por decidir

Também **evitado**: os parâmetros são fixados junto do cliente antes de haver código que os possa assumir por omissão. A lista fechada está na secção 4 e nenhum item dela fica em aberto à entrada da construção. Cada parâmetro, ao ser decidido, gera imediatamente três casos de teste — véspera do limite, no limite, dia seguinte ao limite.

### R6 · Revisão tardia da máquina de estados

A ação preventiva é antecipar o fecho: estados e transições são decididos no documento de requisitos e desenhados antes da construção, não durante. A ação de controlo é a regra de que nenhuma história fecha sem declarar o estado de entrada e o estado de saída do equipamento, o que torna visível qualquer estado em falta no momento em que a história é escrita, e não três sprints depois. O plano de contingência, caso apareça mesmo um estado novo, é tratá-lo como alteração de requisitos com análise de impacto, e não como correção local.

---

## 4. Parâmetros a fixar (mitigação de R5)

Estes seis valores não estão decididos neste documento de visão, pois dependem da definição operacional a ser indicada pelo cliente (Gestor do parque de equipamentos / Direção dos serviços) na fase de levantamento e especificação de requisitos. Enquanto estiverem abertos constituem risco registado, pelo que nenhum chega à fase de construção sem estar formalmente fixado.

| Parâmetro | O que falta decidir com o cliente |
|---|---|
| Duração do empréstimo | Número de dias, e se são de calendário ou úteis |
| Início do atraso | Se o equipamento fica em atraso no fim do dia do prazo ou no início do dia seguinte |
| Unidade da penalização | Dias de bloqueio por dia de atraso, ou valor fixo por ocorrência |
| Duração do bloqueio | Como se calcula e quando termina |
| Requisições simultâneas | Quantas requisições em aberto um requisitante pode ter |
| Atomicidade do kit | Confirmação de que o kit é devolvido obrigatoriamente completo |

---

## 5. Monitorização

O registo é revisto no início de cada entrega e no arranque de cada iteração. Em cada revisão verifica-se, para cada risco: se a probabilidade ou o impacto mudaram, se a resposta planeada foi executada, e se o risco se concretizou.

Um risco que se concretize deixa de ser risco e passa a problema: sai deste registo para o registo de defeitos, com a indicação do ID de origem, o que permite depois verificar quais dos riscos antecipados aqui aconteceram de facto e quais não.

Riscos novos podem ser acrescentados em qualquer revisão. Nenhum risco é removido: se deixar de ser relevante, fica registado como encerrado, com a razão.
