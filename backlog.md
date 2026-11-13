# Product backlog inicial

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 13 de novembro de 2026

---

## 1. Como este backlog está organizado

O backlog aplica três das abordagens de gestão da complexidade:

- **Decomposição modular** — as histórias estão agrupadas por área funcional, não numa lista única: catálogo, requisição, movimento de equipamento, atrasos e penalizações, e estado do equipamento.
- **Priorização** — a ordem é dada pelo valor e pelo impacto de cada história, e não pela facilidade de a implementar. A coluna de justificação diz, para cada uma, porque está onde está.
- **Gestão de versões** — cada história tem um identificador estável. O identificador não é reatribuído nem reordenado: se a prioridade mudar, muda a posição, não o ID. É este identificador que acompanha a história até ao requisito, ao design, ao código e ao teste.

Cada história tem um estado de entrada e um estado de saída do equipamento declarados, quando aplicável. Esta é a regra que impede que um estado em falta só seja descoberto durante a construção.

---

## 2. Backlog

### Área funcional: Catálogo

| ID | História | Prior. | Valor e impacto |
|---|---|---|---|
| **HU-01** | Como requisitante, quero consultar os equipamentos e kits disponíveis, para saber o que posso pedir. | **1** | Sem leitura do estado nenhuma outra história é utilizável. É também a história que valida mais cedo, e ao menor custo, se a representação de estado do equipamento está correta. |
| **HU-12** | Como gestor do parque, quero criar e editar equipamentos e kits no catálogo, para o manter atualizado. | **11** | Resolve-se com dados de arranque fictícios durante toda a construção. Não participa no ciclo de empréstimo. |

### Área funcional: Requisição

| ID | História | Prior. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|
| **HU-02** | Como requisitante, quero submeter uma requisição de um equipamento, para reservar o seu uso. | **2** | Primeiro dos três verbos do domínio. Sem ela não há nada para levantar nem para devolver. | Disponível → Pedido pendente |
| **HU-03** | Como técnico de balcão, quero aprovar ou recusar uma requisição pendente, para controlar o que sai. | **3** | Separa "pedido" de "reserva confirmada". É esta transição que retira o equipamento de disponível e fecha a porta a duas requisições sobre o mesmo equipamento. | Pedido pendente → Reservado (ou → Disponível, se recusada) |
| **HU-10** | Como requisitante, quero consultar as minhas requisições e o seu estado, para saber o que tenho por devolver. | **9** | Valor real para o utilizador, mas é leitura sobre dados que já existem: não acrescenta nenhuma transição à entidade principal. | — |

### Área funcional: Movimento de equipamento

| ID | História | Prior. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|
| **HU-04** | Como técnico de balcão, quero registar o levantamento de um equipamento reservado, fixando o prazo de devolução. | **4** | Segundo verbo do domínio. Cria o prazo, que é o único dado de que depende todo o tratamento de atrasos: sem ele, as histórias HU-06 a HU-08 não têm sobre o que operar. | Reservado → Em empréstimo |
| **HU-05** | Como técnico de balcão, quero registar a devolução de um equipamento, para o devolver ao estado disponível. | **5** | Terceiro verbo do domínio. Fecha o ciclo e é o momento em que o atraso é apurado. | Em empréstimo ou Em atraso → Disponível |

### Área funcional: Atrasos e penalizações

