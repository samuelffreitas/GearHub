# Product backlog inicial

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 22 de novembro de 2026

---

## 1. Product Goal

Dar a cada equipamento um estado único e fiável, obrigar o ciclo de requisição, levantamento e devolução a passar por esse estado, detetar os atrasos a partir do prazo registado no levantamento e aplicar a penalização segundo uma regra igual para todos.

---

## 2. Como este backlog está organizado

O backlog aplica três das abordagens de gestão da complexidade:

- **Decomposição modular** — as histórias estão agrupadas por área funcional, não numa lista única.
- **Priorização** — a prioridade é dada em MoSCoW, pelo valor e pelo impacto de cada história, e não pela facilidade de a implementar.
- **Gestão de versões** — cada história tem um identificador estável. Se a prioridade mudar, muda a classificação, não o identificador. É ele que acompanha a história até ao requisito, ao design, ao código e ao teste.

Cada história tem um estado de entrada e um estado de saída do equipamento declarados, quando aplicável.

**MoSCoW:** Must (tem de ter) · Should (devia ter) · Could (podia ter) · Won't (não desta vez).
**Tamanho:** P, M ou G, por comparação entre histórias.

---

## 3. Backlog

### Área funcional: Catálogo

| ID | História | Prior. | Tam. | Crit. | Valor e impacto |
|---|---|---|---|---|---|
| **HU-01** | Como requisitante, quero consultar os equipamentos e kits disponíveis, para saber o que posso pedir. | **Must** | P | 3 ✓ | Sem leitura do estado nenhuma outra história é utilizável. Valida também, ao menor custo, se a representação de estado está correta. |
| **HU-12** | Como gestor do parque, quero criar e editar equipamentos e kits no catálogo, para o manter atualizado. | Could | M | — | Resolve-se com dados de arranque fictícios durante toda a construção. Não participa no ciclo de empréstimo. |

### Área funcional: Requisição

| ID | História | Prior. | Tam. | Crit. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|---|---|
| **HU-02** | Como requisitante, quero submeter uma requisição de um equipamento, para reservar o seu uso. | **Must** | M | 3 ✓ | Primeiro dos três verbos do domínio. Sem ela não há nada para levantar nem para devolver. | Disponível → Pedido pendente |
| **HU-03** | Como técnico de balcão, quero aprovar ou recusar uma requisição pendente, para controlar o que sai. | **Must** | M | 3 ✓ | É a transição que retira o equipamento de disponível e impede duas requisições sobre o mesmo equipamento. | Pedido pendente → Reservado (ou → Disponível, se recusada) |
| **HU-10** | Como requisitante, quero consultar as minhas requisições e o seu estado, para saber o que tenho por devolver. | Could | P | — | Leitura sobre dados que já existem: não acrescenta nenhuma transição à entidade principal. | — |

### Área funcional: Movimento de equipamento

| ID | História | Prior. | Tam. | Crit. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|---|---|
| **HU-04** | Como técnico de balcão, quero registar o levantamento de um equipamento reservado, fixando o prazo de devolução. | **Must** | M | — | Segundo verbo do domínio. Cria o prazo, de que depende todo o tratamento de atrasos: sem ele, as histórias HU-06 a HU-08 não têm sobre o que operar. | Reservado → Em empréstimo |
| **HU-05** | Como técnico de balcão, quero registar a devolução de um equipamento, para o devolver ao estado disponível. | **Must** | M | — | Terceiro verbo do domínio. Fecha o ciclo e é o momento em que o atraso é apurado. | Em empréstimo ou Em atraso → Disponível |

### Área funcional: Atrasos e penalizações

| ID | História | Prior. | Tam. | Crit. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|---|---|
| **HU-06** | Como gestor do parque, quero que o sistema identifique as requisições cujo prazo de devolução já passou, para as ver como estando em atraso. | **Must** | M | — | Primeira das três dificuldades declaradas do domínio. Sem ela o sistema é apenas um registo de movimentos. | Em empréstimo → Em atraso |
| **HU-07** | Como gestor do parque, quero que um atraso aplique automaticamente uma penalização ao requisitante, para que a consequência seja igual para todos. | **Must** | M | — | Segunda dificuldade declarada. É a história com a regra mais sensível a valores-limite e a que carrega maior risco de erro de geração. | — |
| **HU-08** | Como requisitante, quero ser impedido de submeter nova requisição enquanto tiver penalização ativa, para que a penalização tenha efeito. | **Must** | P | — | Torna HU-07 verificável por comportamento observável. Sem ela, a penalização existe mas não faz nada. | Bloqueia a transição Disponível → Pedido pendente |
| **HU-13** | Como gestor do parque, quero poder anular uma penalização, registando quem a anulou e porquê. | Won't | P | — | Resulta da mediação do conflito entre o técnico de balcão e o gestor do parque, registado como risco R7. O sistema é coerente sem ela: enquanto não existir, a penalização é irreversível. | — |

### Área funcional: Estado do equipamento

