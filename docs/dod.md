# Definition of Done

**Domínio:** Empréstimo de equipamentos
**Grupo:** Samuel Freitas e João Oliveira · **Turma:** A
**Entrega:** E1 — Visão e plano · 22 de novembro de 2026

---

## 1. A regra

Uma história só está concluída quando cumpre **todos** os critérios da secção 2. Enquanto faltar um, a história fica em curso, qualquer que seja a percentagem de código escrito.

---

## 2. Critérios

| # | Critério | Porque está aqui |
|---|---|---|
| **1** | Os critérios de aceitação da história estão verificados, um a um. | É o que distingue "feito" de "parece feito". |
| **2** | Os casos de teste foram desenhados a partir dos requisitos **antes** de existir código, estão escritos e passam. | Risco **R3**: testes derivados do código confirmam o defeito que lá está. |
| **3** | A suite completa corre sem falhas, não apenas os testes da história. | Risco **R4**: regenerar um ficheiro introduz regressões em código vizinho que já passava. |
| **4** | Todo o código gerado por IA foi lido e revisto por um elemento do grupo. | Riscos **R1** e **R3**: o erro de geração não é visível à leitura distraída. |
| **5** | O código entrou por pull request aprovado por outro elemento do grupo, com o diff lido. | Risco **R4**, e a regra do enunciado. |
| **6** | A história declara o estado de entrada e o estado de saída do equipamento, e nenhuma transição proibida passa a ser possível. | Riscos **R1** e **R6**: um estado em falta tem de aparecer quando a história é escrita, não três sprints depois. |
| **7** | A rastreabilidade está atualizada: requisito → design → código → teste. | A ligação é atualizada no momento da alteração, não depois. |
| **8** | Os defeitos encontrados no código gerado estão no registo de defeitos, classificados como falta, erro ou falha, com a forma de deteção e a correção. | Entregável do E4. |
| **9** | Nenhum dado pessoal real e nenhum segredo entrou no código, nos testes ou nos prompts. | Regra do enunciado e exclusão declarada na visão. |

---

## 3. Âmbito

Os **critérios de aceitação** são de cada história e estão na secção 4 de [`backlog.md`](backlog.md). A **Definition of Done** aplica-se a todas, sem exceção, e não se negoceia história a história.

Esta lista é revista na retrospetiva de cada iteração. Um critério só é retirado por decisão registada do grupo; critérios novos podem ser acrescentados a qualquer momento.
