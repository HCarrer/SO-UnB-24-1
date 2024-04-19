## Lista 2
## Exercícios

### Conteúdo: Gerência Básica de Processos, Escalonamento de Processos

1. **Defina processo e diferencie processo de programa.**
Um processo é um programa em execução. Exemplo: programa é a receita de um bolo e processo é o ato de fazer o bolo.

2. **As informações que compõem um processo podem ser de dois tipos. Quais são estes tipos e o que eles representam?**
Informações de ambiente e informações de execução.

3. **Cite um SO onde um processo é criado a partir de um programa e um SO onde um processo é criado a partir de outro processo.**
MS-Dos e Unix, respectivamente.

4. **Que estrutura de dados contém informações sobre um processo?**
Tabela de processos

5. **O que é vetor de interrupções?**
Estrutura responsável por armazenar o endereço de rotina do tratamento de interrupção gerado por cada classe (disco, floppy, terminal, clock, etc).

6. **Defina troca de contexto.**
Troca de contexto é a operação de salvamento de registradores de um processo para depois se recuperar os registradores de um outro processo a ser colocado em execução.

7. **Qual a função de um algoritmo de escalonamento de processos? Em um sistema monoprocessado, o escalonamento de processos é útil?**
Determinar qual processo pronto vai ser colocado em execução e por quanto tempo.

8. **Cite 3 critérios que você considera mais importantes no projeto de um bom escalonador de processos.**
Justiça, maximizar o throughput e minimizar o tempo de resposta.

9. **Cite uma desvantagem do escalonador preemptivo e uma desvantagem do escalonador não-preemptivo.**
Preemptivo: maior complexidade para programar, podendo gerar um overhead.
Não-preemptivo: processos demorados podem acabar monopolizando o uso do processador caso não haja um comando especificando que a troca de contexto deve ocorrer.

10. **Cite parâmetros que devem ser levados em conta na determinação do quantum de um escalonador Round-Robin.**
Tempo médio da troca de contexto do tempo de resposta desejado.

11. **Considere o conjunto de 6 processos e respectivos tempos de execução (quantum = 8ms). A ordem de chegada dos processos foi A->B->C->D->E->F (do mais antigo para o mais recente). No momento de início da execução do algoritmo de escalonamento, todos os 6 processos estão prontos. Diga a ordem na qual este conjunto de processos será executado se considerarmos as políticas de escalonamento Round-Robin e Shortest Job First. Forneça também o diagrama de Gantt, o tempo de *turnaround* de cada processo e o tempo médio de *turnaround*.**

| Processos | Tempo de resposta (ms) |
|-----------|------------------------|
| A         | 9                      |
| B         | 20                     |
| C         | 2                      |
| D         | 6                      |
| E         | 18                     |
| F         | 3                      |

Resolução

**Round-Robin**

    8                 1
A |--|              |--|
       8            |  | 8     4
B    |--|           |  |--|  |--|
          2         |     |  |  |
C       |--|        |     |  |  |
             6      |     |  |  |
D          |--|     |     |  |  |
                8   |     | 8|  |  2
E             |--|  |     |--|  |--|
                   3|
F                |--|

Tn(A) = 8 + 8 + 2 + 6 + 8 + 3 + 1 = 36ms
Tn(B) = 8 + 8 + 2 + 6 + 8 + 3 + 1 + 8 + 8 + 4 = 56ms
Tn(C) = 8 + 8 + 2 = 18ms
Tn(D) = 8 + 8 + 2 + 6 = 24ms
Tn(E) = 8 + 8 + 2 + 6 + 8 + 3 + 1 + 8 + 8 + 4 + 2 = 58ms
Tn(F) = 8 + 8 + 2 + 6 + 8 + 3 = 35ms

Tn(médio) = ( Tn(A) + Tn(B) + Tn(C) + Tn(D) + Tn(E) + Tn(F) ) / 6 = 37,8333...



**Shortest Job First**
             9
A          |--|
           |  |   20
B          |  |  |--|
    2      |  |  |
C |--|     |  |  |
     |    6|  |  |
D    |  |--|  |  |
     |  |     |18|
E    |  |     |--|
     | 3|
F    |--|

Tn(A) = 2 + 3 + 6 + 9 = 20
Tn(B) = 2 + 3 + 6 + 9 + 18 + 20 = 58
Tn(C) = 2
Tn(D) = 2 + 3 + 6 = 11
Tn(E) = 2 + 3 + 6 + 9 + 18 = 38
Tn(F) = 2 + 3 + = 5

Tn(médio) = ( Tn(A) + Tn(B) + Tn(C) + Tn(D) + Tn(E) + Tn(F) ) / 6 = 22,333...