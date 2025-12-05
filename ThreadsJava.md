# Introdução a Threads em Java

#### O que são threads?
Threads são fluxos de execução independentes dentro de um processo. Imagine-as como tarefas que podem ser executadas em paralelo, aumentando a performance de suas aplicações.

#### Por que usar threads?
* **Paralelismo:** Execute múltiplas tarefas simultaneamente.
* **Responsividade:** Mantenha a interface do usuário responsiva enquanto tarefas em segundo plano são executadas.
* **Aproveitamento de múltiplos núcleos:** Utilize toda a capacidade de processamento do seu computador.

#### Quando não usar threads?
* **Problemas simples:** Para tarefas simples e sequenciais, threads podem adicionar complexidade desnecessária.
* **Overhead:** A criação e gerenciamento de threads exigem recursos do sistema.

#### Threads em Java
A classe `Thread` em Java oferece a base para a programação concorrente.
* **Criando threads:**
  * **Extendendo Thread:**
    ```java
    class MinhaThread extends Thread {
        public void run() {
            // Código da thread
        }
    }
    ```
    
  * **Implementando Runnable:**
    ```java
    class MinhaTarefa implements Runnable {
        public void run() {
            // Código da thread
        }
    }
    ```
    
  * **Iniciando threads:**
    ```java
    Thread t = new Thread(tarefa);
    t.start();
    ```

#### Quando Usar o "Kill"?
* **Programas travados:** Quando um programa para de responder e não pode ser encerrado de forma normal.
* **Emergências:** Em situações críticas, onde é necessário interromper a execução de um programa imediatamente.

#### Quando usar CTRL+C (Sinais)?
##### Funcionamento:
Ao pressionar a combinação de teclas CTRL+C em um terminal onde um programa Java está em execução, você está enviando um sinal de interrupção (SIGINT) para o processo. Esse sinal, por padrão, informa ao processo que ele deve interromper sua execução de forma ordenada.
##### Como o Java lida com o sinal SIGINT?
A Máquina Virtual Java (JVM) captura esse sinal e o trata de acordo com a configuração e a implementação. Por padrão, a JVM encerra todos os threads em execução e finaliza o programa. É possível personalizar o comportamento do programa ao receber o sinal SIGINT, utilizando mecanismos como try-with-resources e ShutdownHook.
##### Limitações do CTRL+C:
Em alguns casos, o programa pode levar algum tempo para responder ao sinal de interrupção e finalizar. Se o programa estiver bloqueado em uma operação de E/S ou em um loop infinito sem verificação de interrupções, o CTRL+C pode não ser eficaz.
##### Cenários Comuns para Usar o CTRL+C:
** **Script em execução:** Se você executar um script shell ou um programa diretamente no terminal, pressionar CTRL+C geralmente envia um sinal de interrupção (SIGINT) para o processo, solicitando que ele pare sua execução.
** **Comandos longos:** Se um comando estiver em execução e você quiser interromper sua execução, CTRL+C é uma forma rápida de fazer isso.
** **Loops infinitos:** Se um programa entrar em um loop infinito e não responder a outros comandos, CTRL+C pode ser a única maneira de interromper sua execução.
** **Testes e depuração:** Durante o desenvolvimento, você pode usar CTRL+C para interromper um programa em um ponto específico para inspecionar variáveis, depurar o código ou simular cenários de erro.

#### Quando usar ShutdownHook?
* **Aplicações com longa duração:** Servidores, daemons e aplicações que rodam por longos períodos.
* **Aplicações que utilizam recursos externos:** Conexões de banco de dados, arquivos, sockets, etc.
* **Aplicações que precisam realizar tarefas de limpeza antes de serem encerradas:** Liberar locks, salvar dados em disco, etc.
 
# Atividade Prática - Criando uma nova Thread em Java:
#### Objetivo:
* Compreender os conceitos básicos de threads em Java;
* Implementar threads para executar tarefas em paralelo;
* Compreender o comportamento de threads em Java e o impacto do método yield().
* Analisar a saída de programas concorrentes e identificar padrões de execução.
* Identificar as diferenças entre as duas implementações.

