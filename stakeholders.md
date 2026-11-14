# Análise de stakeholders

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 13 de novembro de 2026

> Os stakeholders são fictícios, nenhum corresponde a uma pessoa real e nenhum nome real é usado.

---

## 1. Identificação

Critério de identificação: **quem usa, paga, gere, mantém ou é afetado pelo sistema.**

| ID | Stakeholder | Categoria | Porque é stakeholder |
|---|---|---|---|
| **STK-01** | Requisitante (aluno ou docente) | Utilizador final | **Usa** o sistema para pedir, levantar e devolver equipamento. |
| **STK-02** | Técnico de balcão | Utilizador final | **Usa** o sistema para aprovar, entregar e receber equipamentos. |
| **STK-03** | Gestor do parque de equipamentos | Cliente | **Gere** o catálogo e responde pelo estado do parque. |
| **STK-04** | Direção dos serviços | Cliente / patrocinador | **Paga** o sistema e define a política de empréstimo e de penalização. |
| **STK-05** | Assistência técnica contratada | Responsável de manutenção | **Mantém** o equipamento físico. É afetada pela forma como o sistema sinaliza avarias e retira equipamento de circulação. |
| **STK-06** | Conselho pedagógico | Stakeholder externo | **É afetado**: aprova o regulamento de empréstimo e é a instância a que um requisitante recorre se contestar uma penalização. |
| **STK-07** | Equipa de desenvolvimento | Equipa de desenvolvimento | Especifica, decide e responde pelo que é construído. |

---

## 2. Classificação

| ID | Stakeholder | Posição | Influência | Interesse | Função |
|---|---|---|---|---|---|
| STK-01 | Requisitante | Interno | Baixa | Direto | Negócio |
| STK-02 | Técnico de balcão | Interno | Média | Direto | Suporte |
| STK-03 | Gestor do parque | Interno | Alta | Direto | Negócio |
| STK-04 | Direção dos serviços | Interno | Alta | Indireto | Negócio |
| STK-05 | Assistência técnica contratada | Externo | Baixa | Indireto | Suporte |
| STK-06 | Conselho pedagógico | Interno | Alta | Indireto | Legal |
| STK-07 | Equipa de desenvolvimento | Externo | Média | Direto | Técnica |

- **Posição** é lida face à organização onde o sistema é implantado: internos os serviços e quem a eles pertence, externos a assistência contratada e a equipa de projeto.
- **Interesse** direto significa impacto operacional enquanto que o indireto significa impacto estratégico ou normativo.

---

## 3. Matriz poder–interesse

|  | **Interesse baixo** | **Interesse alto** |
|---|---|---|
| **Poder alto** | **Manter satisfeito**<br>STK-04 Direção dos serviços<br>STK-06 Conselho pedagógico | **Gerir de perto e envolver**<br>STK-03 Gestor do parque |
| **Poder baixo** | **Monitorizar**<br>STK-05 Assistência técnica contratada | **Manter informado**<br>STK-01 Requisitante<br>STK-02 Técnico de balcão<br>STK-07 Equipa de desenvolvimento |

Leitura da matriz:

- **STK-03** é quem tem poder de decisão sobre o parque e, ao mesmo tempo, sofre diariamente as consequências do sistema.
- **STK-04 e STK-06** têm poder para travar o sistema, mas não o usam no dia a dia.
- **STK-02** tem interesse altíssimo e pouco poder formal. Se o sistema o atrapalhar contorna-o, assim como é a via mais provável de falha do sistema, mesmo que tudo o resto esteja correto.
- **STK-05** acompanha-se com esforço mínimo, com atenção a mudanças no modo como as avarias são sinalizadas.

---

## 4. Necessidades e objetivos

### STK-01 · Requisitante

- *Explícitas:* saber o que está disponível; requisitar sem processo moroso; conhecer o prazo de devolução; saber se tem penalização ativa e até quando.
- *Implícita:* que a penalização dependa apenas da regra e não de quem o atende.
- *Restrição que impõe:* não aceita ser penalizado sem conseguir saber porquê.

### STK-02 · Técnico de balcão

- *Explícitas:* registar levantamentos e devoluções em poucos passos; ver o estado do equipamento no momento do atendimento; retirar de circulação equipamento avariado sem esperar por autorização.
- *Implícita:* não ser obrigado a decidir sozinho os casos duvidosos como atraso limítrofe, kit incompleto, equipamento devolvido com dano.
- *Restrição que impõe:* o registo tem de ser mais rápido do que o papel, ou é abandonado.

