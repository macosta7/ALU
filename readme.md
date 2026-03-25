# Unidade Lógica e Aritmética (ULA) de 8 bits

&emsp; O projeto é o desenvolvimento de uma Unidade Lógica e Aritmétrica (ULA) de 8 bits utilizando o simulador Digital. A ULA é um dos componentes mais importantes, considerado como o coração do processador, ele é responsável por realizar operações aritmétricas e lógica dentro dele.

&emsp; O sistema foi construído utilizando uma arquitetura baseada em registradores, onde o Acumulador (AC) armazena os resultados principais e o MQ (Multiplier/Quotient) lida com operações estendidas de multiplicação e divisão. O operando de entrada é representado por N.

## Operações Implementadas

### Soma
**Operação:** AC + N -> AC (8 bits)

&emsp; Para a implementação da soma, comecei construindo a tabela verdade para a soma de 1 bit, que inclui as entradas A, B e o Carry In (Cin), e as saídas Sum e Carry Out (Cout). Com base na tabela, realizei 2 mapas de Karnaugh para conseguir as expressões de Sum e Cout.

<img src="assets/tabela-verdade-soma.jpeg" alt="Tabela Verdade da Soma" width="400">

&emsp; As expressões obtidas foram:
- Sum = A XOR B XOR Cin
- Cout = (A AND B) OR (Cin AND A) OR (Cin AND B)

&emsp; Depois de encontrar as expressões, construi um somador de 1 bit utilizando: três entradas (A, B, Cin) e duas saídas (Sum, Cout). Assim adicionei uma porta lógica XOR e três portas AND para obter o resultado da soma.

<img src="assets/soma-1-bit.png" alt="Somador de 1 bit" width="400">

&emsp; Apartir do somador de 1 bit, salvei ele com um componente e para construir o somador de 8 bits, utilizei 8 somadores de 1 bit que são interligados, onde o primeiro somador recebe o terra como Carry In (Cin) e o Carry Out (Cout) é conectado ao Carry In (Cin) do próximo somador, e assim por diante até o último somador. Então, o resultado da soma de 8 bits é obtido a partir dos Sum de cada somador e o Carry Out do último somador.

<img src="assets/soma-8-bits.png" alt="Somador de 8 bits" width="400">

### Subtração
**Operação:** AC - N -> AC (8 bits)

&emsp; Para a implementação da subtração, comecei construindo a tabela verdade para a subtração de 1 bit, que inclui as entradas A, B e o Borrow In (Bin), e as saídas Diff e Borrow Out (Bout). Com base na tabela, realizei 2 mapas de Karnaugh para conseguir as expressões de Diff e Bout.

<img src="assets/tabela-verdade-subtracao.jpeg" alt="Tabela Verdade da Subtração" width="400">

&emsp; As expressões obtidas foram:
- Diff = A XOR B XOR Bin
- Bout = (NOT A AND B) OR (Bin AND NOT A) OR (Bin AND B)

&emsp; Depois de encontrar as expressões, construí um subtrator de 1 bit utilizando: três entradas (A, B, Bin) e duas saídas (Diff, Bout). No sistema, adicionei uma porta lógica XOR e três portas AND, em duas delas adicionei uma porta NOT para que a entrada A seja invertida, assim obtendo o resultado da subtração.

<img src="assets/subtrator-1-bit.png" alt="Subtrator de 1 bit" width="400">

&emsp; A partir do subtrator de 1 bit, salvei ele com um componente e para construir o subtrator de 8 bits, utilizei 8 subtratores de 1 bit que são interligados, onde o primeiro subtrator recebe o terra como Borrow In (Bin) e o Borrow Out (Bout) é conectado ao Borrow In (Bin) do próximo subtrator, e assim por diante até o último subtrator. Então, o resultado da subtração de 8 bits é obtido a partir dos Diff de cada subtrator e o Borrow Out do último subtrator.

<img src="assets/subtrator-8-bits.png" alt="Subtrator de 8 bits" width="400">

