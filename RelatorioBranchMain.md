# 🧮 Atividade 04 – Estado de Tarefas (Branch main)  
**Disciplina:** Sistemas Operacionais  
**Curso:** TADS – IFRN / CNAT  
**Aluno:** Aaron Guerra Goldberg  
**Matrícula:** 20251014040042  
**Período:** 2025.2  
**Professor:** Leonardo A. Minora  

---

## 🎯 Objetivo
Preencher as tabelas de transição de estados das tarefas t1, t2 e t3 com base no quantum do SO e analisar o comportamento da tarefa t3.

---

## ⚙️ Atividade 1 – Fatia de tempo = 1 tick

| Tick | SO   | t1          | t2          | t3          | Fila de pr   |
|------|------|-------------|-------------|-------------|--------------|
| 01   | ex   | --          | --          | --          | --           |
| 02   | ex   | no          | --          | --          | --           |
| 03   | ex   | pr          | no          | --          | t1           |
| 04   | ex   | --          | pr          | no          | t1, t2       |
| 05   | ex t1| --          | --          | pr          | t2, t3       |
| 06   | --   | ex linha 1  | --          | --          | t2, t3       |
| 07   | ex t2| su 1        | --          | --          | t2, t3       |
| 08   | --   | su 2        | ex linha 1  | --          | t3           |
| 09   | ex t3| pr          | su 1        | --          | t1           |
| 10   | --   | --          | su 2        | ex linha 1  | t1           |
| 11   | ex t1| --          | --          | pr          | t1           |
| 12   | --   | fi          | --          | ex linha 1  | t1           |

**Comentários:**  
- A tarefa t3 só entra em execução depois que t1 e t2 entram em espera (su).  
- Devido ao quantum = 1 tick, as tarefas alternam rapidamente, causando várias trocas de contexto.

---

## ⚙️ Atividade 2 – Fatia de tempo = 10 ticks

| Tick | SO   | t1          | t2          | t3          | Fila de pr   |
|------|------|-------------|-------------|-------------|--------------|
| 01   | ex   | --          | --          | --          | --           |
| 02   | ex   | no          | --          | --          | --           |
| 03   | ex   | pr          | no          | --          | t1           |
| 04   | ex   | --          | pr          | no          | t1, t2       |
| 05   | ex t1| --          | --          | pr          | t2, t3       |
| 06   | --   | ex linha 1  | --          | --          | t2, t3       |
| 07   | ex t2| su 1        | --          | --          | t2, t3       |
| 08   | --   | su 2        | ex linha 1  | --          | t3           |
| 09   | ex t3| pr          | su 1        | --          | t1           |
| 10   | --   | --          | su 2        | ex linha 1  | t1           |
| 11   | ex t1| --          | --          | pr          | t1           |
| 12   | --   | fi          | --          | ex linha 1  | t1           |

**Comentários:**  
- Com quantum maior (10 ticks), as tarefas executam por mais tempo contínuo antes de serem preemptadas.  
- A tarefa t3 executa mais “seguidas”, sofrendo menos interrupções, o que reduz o overhead de troca de contexto.

---

## 🔄 Comparação do comportamento da tarefa t3

- **Quantum 1 tick:** t3 sofre várias preempções e alternâncias entre execução e espera.  
- **Quantum 10 ticks:** t3 executa por períodos maiores de uma vez, com menos trocas de contexto.  

**Conclusão:**  
O tamanho da fatia de tempo influencia diretamente o comportamento da tarefa t3: quanto menor o quantum, mais trocas de contexto ocorrem; quanto maior, a execução é mais contínua e eficiente, mas pode atrasar a execução de outras tarefas.