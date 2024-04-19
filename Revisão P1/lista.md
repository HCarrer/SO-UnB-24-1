## Lista Revisão P1
## Exercícios

### Conteúdo: Conceitos de base, Gerência de Processos, Deadlock

1. **Explique como o vetor de interrupções é utilizado na implementação da multiprogramação.**<br/>
Vetor de interrupções é um vetor contendo os endereços de memória das rotinas de tratamento de interrupção de cada classe do sistema. Quando uma interrupção ocorre em um processo, o SO captura o erro X e acessa o vetor de interrupções na posição X, obtendo assim o endereço da rotina de tratamento da interrupção obtida. Após isso o sistema lê este endereço e executa a rotina presente naquele endereço.

2. **Considere os processos abaixo**

| Processos | Tempo de execução |
|-----------|-------------------|
| P1        | 2                 |
| P2        | 14                |
| P3        | 10                |
| P4        | 1                 |
| P5        | 6                 |

**A ordem de chegada dos processos no sistema é P1, P2, P3, P4 e P5 (do mais antigo para o mais recente). No instante 0, todos os processos estão no estado ready. Admita que o tempo de salvamento de contexto é 1, o tempo de restauração de contexto é 1 e o quantum é 5. Forneça a ordem de execução dos processos e o diagrama de Gantt. Determine o tempo de turnaround de cada processo bem como o tempo médio de turnaround para o Round-Robin e o First Come First Served.**<br/>

**Round Robin**
```
      1   2
P1  |---|---|
            | 1   5   1                                   1   5   1                   1   4 
P2          |---|---|---|                               |---|---|---|               |---|---|
                        | 1   5   1                     |           | 1   5         |
P3                      |---|---|---|                   |           |---|---|       |
                                    | 1   1             |                   |       |
P4                                  |---|---|           |                   |       |
                                            | 1   5   1 |                   | 1   1 |
P5                                          |---|---|---|                   |---|---|

Tn(P1) = 1 + 2 = 3
Tn(P2) = 1 + 2 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 1 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 1 + 4 = 46
Tn(P3) = 1 + 2 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 1 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 5 = 39
Tn(P4) = 1 + 2 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 1 = 19
Tn(P5) = 1 + 2 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 1 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 5 + 1 + 1 = 41

Tn(médio) = ( Tn(P1) + Tn(P2) + Tn(P3) + Tn(P4) + Tn(P5) ) / 5 = 29,6

Ordem = P1 -> P2 -> P3 -> P4 -> P5 -> P2 -> P3 -> P5 -> P2
```

**First Come First Served**
```
      1   2
P1  |---|---|
            | 1   14
P2          |---|---|
                    | 1   10
P3                  |---|---|
                            | 1   1
P4                          |---|---|
                                    | 1   6
P5                                  |---|---|

Tn(P1) = 1 + 2 = 3
Tn(P2) = 1 + 2 + 1 + 14 = 18
Tn(P3) = 1 + 2 + 1 + 14 + 1 + 10 = 29
Tn(P4) = 1 + 2 + 1 + 14 + 1 + 10 + 1 + 1 = 31
Tn(P5) = 1 + 2 + 1 + 14 + 1 + 10 + 1 + 1 + 1 + 6 = 38

Tn(médio) = ( Tn(P1) + Tn(P2) + Tn(P3) + Tn(P4) + Tn(P5) ) / 5 = 23,8

Ordem = P1 -> P2 -> P3 -> P4 -> P5
```

3. **Mostre que a exclusão mútua não é garantida se a primitiva P(sem) (ou Down(sem)) não for implementada de maneira atômica**<br/>

```
P(sem): if(sem > 0)
          sem--
        else
          bloqueia(sem)
```

```
P1          |   P2
            |   
P(sem)      |   P(sem)
/* SC */    |   /* SC */
V(sem)      |   V(sem)
```

```
- P1 executa                      |
- quantum depois de if(sem > 0)   |
                                  |   P2 executa
                                  |   quantum na SC
- entra na SC                     |
```

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
Exclusão mútua: cada recurso deve ser alocado de maneira exclusiva<br/>
Posse e espera: um processo que detem recursos pode solicitar novos recursos<br/>
Não-preempção: cada recurso só pode ser liberado pelo processo que o detém<br/>
Espera circular: deve existir um ciclo de processos onde cada processo está esperando por um recurso detido pelo próximo membro da cadeia<br/>

**b) Diga quais condições necessárias para a ocorrência de deadlock estão presentes nesse exemplo. Justifique sua resposta.**<br/>
Exclusão Mútua: Impressoa e scanner são recursos exclusivos<br/>
Posse e espera: Os dois processos solicitam novos recursos sem liberar os outros<br/>
Não preempção: Interromper impressora e scanner causam prejuizo da computação<br/>
Espera circular:

```
Seja:
  ___
/  X  \    => Processo X
\_____/

 _____
|  Y  |    => Recurso Y
|_____|

```

```
       ___                 _____
     /  P1 \   <--------  |  R1 |
     \_____/              |_____|
        \                    /\
         \                   |
          \    ______________|
           \  /
            \/_______________
            /                | 
           /                 |
          /                  \/
       ___                 _____
     /  P2 \   <--------  |  R2 |
     \_____/              |_____|

```

**---------------------------**<br/>

**Extra: Suponha que os processos P1, P3 e P5 do exercício 2 possuem prioridade 1 e os processos P2 e P4 possuem prioridade 2. Forneça a ordem de execução dos processos e o diagrama de Gantt. Determine o tempo de turnaround de cada processo bem como o tempo médio de turnaround para ambas as filas de prioridade utilizando o método Round-Robin.**

**Prioridade 1**
```
      1   2
P1  |---|---|
            | 1   5   1               1   5
P3          |---|---|---|           |---|---|
                        | 1   5   1 |       | 1   1
P5                      |---|---|---|       |---|---|

Tn(P1) = 1 + 2 = 3
Tn(P3) = 1 + 2 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 5 = 23
Tn(P5) = 1 + 2 + 1 + 5 + 1 + 1 + 5 + 1 + 1 + 5 + 1 + 1 = 25
```

**Prioridade 2**
```
     Tn(P5)  1   5   1           1   5   1   1   4
P2  |------|---|---|---|       |---|---|---|---|---|
                       | 1   1 |
P4                     |---|---|

Tn(P2) = Tn(P5) + 1 + 5 + 1 + 1 + 1 + 1 + 5 + 1 + 1 + 4 = 46
Tn(P4) = Tn(P5) + 1 + 5 + 1 + 1 + 1 = 34

Tn(médio) = ( Tn(P1) + Tn(P2) + Tn(P3) + Tn(P4) + Tn(P5) ) / 5 = 26,2

Ordem = P1 -> P3 -> P5 -> P3 -> P5 -> P2 -> P4 -> P2
```