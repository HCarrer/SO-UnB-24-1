## Lista 4
## Exercícios

### Conteúdo: ?

1. **Defina condições de corrida.**<br/>
Acontecem quando dois processos acessam concorrentemente as mesmas posições de memória.

2. **Cite 2 maneiras pelas quais pode ser implementada a espera de um processo pela posse da seção crítica.**<br/>
Espera limitada (busy wait) e bloqueio de processos.

3. **Diferencie seção crítica e exclusão mútua.**<br/>
Seção crítica é a parte do código onde há condição de corrida. Exclusão mútua impede as condições de corrida que geram problema.

4. **Comente os seguintes critérios utilizados para avaliar uma solução para o problema da exclusão mútua: exclusão mútua. progresso e espera limitada no número de vezes.**<br/>
Exclusão mútua: jamais dois ou mais processos estarão na seção crítica.
Progresso: somente os processos interessados em entrar na seção crítica decidirão qual processo de fato vai entrar.
Espera limitada: deve existir um limite no número de vezes que outros processos acessam a seção crítica quando um processo está esperando para entrar nela.

5. **Explique a técnica de estrita alternância pra a implementação da exclusão mútua entre os processos. Ela atende os critérios de exclusão mútua, progresso e espera limitada? Comente cada um destes critérios em relação à estrita alternância.**<br/>
Cada processo tem a sua vez de entrar na seção crítica, onde é controlado pela variável `vez`. Processo P1 entra na seção crítica quando vez é igual a zero e P2 entra quando vez é igual a 1. Toda vez que o processo sai da seção crítica a vez muda de zero para um ou de um para zero. Atende exclusão mútua mas não o progresso e atende espera limitada sem ser número de vezes.

6. **Cite um argumento contra a implementação da exclusão mútua por bloqueio de processos.**<br/>
É necessário chamada no sistema para exclusão mútua e aumenta o potencial da troca de contexto, gerando overhead.

7. **Cite uma utilização de semáforos generalizados.** <br/>
Com semáforos generalizados, como é possível que se assumam valores negativos, o semáforo sempre é decrementado, tornando possível que se tenha controle de quantos processos estão bloqueados. Em semáforos normais, ao se truncar em zero o semáforo, não sabemos quantos processos estão bloqueados.

8. **O que são variáveis de condição e como elas são utilizadas.**<br/>
Variáveis de condição são variáveis utilizadas para ordenar a execução de diferentes processos. São duas as utilizações possíveis: `wait(var)`, usada para bloquear o processo em var e `signal(var)`, usada para acordar os processos bloqueados em var.

9. **Cite uma vantagem e uma desvantagem das primitivas não-bloqueadas de troca de mensagens.**<br/>
Vantagem: avançar mais rápido na execução.
Desvantagem: aumenta a complexidade do programa.

10. **Considere o problema do produtor-consumidor com um buffer de tamanho infinito. Neste caso, precisamos ainda controlar o número de mensagens no buffer? Por quê?** <br/>
Precisamos controlar o número mínimo somente, para o processo consumidor não retirar dados do buffer vazio. Já como numero máximo não precisamos nos preocupar uma vez que nunca se atingirá o limite.