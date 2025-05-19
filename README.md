### [Philosophers](/philosophers)

<img src="assets/philosopherse.png" alt="philosophers" style="width: 100px; vertical-align: middle;padding-bottom: 8px;" />

> &nbsp; &nbsp; &nbsp;
>
> -   **Objetivo**: O projeto Philosophers é um exercício de programação voltado ao estudo e à aplicação prática de conceitos de **concorrência e sincronização em sistemas operacionais**. Inspirado no clássico problema dos "Filósofos Jantando", o projeto busca implementar uma solução eficiente e segura para gerenciar o acesso concorrente a recursos limitados (garfos) por múltiplas **threads (filósofos)**, evitando **condições de corrida (race conditions)**, **deadlocks e fomes (starvation)**, e garantindo a integridade do sistema durante a execução simultânea das threads.
> -   **Habilidades**:
>       - Programação concorrente e paralela  
>       - Prevenção de deadlocks e starvation  
>       - Sincronização com mutexes e controle de acesso a recursos críticos  
>       - Criação e gerenciamento de threads  
>       - Uso de estruturas de monitoramento para detectar estados críticos  
>       - Manipulação precisa de tempo com `gettimeofday`, `usleep` e controle de tempo absoluto
>
> &nbsp; &nbsp; &nbsp;

### Clonar o repositório
```bash
git clone link do repositório
cd philosophers
```
### Compilar o projeto
```bash
make 
```
### Executar o programa
```bash
./philo <número_de_filósofos> <tempo_para_morrer> <tempo_para_comer> <tempo_para_dormir> [opcional:número_de_vezes_que_cada_filósofo_deve_comer]
```

### Valgrind e Helgrind
Valgrind é uma ferramenta poderosa para depuração de memória e análise de desempenho em programas C/C++. Ele pode ser usado para detectar vazamentos de memória, erros de acesso à memória e problemas de concorrência.
valgrind --tool=helgrind ./deadlock
```bash
valgrind --tool=helgrind ./philo 5 800 400 400
```
### Sanitizers
Saniteze thread é uma opção do compilador que ativa a verificação de concorrência em tempo de execução. Ele ajuda a detectar problemas como condições de corrida, deadlocks e uso incorreto de mutexes durante a execução do programa.

```bash
gcc -Wall -Wextra -Werror -pthread -fsanitize=thread -g -o philo philo.c
./philo 5 800 400 400
```


</br> </br> </br>

### Threads, Mutex, Race conditions, deadlocks, starvation, sincronização
_Conceitos com exemplos do projeto Philosoph_

**- Threads**
Threads são unidades de execução dentro de um processo que compartilham o mesmo espaço de memória.</br>
Exemplo:
Cada filósofo é implementado como uma thread independente, que executa seu próprio ciclo de ações (pensar, pegar garfos, comer, dormir). Todas essas threads compartilham os mesmos recursos (ex: array de garfos/mutexes), o que exige coordenação cuidadosa para evitar erros.

**- Mutex (Mutual Exclusion)**
Um mutex é um mecanismo de sincronização que garante que apenas uma thread acesse um recurso compartilhado por vez, prevenindo race conditions.</br>
Exemplo:
Cada garfo é protegido por um mutex. Quando um filósofo tenta comer, ele precisa bloquear os dois mutexes correspondentes aos garfos à sua esquerda e à sua direita. Isso evita que outro filósofo use os mesmos garfos ao mesmo tempo, garantindo o acesso exclusivo e seguro.


**- Race condition**
Ocorre quando o resultado do programa depende da ordem de execução das threads acessando recursos compartilhados sem sincronização adequada.</br>
Exemplo:
Dois filósofos tentam escrever no terminal ao mesmo tempo:
```c
printf("Filósofo 2 está comendo\n");
printf("Filósofo 3 está pensando\n");
```


**- Deadlock**
Situação em que dois ou mais filósofos esperam indefinidamente por recursos (garfos) bloqueados uns pelos outros.</br>
Exemplo:
Todos os filósofos pegam o garfo da esquerda e ficam esperando o da direita. Nenhum libera o recurso:
```c
pthread_mutex_lock(&garfo_esquerda);
// esperando eternamente pelo garfo_direita...
```


**- Starvation**
Ocorre quando uma thread não consegue acessar um recurso compartilhado por um período prolongado, geralmente devido a outras threads monopolizando o recurso, resultando em espera infinita.</br>
Exemplo:
O filósofo 4 nunca obtém os dois garfos porque os filósofos 3 e 5 sempre comem antes dele, gerando fome infinita.



**- Sincronização**
A sincronização é o processo de coordenar o acesso a recursos compartilhados entre threads para evitar condições de corrida, deadlocks e starvation. Isso pode ser feito usando mutexes, semáforos ou outras estruturas de controle de concorrência.
Exemplo:
```c
pthread_mutex_lock(&fork[i]);
pthread_mutex_lock(&fork[(i + 1) % n]);
// seção crítica: filósofo come
pthread_mutex_unlock(&fork[i]);
pthread_mutex_unlock(&fork[(i + 1) % n]);
```