### STK-03 · Gestor do parque de equipamentos

- *Explícitas:* ter o estado real e único de cada equipamento a qualquer momento; obter a lista de requisições em atraso sem a construir à mão; consultar o histórico de uso de um equipamento.
- *Implícita:* que o sistema nunca perca o registo de uma devolução.
- *Restrição que impõe:* nenhum equipamento em manutenção pode voltar a ser emprestado.

### STK-04 · Direção dos serviços

- *Explícitas:* reduzir perdas e devoluções fora de prazo; penalização uniforme para todos; poder justificar qualquer decisão tomada.
- *Implícita:* poder ajustar prazos e valores de penalização sem mandar reescrever o sistema.
- *Restrição que impõe:* a regra de penalização tem de estar conforme o regulamento aprovado.

### STK-05 · Assistência técnica contratada

- *Explícita:* saber que equipamento está sinalizado como avariado e desde quando.
- *Implícita:* que o equipamento não lhe chegue ainda associado a uma requisição aberta.
- *Restrição que impõe:* equipamento em manutenção fica indisponível até ela o devolver ao serviço.

### STK-06 · Conselho pedagógico

- *Explícita:* que as penalizações aplicadas sejam rastreáveis até ao regulamento.
- *Implícita:* que exista registo suficiente para instruir uma reclamação.
- *Restrição que impõe:* a regra de penalização não pode ser alterada sem aprovação.

### STK-07 · Equipa de desenvolvimento

- *Explícitas:* âmbito limitado a 3 a 5 casos de uso; requisitos verificáveis; rastreabilidade mantida entre requisito, design, código e teste.
- *Implícita:* que o código gerado por IA seja tratado como suspeito até ser verificado.
- *Restrição que impõe:* nenhuma funcionalidade é dada como concluída sem passar nos testes desenhados a partir dos requisitos.

---

## 5. Conflito previsível

**STK-02 (Técnico de balcão) × STK-03 (Gestor do parque de equipamentos)**

O técnico de balcão quer poder aceitar uma devolução em atraso **sem aplicar penalização**, quando o requisitante apresenta uma justificação que lhe parece razoável. O gestor do parque quer a regra aplicada **sem exceções**, porque é a uniformidade que dá à penalização efeito dissuasor e é ela que lhe permite justificar as decisões perante a direção e perante o conselho pedagógico.

Os dois objetivos são incompatíveis: ou existe discricionariedade no atendimento, ou não existe.

**Mediação proposta pela equipa de desenvolvimento.** A penalização é aplicada automaticamente pelo sistema, sem exceção no momento do atendimento, o que satisfaz STK-03, STK-04 e STK-06. Em compensação, o sistema regista a devolução com um campo de observação livre preenchido pelo técnico, e a penalização é **anulável a posteriori** por STK-03, com registo de quem a anulou e porquê. O técnico deixa de ter de decidir sozinho, mas a sua observação não se perde.

Esta decisão tem consequência direta no âmbito: a anulação de penalização é uma funcionalidade nova, que entra no backlog com prioridade baixa e **não** está entre os primeiros casos de uso a implementar. Enquanto não existir, a penalização é irreversível dentro do sistema.

O conflito está inscrito no registo de riscos como **R7**, do tipo *Conflito de stakeholders*.

---

## 6. Estratégia de comunicação

| ID | Stakeholder | Canal | Frequência | Linguagem |
|---|---|---|---|---|
| STK-01 | Requisitante | Sessões de teste de aceitação | A cada incremento | Operacional |
| STK-02 | Técnico de balcão | Reuniões curtas no local de trabalho e testes de usabilidade | Semanal | Operacional |
| STK-03 | Gestor do parque | Reunião de acompanhamento e demonstração do incremento | Semanal | Operacional e técnica |
| STK-04 | Direção dos serviços | Relatório de progresso | No fim de cada iteração | Estratégica |
| STK-05 | Assistência técnica contratada | Email e documentação | Quando necessário | Técnica e formal |
| STK-06 | Conselho pedagógico | Documento formal com a regra de penalização implementada | Uma vez, antes da entrada em serviço | Legal e formal |
| STK-07 | Equipa de desenvolvimento | Reuniões técnicas e revisão de pull requests | Diária | Técnica |

---

## 7. Manutenção deste registo

Este documento é revisto no início de cada entrega seguinte e sempre que o âmbito mudar, em particular quando chegar a alteração de requisitos de janeiro.