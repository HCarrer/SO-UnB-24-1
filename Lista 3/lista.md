## Lista 3
## Exercícios

### Conteúdo: Concorrência

1. **Mostre que o algoritmo de Hyman não garante a exclusão mútua. Para tanto, admita dois processos P0 e P1, com variáveis locais (i=0, j=1) e (i=1, j=0), respectivamente. As variáveis turn, flag[0] e flag[1] são compartilhadas.**
```
1  | while(TRUE)
2  | {
3  |   flag[i] = TRUE;
4  |   while(turn != i)
5  |   {
6  |     while(flag[j] == TRUE) {};
7  |     turn = i;
8  |   }
9  |   secao_critica();
10 |   flag[i] = FALSE;
11 |   secao_nao_critica();
12 | }
```

**Resolução**
Iniciando-se com o processo P1, temos a seguinte sequência de eventos:
```
Linha executada em P0 | Linha executada em P1 |
                      |          3            | `flag[1]` = TRUE
                      |          4            | entra no loop -> `turn` == 0 e `i` == 1
                      |          6            | executa verificação mas não entra no loop -> `flag[0]` == TRUE
                      |          -            | quantum logo após a linha 6
         3            |                       | `flag[0]` = TRUE
         4            |                       | executa verificação mas não entra no loop -> `turn` == 0 e `i` == 0
         9            |                       | *entra na seção crítica*
         -            |                       | quantum na seção crítica
                      |         7             | `turn` = 1
                      |         9             | *entra na seção crítica*
```

Como os dois processos entraram na seção crítica ao mesmo tempo nesta situação, isto fere o princípio da exclusão mútua, não garantindo-a assim sempre.