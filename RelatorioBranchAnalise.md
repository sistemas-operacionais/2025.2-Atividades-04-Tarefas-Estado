# 📘 Atividade 04 – Estados e Troca de Contexto de Tarefas  
**Disciplina:** Sistemas Operacionais  
**Curso:** TADS – IFRN / CNAT  
**Aluno:** Aaron Guerra Goldberg   
**Matrícula:** 20251014040042  
**Período:** 2025.2  
**Professor:** Leonardo A. Minora  

---

## 🧩 Atividade 1 – Identificação dos Estados de uma Tarefa  

### 🎯 Objetivo  
Compreender os diferentes estados pelos quais uma tarefa pode passar durante sua execução em um sistema operacional.

### 🧠 Estados principais  
- **Novo (New):** o processo está sendo criado e ainda não foi admitido pelo SO.  
- **Pronto (Ready):** o processo aguarda ser escolhido para usar a CPU.  
- **Executando (Running):** o processo está sendo executado.  
- **Esperando (Waiting/Blocked):** o processo está aguardando algum evento, como E/S.  
- **Terminado (Terminated):** o processo finalizou sua execução e liberou os recursos.

---

### 🗺️ Diagrama de estados (texto simplificado)

```
Novo → Pronto → Executando → Esperando → Pronto → Executando → Terminado
```

---

### 🔄 Transições e exemplos  

| Transição | Evento que causa a mudança | Exemplo prático |
|------------|----------------------------|-----------------|
| Novo → Pronto | Processo é criado e admitido pelo SO | Abrir um programa no computador |
| Pronto → Executando | Escalonador escolhe o processo para usar a CPU | O programa começa a rodar |
| Executando → Esperando | Processo realiza uma operação de E/S | Ler dados de um arquivo |
| Esperando → Pronto | E/S foi concluída | Leitura do arquivo terminou |
| Executando → Terminado | Processo concluiu suas instruções | Programa fecha normalmente |
| Executando → Pronto | Fim da fatia de tempo (preempção) | SO pausa o processo e escolhe outro |

---

## ⚙️ Atividade 2 – Simulação de Transições de Estado  

### 🎯 Objetivo  
Simular a execução de três processos e observar suas transições de estado ao longo do tempo.

### 🧩 Cenário  
- **P1:** Processo intensivo em CPU (não faz E/S)  
- **P2:** Processo que faz E/S de disco  
- **P3:** Processo que aguarda entrada do usuário  

---

### 🕒 Tabela temporal  

| Tempo (t) | P1 | P2 | P3 | Evento / Justificativa |
|------------|----|----|----|------------------------|
| t0 | Novo | Novo | Novo | Processos criados |
| t1 | Executando | Pronto | Pronto | Escalonador inicia P1 |
| t2 | Executando | Pronto | Pronto | P1 continua (é CPU-bound) |
| t3 | Pronto | Executando | Pronto | P2 entra na CPU |
| t4 | Pronto | Esperando | Pronto | P2 faz E/S de disco e é bloqueado |
| t5 | Executando | Esperando | Pronto | Escalonador dá CPU para P1 |
| t6 | Executando | Pronto | Pronto | P2 termina a E/S e volta para a fila |
| t7 | Pronto | Executando | Pronto | Escalonador escolhe P2 novamente |
| t8 | Pronto | Esperando | Executando | P2 faz nova E/S e P3 ganha a CPU |
| t9 | Pronto | Esperando | Esperando | P3 solicita entrada do usuário |
| t10 | Executando | Esperando | Esperando | Escalonador retorna o CPU-bound P1 |
| t11 | Terminado | Esperando | Esperando | P1 termina a execução |
| t12 | -- | Executando | Esperando | P2 volta e executa até o fim |
| t13 | -- | Terminado | Esperando | P2 finaliza |
| t14 | -- | -- | Executando | P3 recebe entrada e termina |
| t15 | -- | -- | Terminado | Todos os processos finalizados |

---

### 💬 Análise do escalonamento  
O escalonador utiliza um algoritmo **round robin simples**, alternando os processos conforme a disponibilidade da CPU.  
P1 fica mais tempo executando porque não realiza E/S.  
P2 e P3 entram em espera várias vezes, o que faz o SO alternar entre eles e P1.  
Ao final, P1 termina primeiro, seguido por P2 (depois das operações de E/S) e P3 (após a entrada do usuário).

---

## 🔄 Atividade 3 – Análise de Troca de Contexto  

### 🎯 Objetivo  
Analisar as trocas de contexto e seu impacto no desempenho do sistema.

---

### 🧩 Identificação de trocas de contexto  

As principais transições que causam troca de contexto são:
- **Executando → Pronto (preempção)**  
- **Executando → Esperando (bloqueio por E/S)**  
- **Pronto → Executando (despacho de CPU)**  

Essas trocas ocorrem porque o sistema operacional precisa **salvar o estado do processo atual** e **carregar o estado de outro processo** que vai assumir a CPU.

---

### 🧮 Análise do cenário da Atividade 2  

| Momento | Processo que saiu | Processo que entrou | Motivo da troca |
|----------|------------------|--------------------|----------------|
| t2 | P1 | P2 | Preempção (fatia de tempo terminou) |
| t4 | P2 | P1 | Bloqueio por E/S |
| t7 | P1 | P2 | P2 voltou da E/S |
| t8 | P2 | P3 | Bloqueio por nova E/S |
| t10 | P3 | P1 | Entrada do usuário pendente |
| t12 | P1 | P2 | P1 terminou, CPU passa a P2 |
| t14 | P2 | P3 | P2 finalizou, P3 executa |

---

### 💰 Custo da troca de contexto  

Durante cada troca, o SO precisa salvar:
- Registradores gerais  
- Contador de programa (PC)  
- Ponteiro de pilha (SP)  
- Estado da memória e de dispositivos  

Essas operações não executam instruções dos usuários, mas gastam **tempo da CPU**, gerando um **overhead**.

> Quanto mais trocas de contexto, maior o custo total e menor o desempenho geral do sistema.

---

### 🚀 Otimizações e conclusões  

**Como reduzir trocas desnecessárias:**
- Aumentar o quantum de CPU para evitar preempções muito frequentes;  
- Priorizar processos curtos e evitar alternância excessiva;  
- Manter um bom balanceamento entre CPU-bound e I/O-bound.

**Conclusão:**
> O estudo das trocas de contexto ajuda a entender como o sistema operacional gerencia vários processos ao mesmo tempo.  
> Compreender os estados e as transições é essencial para perceber como o SO busca equilibrar **desempenho**, **justiça** e **resposta rápida** ao usuário.