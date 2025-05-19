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