### Multiplicação
**Operação:** AC * N -> AC (8 LSB) e MQ (8 MSB)

### Divisão
**Operação:** AC / N -> AC (Resto) e MQ (Quociente)

### Shift Lógico à Esquerda
**Operação:** AC -> AC (8 bits)

&emsp; Para a implementação do shift lógico à esquerda, utilizei um componente de 8 bits onde cada bit é conectado ao próximo bit, ou seja, o bit 0 da entrada é conectado ao bit 1 da saída, o bit 1 da entrada é conectado ao bit 2 da saída, e assim por diante, até o bit 6 da entrada que é conectado ao bit 7 da saída. O bit 0 da saída é conectado ao terra, pois no shift lógico à esquerda, o bit mais à direita é preenchido com zero.

<img src="assets/shift-esquerda.png" alt="Shift Lógico à Esquerda" width="400">

&emsp; O resultado do shift lógico à esquerda resulta no dobro do valor colocado na entrada, isso porque cada bit é deslocado para a esquerda, o que equivale a multiplicar o valor por 2. Por exemplo, se a entrada for 00000001 (1 em decimal), o resultado do shift lógico à esquerda será 00000010 (2 em decimal). Se a entrada for 00000010 (2 em decimal), o resultado será 00000100 (4 em decimal), e assim por diante.

### Shift Lógico à Direita
**Operação:** AC -> AC (8 bits)

&emsp; Para a implementação do shift lógico à direita, utilizei um componente de 8 bits onde cada bit é conectado ao próximo bit, ou seja, o bit 7 da entrada é conectado ao bit 6 da saída, o bit 6 da entrada é conectado ao bit 5 da saída, e assim por diante, até o bit 1 da entrada que é conectado ao bit 0 da saída. O bit 7 da saída é conectado ao terra, pois no shift lógico à direita, o bit mais à esquerda é preenchido com zero.

<img src="assets/shift-direita.png" alt="Shift Lógico à Direita" width="400">

&emsp; O resultado do shift lógico à direita resulta na metade do valor colocado na entrada, isso porque cada bit é deslocado para a direita, o que equivale a dividir o valor por 2. Por exemplo, se a entrada for 00000010 (2 em decimal), o resultado do shift lógico à direita será 00000001 (1 em decimal). Se a entrada for 00000100 (4 em decimal), o resultado será 00000010 (2 em decimal), e assim por diante.

### NAND
**Operação:** AC NAND N -> AC (8 bits)

&emsp; Para a implementação da operação NAND, utilizei duas entradas (A e B) então liguei essas entradas em uma porta lógica NAND e a saída da porta NAND é conectada na saída S.

<img src="assets/nand2.png" alt="NAND" width="400">

&emsp; O resultado da operação NAND é o inverso da operação AND. Ou seja, se ambos os bits de A e N forem 1, o resultado será 0, caso contrário, o resultado será 1. Por exemplo, se A for 00000011 (3 em decimal) e N for 00000001 (1 em decimal), o resultado da operação NAND será 11111110 (254 em decimal), pois apenas o bit 0 de A e N são ambos 1, resultando em um bit 0 na saída, enquanto os outros bits resultam em 1.

### XOR
**Operação:** AC XOR N -> AC (8 bits)

&emsp; Para a implementação da operação XOR, utilizei duas entradas (A e B) então liguei essas entradas em uma porta lógica XOR e a saída da porta XOR é conectada na saída S.

<img src="assets/xor2.png" alt="XOR" width="400">

&emsp; O resultado da operação XOR é 1 se os bits de A e N forem diferentes, e 0 se forem iguais. Por exemplo, se A for 00000011 (3 em decimal) e N for 00000001 (1 em decimal), o resultado da operação XOR será 00000010 (2 em decimal), pois apenas o bit 0 de A e N são diferentes, resultando em um bit 1 na saída, enquanto os outros bits resultam em 0.

## Link do Video