| ID | História | Prior. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|
| **HU-06** | Como gestor do parque, quero que o sistema identifique as requisições cujo prazo de devolução já passou, para as ver como estando em atraso. | **6** | Primeira das três dificuldades declaradas do domínio. Sem esta história o sistema é apenas um registo de movimentos e não resolve o problema que motivou a sua construção. | Em empréstimo → Em atraso |
| **HU-07** | Como gestor do parque, quero que um atraso aplique automaticamente uma penalização ao requisitante, para que a consequência seja igual para todos. | **7** | Segunda dificuldade declarada. É a história com a regra mais sensível a valores-limite e, por isso, a que carrega o maior risco de erro de geração. | — |
| **HU-08** | Como requisitante, quero ser impedido de submeter nova requisição enquanto tiver penalização ativa, para que a penalização tenha efeito. | **8** | É o que torna HU-07 verificável por comportamento observável, e não apenas por um campo guardado em memória. Sem ela, a penalização existe mas não faz nada. | Bloqueia a transição Disponível → Pedido pendente |
| **HU-13** | Como gestor do parque, quero poder anular uma penalização, registando quem a anulou e porquê. | **12** | Resulta da mediação do conflito entre o técnico de balcão e o gestor do parque. É a compensação dada ao técnico, mas o sistema é coerente sem ela: enquanto não existir, a penalização é irreversível, limitação assumida. | — |

### Área funcional: Estado do equipamento

| ID | História | Prior. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|
| **HU-09** | Como técnico de balcão, quero marcar um equipamento como em manutenção ou indisponível, para o retirar de circulação. | **10** | Terceira dificuldade declarada do domínio. Fecha a máquina de estados do equipamento e cria as transições proibidas que dão origem aos testes negativos previstos para o risco R1. | Disponível → Em manutenção, e Em manutenção → Disponível |
| **HU-11** | Como gestor do parque, quero consultar o histórico de requisições de um equipamento, para perceber o seu uso. | **13** | Leitura sobre dados já existentes. Não participa no ciclo de empréstimo nem acrescenta transições. | — |

---

## 3. Histórias excluídas

Registadas para que não voltem a ser propostas, por um elemento do grupo ou por uma ferramenta de IA. A razão é, em todos os casos, a lista de exclusões da visão.

| ID | História | Razão da exclusão |
|---|---|---|
| **HX-01** | Como requisitante, quero ser avisado antes do prazo de devolução. | Integração com sistemas externos está fora do âmbito. |
| **HX-02** | Como requisitante, quero pagar a minha penalização. | Pagamentos reais estão fora do âmbito. |
| **HX-03** | Como requisitante, quero reservar equipamento com semanas de antecedência num calendário. | Reserva por calendário está fora do âmbito; é a dificuldade de outro domínio. |
| **HX-04** | Como técnico de balcão, quero aceitar a devolução de um kit incompleto. | O kit é tratado como unidade indivisível; a devolução parcial está fora do âmbito. |
| **HX-05** | Como gestor do parque, quero abrir ordens de reparação para equipamento avariado. | Manutenção como processo está fora do âmbito. |

---

## 4. Linha de corte

As histórias **HU-01 a HU-08**, por ordem de prioridade, constituem o núcleo que tem de funcionar de ponta a ponta. Cobrem os três verbos do domínio — requisição, levantamento e devolução — e as duas primeiras dificuldades declaradas, os atrasos e as penalizações.

**HU-09** é a primeira candidata a entrar acima da linha, porque é a única das restantes que fecha a terceira dificuldade do domínio e acrescenta transições à entidade principal.

**HU-10 a HU-13** são leitura ou funcionalidade de conveniência. Entram apenas se o âmbito o permitir, e a sua ausência não impede o sistema de resolver o problema descrito na visão.

Esta linha é a aplicação direta do princípio de priorização: tratar primeiro o que tem maior valor e impacto. Se o tempo faltar, corta-se a partir do fundo da lista, nunca na verificação das histórias que ficam.

---

## 5. Manutenção deste backlog

O backlog é revisto no planeamento de cada iteração. Uma história nova entra sempre no fim da sua área funcional e só sobe por decisão explícita e registada do grupo — é esta regra que protege o projeto do crescimento de âmbito.

Quando a alteração de requisitos chegar, as histórias afetadas são identificadas pelo seu ID antes de qualquer alteração de código, e o backlog é atualizado em conjunto com os requisitos e a rastreabilidade, não depois.
