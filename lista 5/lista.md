## Lista 5
## Exercícios

### Conteúdo: Deadlocks

1. **Considere um conjunto de processos P={P0, P1, ..., Pn} e um conjunto de recursos R={R0, R1, ..., Rm}. Cada recurso Ri pode ter várias instâncias Iri={Ii0, Ii1, ..., Iix}. Neste contexto, a presença de ciclos no grafo implica a ocorrência de deadlocks? (admita que as condições de exclusão mútua, posse e espera e não-preempção são observadas)**<br/>
![Ilustração 1](assets/1.png)

2. **É possível um deadlock que envolva um único processo?**<br/>

3. **Qual a maior diferença entre deadlock e starvation?**<br/>

4. **No modelo que considera os estados inseguros para a prevenção de deadlocks, todas as trajetórias são horizontais ou vericais, da esquerda para a direita. Exemplifique quando podemos obter trajetórias diagonais e trajetórias da direita para a esquerda.**<br/>
![Ilustração 2](assets/4.png)

5. **Um sistema pode estar em um estado que não seja nem um deadlock e nem um estado seguro? O que significa este estado?**<br/>

6. **Em um sistema com primitivas de comunicação entre processos SEND(processo, mensagem) e RECEIVE(processo, mensagem), onde o RECEIVE bloqueia o processo que o chamou se não houver mensagem para ele, pode haver deadlock? Se sim, exemplifique.**<br/>
