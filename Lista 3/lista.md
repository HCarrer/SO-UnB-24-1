## Lista 3
## Exercícios

### Conteúdo: Concorrência

1. **Mostre que o algoritmo de Hyman não garante a exclusão mútua. Para tanto, admita dois processos P0 e P1, com variáveis locais (i=0, j=1) e (i=1, j=0), respectivamente. As variáveis turn, flag[0] e flag[1] são compartilhadas.**
```
while(TRUE)
{
  flag[i] = TRUE;
  while(turn != i)
  {
    while(flag[j] == TRUE);
    turn = i;
  }
  secao_critica();
  flag[i] = FALSE;
  secao_nao_critica();
}
```

**Resolução**
