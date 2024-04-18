## Lista Revisão P1
## Exercícios

### Conteúdo: Conceitos de base, Gerência de Processos, Deadlock

1. **Explique como o vetor de interrupções é utilizado na implementação da multiprogramação.**<br/>

2. **Considere os processos abaixo**
| Processos | Tempo de execução |
|-----------|-------------------|
| P1        | 2                 |
| P2        | 14                |
| P3        | 10                |
| P4        | 1                 |
| P5        | 6                 |

**A ordem de chegada dos processos no sistema é P1, P2, P3, P4 e P5 (do mais antigo para o mais recente). No instante 0, todos os processos estão no estado ready. Admita que o tempo de salvamento de contexto é 1, o tempo de restauração de contexto é 1 e o quantum é 5. Forneça a ordem de execução dos processos e o diagrama de Gantt. Determine o tempo de turnaround de cada processo bem como o tempo médio de turnaround para o Round-Robin e o First Come First Served.**<br/>


3. **Mostre que a exclusão mútua não é garantida se a primitiva P(sem) (ou Down(sem)) não for implementada de maneira atômica**<br/>

4. **Considere o seguinte cenário**
```
P1              |   P2
                |
Obtem(R2);      |   Obtem(R1);
Obtem(R1);      |   Obtem(R2);
-- processa --  |   -- processa --
Libera(R1);     |   Libera(R2);
Libera(R2);     |   Libera(R1);
```

**Admita que R1=impressora e R2=scanner.**<br/>

**a) Comente as condições necessárias para a ocorrência de deadlock.**<br/>
**b) Diga quais condições necessárias para a ocorrência de deadlock estão presentes nesse exemplo. Justifique sua resposta.**<br/>

**---------------------------**<br/>

**Extra: Suponha que os processos P1, P3 e P5 do exercício 2 possuem prioridade 1 e os processos P2 e P4 possuem prioridade 2. Forneça a ordem de execução dos processos e o diagrama de Gantt. Determine o tempo de turnaround de cada processo bem como o tempo médio de turnaround para ambas as filas de prioridade utilizando o método Round-Robin.**