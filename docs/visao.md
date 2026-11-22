# Visão do sistema

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 22 de novembro de 2026

> Nota de contexto: Os dados de utilizadores, equipamentos e requisições usados em exemplos, testes e demonstrações são inteiramente fictícios.

---

## 1. Problema

O empréstimo de portáteis e kits é hoje gerido fora de qualquer sistema. O pedido é feito informalmente ao balcão, o registo do que saiu e do que voltou fica em papel ou numa folha de cálculo mantida à mão, e o estado real de cada equipamento só é conhecido por quem está de serviço nesse momento.

Daí resultam três falhas, que correspondem às três dificuldades do domínio e que o sistema existe para eliminar:

### 1.1 O estado do equipamento não é fiável

Não há forma de saber, num dado instante, se um portátil está disponível, reservado, emprestado, em atraso ou em manutenção. 

### 1.2 Os atrasos não são detetados

A devolução fora de prazo só é notada quando alguém precisa do equipamento e ele não está lá, ou seja, "Em atraso" não existe como estado.

### 1.3 As penalizações não são aplicadas de forma consistente

Sem regra escrita e sem registo do que aconteceu, a consequência de um atraso depende de quem está a atender.

---

## 2. Utilizadores

| Utilizador | O que faz no sistema |
|---|---|
| **Requisitante** (aluno ou docente) | Consulta o que está disponível, submete uma requisição, levanta e devolve o equipamento, consulta as suas requisições e o seu estado de penalização. |
| **Técnico de balcão** | Aprova ou recusa requisições, confirma o levantamento fixando o prazo de devolução, regista a devolução e marca equipamento como em manutenção. |
| **Gestor do parque de equipamentos** | Mantém o catálogo de equipamentos e kits, consulta o histórico de cada equipamento e a lista de requisições em atraso. |


---

## 3. O que fica fora do âmbito

Os temas seguintes ficam **explicitamente** fora do âmbito. Qualquer proposta nestes termos é rejeitada por referência a esta secção, venha de um elemento do grupo ou de uma ferramenta de IA:

| Fora do âmbito | Fronteira exata |
|---|---|
| **Pagamentos reais** | A penalização é registada e produz efeito dentro do sistema, impedindo novas requisições. Não há cobrança, integração bancária nem emissão de documentos de dívida. |
| **Gestão de compras e inventário patrimonial** | O catálogo de equipamentos é dado. O sistema não trata aquisições, abates, amortizações nem contabilidade. |
| **Integração com sistemas externos** | Sem autenticação institucional, sem calendário académico, sem envio de email ou SMS. As notificações de aproximação do prazo ficam fora desta iteração. |
| **Manutenção como processo** | Um equipamento pode ser marcado como "em manutenção", mas o sistema não gere ordens de reparação, prazos de assistência, custos nem fornecedores. |
| **Reserva por calendário** | A requisição é para levantamento imediato ou para uma data única. Não há agenda nem gestão de conflitos de horário. |
| **Devolução parcial de kits** | Um kit é tratado como unidade indivisível. Devolve-se inteiro ou fica por devolver. |
| **Aplicação móvel, leitura de códigos de barras e interface elaborada** | A qualidade visual não é objeto de avaliação. A interface é a mínima necessária para executar os casos de uso. |
| **Dados pessoais reais** | Nenhum nome, email ou número de aluno real entra no sistema nem nos prompts dados às ferramentas de IA. |

---

## 4. Documentos relacionados

| Documento | Conteúdo |
|---|---|
| [`stakeholders.md`](stakeholders.md) | Identificação, classificação, matriz poder–interesse e comunicação |
| [`riscos.md`](riscos.md) | Registo de riscos com probabilidade, impacto, nível e resposta |
| [`processo.md`](processo.md) | Modelo de processo escolhido e alternativas consideradas |
| [`backlog.md`](backlog.md) | Product Goal, backlog priorizado em MoSCoW e critérios de aceitação |
| [`dod.md`](dod.md) | Definition of Done aplicada a todas as histórias |
