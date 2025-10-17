# 2025.2-Atividades-04-Tarefas-Estado
Atividade sobre transição de estado de uma tarefa no sistema operacional

## Atividade 1: Identificação dos Estados de uma Tarefa

**Objetivo:** Compreender os diferentes estados pelos quais uma tarefa (processo) pode passar durante sua execução em um sistema operacional.

**Descrição:**
Nesta atividade, você irá identificar e descrever os principais estados de uma tarefa em um sistema operacional. Os estados básicos incluem:

- **Novo (New):** O processo está sendo criado
- **Pronto (Ready):** O processo está aguardando ser atribuído a um processador
- **Executando (Running):** As instruções do processo estão sendo executadas
- **Esperando (Waiting/Blocked):** O processo está aguardando algum evento ocorrer (como conclusão de E/S)
- **Terminado (Terminated):** O processo terminou sua execução

**Tarefas:**
1. Desenhe um diagrama de estados mostrando todos os estados possíveis de uma tarefa
2. Para cada transição entre estados, identifique o evento que causa essa mudança
3. Dê exemplos práticos de situações que causariam cada transição

## Atividade 2: Simulação de Transições de Estado

**Objetivo:** Simular e analisar as transições de estado de processos em diferentes cenários.

**Descrição:**
Você irá simular a execução de múltiplos processos e acompanhar suas transições de estado ao longo do tempo.

**Cenário:**
Considere três processos (P1, P2, P3) com as seguintes características:
- P1: Processo intensivo em CPU (sem operações de E/S)
- P2: Processo que realiza operações de E/S de disco
- P3: Processo que aguarda entrada do usuário

**Tarefas:**
1. Crie uma tabela temporal mostrando o estado de cada processo em diferentes instantes (t0, t1, t2, ...)
2. Identifique os momentos em que ocorrem transições de estado
3. Justifique cada transição com base nas características do processo
4. Explique como o escalonador do sistema operacional decide qual processo executar em cada momento

## Atividade 3: Análise de Troca de Contexto

**Objetivo:** Analisar o processo de troca de contexto (context switching) e seu impacto no desempenho do sistema, utilizando os conceitos das Atividades 1 e 2.

**Descrição:**
A troca de contexto é o processo pelo qual o sistema operacional salva o estado de um processo em execução e restaura o estado de outro processo que estava pronto para executar. Este é um conceito fundamental que conecta as transições de estado estudadas anteriormente.

**Fundamentação teórica:**
Com base nas Atividades 1 e 2, você já conhece os estados pelos quais uma tarefa pode passar e como ocorrem as transições entre esses estados. A troca de contexto ocorre especificamente quando:
- Um processo passa do estado **Executando** para **Pronto** (preempção)
- Um processo passa do estado **Executando** para **Esperando** (bloqueio)
- Um processo passa do estado **Pronto** para **Executando** (despacho)

**Tarefas:**

1. **Identificação de trocas de contexto:**
   - Revise o diagrama de estados que você criou na Atividade 1
   - Identifique e marque todas as transições que envolvem uma troca de contexto
   - Explique por que essas transições específicas requerem troca de contexto

2. **Análise do cenário da Atividade 2:**
   - Retome a tabela temporal criada na Atividade 2 com os processos P1, P2 e P3
   - Identifique quantas trocas de contexto ocorreram durante a simulação
   - Para cada troca de contexto, descreva:
     * Qual processo estava executando
     * Qual processo passou a executar
     * O motivo da troca (preempção, bloqueio, conclusão de E/S, etc.)

3. **Custo da troca de contexto:**
   - Liste as informações que precisam ser salvas durante uma troca de contexto (registradores, contador de programa, ponteiro de pilha, etc.)
   - Explique por que a troca de contexto representa um overhead (custo) para o sistema
   - Discuta situações em que o número de trocas de contexto pode aumentar e impactar negativamente o desempenho

4. **Otimizações:**
   - Proponha estratégias que um sistema operacional pode adotar para minimizar o número de trocas de contexto desnecessárias
   - Discuta o trade-off entre responsividade do sistema e overhead de troca de contexto

**Entrega:**
Documente sua análise em um relatório contendo:
- Respostas para todas as tarefas acima
- Diagramas e tabelas quando apropriado
- Reflexões sobre como o conhecimento de troca de contexto ajuda a entender o funcionamento de um sistema operacional