| ID | História | Prior. | Tam. | Crit. | Valor e impacto | Estado do equipamento |
|---|---|---|---|---|---|---|
| **HU-09** | Como técnico de balcão, quero marcar um equipamento como em manutenção ou indisponível, para o retirar de circulação. | Should | P | — | Terceira dificuldade declarada do domínio. Fecha a máquina de estados do equipamento e cria as transições proibidas que dão origem aos testes negativos previstos para o risco R1. | Disponível → Em manutenção, e Em manutenção → Disponível |
| **HU-11** | Como gestor do parque, quero consultar o histórico de requisições de um equipamento, para perceber o seu uso. | Could | P | — | Leitura sobre dados já existentes. Não participa no ciclo de empréstimo nem acrescenta transições. | — |

---

## 4. Critérios de aceitação

Escritos para as três histórias de maior prioridade. Os restantes são produzidos no E2, com a numeração dos requisitos. Cada história inclui um cenário negativo, que dá origem aos testes negativos exigidos pelo risco R1.

### HU-01 · Consultar equipamentos disponíveis

- Dado um catálogo com equipamentos em vários estados, quando o requisitante consulta a lista de disponíveis, então vê apenas os equipamentos em estado **Disponível**.
- Dado um equipamento em estado **Em manutenção**, quando o requisitante consulta a lista de disponíveis, então esse equipamento não aparece.
- Dado um kit cujos componentes estão todos disponíveis, quando o requisitante consulta a lista, então o kit aparece como uma unidade indivisível, e não como componentes soltos.

### HU-02 · Submeter uma requisição

- Dado um equipamento **Disponível** e um requisitante sem penalização ativa, quando submete uma requisição, então é criada com estado **Pedido pendente** e o equipamento deixa de aparecer como disponível para novos pedidos.
- Dado um requisitante com penalização ativa, quando tenta submeter uma requisição, então o sistema recusa e indica a data em que a penalização termina.
- Dado um equipamento em estado **Em manutenção**, quando o requisitante tenta requisitá-lo, então o sistema recusa, porque a transição Em manutenção → Pedido pendente não existe.

### HU-03 · Aprovar ou recusar uma requisição

- Dado um pedido pendente sobre um equipamento, quando o técnico de balcão o aprova, então o equipamento passa a **Reservado** e deixa de poder ser pedido por outro requisitante.
- Dado um pedido pendente, quando o técnico de balcão o recusa, então o equipamento volta a **Disponível** e o motivo da recusa fica registado.
- Dado um pedido já aprovado, quando o técnico tenta aprová-lo de novo, então o sistema recusa, porque a transição Reservado → Reservado não existe.

---

## 5. Histórias excluídas

Registadas para que não voltem a ser propostas, por um elemento do grupo ou por uma ferramenta de IA. A razão é sempre a lista de exclusões de [`visao.md`](visao.md).

| ID | História | Razão da exclusão |
|---|---|---|
| **HX-01** | Como requisitante, quero ser avisado antes do prazo de devolução. | Integração com sistemas externos está fora do âmbito. |
| **HX-02** | Como requisitante, quero pagar a minha penalização. | Pagamentos reais estão fora do âmbito. |
| **HX-03** | Como requisitante, quero reservar equipamento com semanas de antecedência num calendário. | Reserva por calendário está fora do âmbito. |
| **HX-04** | Como técnico de balcão, quero aceitar a devolução de um kit incompleto. | O kit é tratado como unidade indivisível; a devolução parcial está fora do âmbito. |
| **HX-05** | Como gestor do parque, quero abrir ordens de reparação para equipamento avariado. | Manutenção como processo está fora do âmbito. |

---

## 6. Linha de corte

- **Must (HU-01 a HU-08)** — o núcleo que tem de funcionar de ponta a ponta. Cobrem os três verbos do domínio (requisição, levantamento e devolução) e as duas primeiras dificuldades declaradas, os atrasos e as penalizações.
- **Should (HU-09)** — primeira candidata a entrar acima da linha, por ser a única das restantes que fecha a terceira dificuldade do domínio e acrescenta transições à entidade principal.
- **Could (HU-10, HU-11, HU-12)** — leitura ou funcionalidade de conveniência. Entram apenas se o âmbito o permitir, e a sua ausência não impede o sistema de resolver o problema descrito na visão.
- **Won't (HU-13)** — a anulação de penalização, adiada por decisão registada na secção 6 de [`stakeholders.md`](stakeholders.md).

Se o tempo faltar, corta-se pelos Could, nunca na verificação das histórias que ficam.

---

## 7. Manutenção deste backlog

O backlog é revisto no planeamento de cada iteração. Uma história nova entra sempre no fim da sua área funcional e só sobe de classificação por decisão explícita e registada do grupo.

Quando a alteração de requisitos chegar, as histórias afetadas são identificadas pelo seu ID antes de qualquer alteração de código, e o backlog é atualizado em conjunto com os requisitos e a rastreabilidade, não depois.