#### Ao final você será capaz de:
* **Demonstrar:** Compreensão dos conceitos de threads e encerramento.
* **Analisar:** Resultados de experimentos e identificar padrões.
* **Comparar:** Diferentes abordagens para programação concorrente.
* **Justificar:** Suas escolhas com base em argumentos técnicos.

#### Tarefas:
* **Execução paralela de threads:** [ThreadsConcorrenteInfinitas.java](https://github.com/anapaulacostacurta-ifpr/Sistemas_Distribuidos/blob/main/conteudos/ThreadsJava/ThreadsConcorrenteInfinitas.java);
* **Implementação e Execução paralela de threads com ShutdownHook:** [ThreadsConcorrenteShutdownHook.java](https://github.com/anapaulacostacurta-ifpr/Sistemas_Distribuidos/blob/main/conteudos/ThreadsJava/ThreadsConcorrenteShutdownHook.java);
* **Execução paralela de threads com yield:** [ThreadsConcorrenteInterrupet.java](https://github.com/anapaulacostacurta-ifpr/Sistemas_Distribuidos/blob/main/conteudos/ThreadsJava/ThreadsConcorrenteInterrupet.java);

## Procedimento

### Compilação:
* Salve os arquivo em seu repositório github (ThreadsConcorrenteInfinitas.java, ThreadsConcorrenteShutdownHook.java e ThreadsConcorrenteInterrupet.java). 
* Utilize um compilador Java (javac) para compilar cada classe:
  ```bash
  javac ThreadsConcorrenteInfinitas.java
  Javac ThreadsConcorrenteShutdownHook.java
  javac ThreadsConcorrenteInterrupet.java
  ```

### Execução 1 - Threads com loop infinito:
* **Ordem de execução:** Ao executar esses comandos, você provavelmente verá uma mistura dos caracteres 'A' e 'B' sendo impressos na tela de forma aleatória, a ordem em que os comandos são executados não garante que as threads dentro de cada programa sejam executadas em uma ordem específica. Isso dependerá do escalonador do sistema operacional e de outros fatores.
* **Saída:** A saída de cada programa será exibida na tela do terminal, a menos que você redirecione a saída para um arquivo, como nos exemplos anteriores.
* **Encerramento:** Pressionar CTRL+C é uma forma rápida e simples de interromper a execução de um programa Java. No entanto, para garantir um encerramento limpo e ordenado, é recomendado utilizar mecanismos como ShutdownHook e tratar o sinal de interrupção de forma personalizada. A escolha do método de encerramento dependerá das necessidades específicas de cada aplicação.
* Execute a classe principal:
   ```bash
   java ThreadsConcorrenteInfinitas
   ```
* Pressione CTRL+C;

### Execução 2 - Threads com loop infinito e geração de arquivo de log de execução:
* Execute a classe principal novamente em backgroud:
   ```bash
   java ThreadsConcorrenteInfinitas > ThreadsConcorrenteInfinitas_$(date +%Y%m%d_%H%M%S).log & 
   ```
* Executar o comando: kill -SIGINT <PID>;

### Execução 3 - Threads com ShutdownHook:
* **Explicação Detalhada**: Uma variável AtomicBoolean é utilizada para controlar a execução das threads de forma atômica, evitando problemas de concorrência. O ShutdownHook é registrado utilizando Runtime.getRuntime().addShutdownHook(). Quando a JVM está prestes a ser encerrada, este hook é executado. Dentro do ShutdownHook, a variável running é definida como false, sinalizando para as threads que devem parar sua execução.
* **Ao pressionar CTRL+C** para interromper o programa, as threads serão encerradas de forma ordenada e a mensagem "Encerrando threads Concorrente com ShutdownHook..." será exibida.
* **Vantagens do ShutdownHook:** Evita vazamentos de recursos e garante que as threads sejam finalizadas corretamente. Permite realizar tarefas de limpeza, como fechar arquivos ou conexões de banco de dados. Pode ser personalizado para atender a diferentes necessidades de encerramento.
* Execute a classe principal:
   ```bash
   java ThreadsConcorrenteShutdownHook
   ```
* Pressione CTRL+C;
 
### Execução 4 - Threads com interrupt e geração de arquivo de log de execução:
* **Sinalização:** Quando uma thread é interrompida, ela recebe um sinal de interrupção. É importante verificar esse sinal dentro do loop para decidir se deve continuar a execução.
* **Controle do tempo:** No exemplo, foi adicionado um atraso para simular uma tarefa que leva algum tempo. Em um cenário real, você pode usar outros mecanismos para controlar o tempo de execução das threads.
* Execute a classe principal direncionado a saída para um arquivo de log:
   ```bash
   java ThreadsConcorrenteInterrupet > ThreadsConcorrenteInterrupet_$(date +%Y%m%d_%H%M%S).log
   ```
* Aguarde o encerramento da execução

### Execução 5 - Threads com interrupt, geração de arquivo de log de execução e Encerramento com Kill:
* **Sinalização:** Quando uma thread é interrompida, ela recebe um sinal de interrupção. É importante verificar esse sinal dentro do loop para decidir se deve continuar a execução.
* **Controle do tempo:** No exemplo, foi adicionado um atraso para simular uma tarefa que leva algum tempo. Em um cenário real, você pode usar outros mecanismos para controlar o tempo de execução das threads.
* Execute a classe principal direncionado a saída para um arquivo de log:
   ```bash
   java ThreadsConcorrenteInterrupet > ThreadsConcorrenteInterrupet_$(date +%Y%m%d_%H%M%S).log &
   ```
* Executar o comando no kill -SIGINT <PID>

### Análise dos Resultados:
* **Execução paralela em ThreadsConcorrenteInfinitas.java:** As threads devem executar suas tarefas de forma concorrente, sem uma ordem específica. Como executa em Loop infinito e o terminal fica bloqueado com a execução precisamos precionar CTRL+C para encerrar a execução. Se a Execução for realizada com "&" é necessário executar o comando kill para encerrar o processo.
* **Execução paralela em ThreadsConcorrenteShutdownHook.java:** Ao pressionar CTRL+C ou kill para interromper o programa, as threads serão encerradas de forma ordenada e a mensagem "Encerrando threads Concorrente com ShutdownHook..." será exibida.
* **Execução Método yield() em ThreadsConcorrenteInterrupet.java:** O método yield() sugere ao escalonador que permita que outra thread com a mesma prioridade seja executada. No entanto, não há garantia de que outra thread será imediatamente selecionada. O programa executa por um tempo e depois encerrada. Pode ser encerrado a execução antecipada utilizando CTRL+C ou o comando Kill.

### Orientações para responder a atividade:
* Deve ser criado um repositório no github para essa atividade;
* Realizar o upload dos arquivos ThreadsConcorrenteInfinitas.java, ThreadsConcorrenteShutdownHook e ThreadsConcorrenteInterrupet.java;
* Criar um Codespace no github para realizar a execução em terminal;
* Realizar as cinco execuções no seu codespace do github;
* Após as execuções no codespace, realizar o commit dos três arquivos para seu repositório no github: ThreadsConcorrenteInfinitas.java, ThreadsConcorrenteShutdownHook e ThreadsConcorrenteInterrupet.java;
* Realizar os print das cinco execução dos programas, na imagem deve consta o nome do usuário do github que executou a atividade.
* Realizar o upload os prints de execução das três execuções em seu repositório;
* Enviar o link do seu github, onde contem os códigos executados e as logs de execução. O Envio do link deverá ser realizado exclusivamente pelo formulário do Google Sala de Aula.
  
## Perguntas para reflexão - Você deve responder a perguntas abaixo no formulário no Google Sala de aula: 
#### Analisando os resultados das cinco execuções, descreva detalhadamente as diferenças observadas no comportamento das threads, considerando os seguintes aspectos:
* **Ordem de execução:** Houve alguma ordem previsível na execução das threads? Por quê?
* **Efeito do método yield():** O método yield() influenciou a ordem de execução das threads? Explique o porquê.
* **Influência do CTRL+C:** Como o sinal de interrupção (CTRL+C) afetou a execução dos programas? Houve alguma diferença no comportamento entre os programas?
* **Comparação entre as implementações:** Quais são as principais diferenças entre as três implementações e quais as vantagens e desvantagens de cada uma?
* **Comparação entre execuções:** Quais são as principais diferenças entre as cinco execuções e quais as vantagens e desvantagens de cada uma?
