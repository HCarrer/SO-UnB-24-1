## Lista 5
## Exercícios

### Conteúdo: Deadlocks

1. **Considere um conjunto de processos P={P0, P1, ..., Pn} e um conjunto de recursos R={R0, R1, ..., Rm}. Cada recurso Ri pode ter várias instâncias Iri={Ii0, Ii1, ..., Iix}. Neste contexto, a presença de ciclos no grafo implica a ocorrência de deadlocks? (admita que as condições de exclusão mútua, posse e espera e não-preempção são observadas)**<br/>
![Ilustração 1](./assets/1.png)
Sim, pois pode ocorrer de uma instância do recurso R1 estar alocada pelo processo P1 e outra instância estar alocada por P2. P2, por sua parte, deseja alocar o recurso R2, que está alocado pelo processo P3, o qual deseja alocar uma instância do recurso R1, gerando assim um ciclo no grafo.

2. **É possível um deadlock que envolva um único processo?**<br/>
Sim, por exemplo no trecho de código abaixo
```
for(i=0; i<2; i++>)
  a[i] = obtem(R1);
```

3. **Qual a maior diferença entre deadlock e starvation?**<br/>
No deadlock os processos estão esperando por recursos que nunca serão liberados, já no starvation os processos estão esperando recursos que serão liberados em tempo indefinido.

4. **No modelo que considera os estados inseguros para a prevenção de deadlocks, todas as trajetórias são horizontais ou vericais, da esquerda para a direita. Exemplifique quando podemos obter trajetórias diagonais e trajetórias da direita para a esquerda.**<br/>
![Ilustração 2](./assets/4.png)

Retas diagonais: multicore
Direita para esquerda: rollback

5. **Um sistema pode estar em um estado que não seja nem um deadlock e nem um estado seguro? O que significa este estado?**<br/>
Sim. O sistema pode estar em estado inseguro, o que levará ao deadlock futuramente, onde o sistema não pode garantir que todas as requisições pendentes serão atendidas.

6. **Em um sistema com primitivas de comunicação entre processos SEND(processo, mensagem) e RECEIVE(processo, mensagem), onde o RECEIVE bloqueia o processo que o chamou se não houver mensagem para ele, pode haver deadlock? Se sim, exemplifique.**<br/>
Sim, um exemplo disso seria o seguinte:
```
Processo A        |    Processo B         |     
__________________|_______________________|
                  |                       |
send(A, msg)      |                       |   processo A envia mensagem para o processo B
                  |    receive(B, msg)    |   processo B tenta receber mensagem de A antes de ela chegar, o que bloqueia B enquanto a mensagem não chega
receive(A, msg)   |                       |   processo A tenta receber mensagem de B, mas como B está bloqueado, a mensagem não chega, o que bloqueia A
                  |                       |   ambos os processos estão agora bloqueados esperando que o outro processo envie uma mensagem
```