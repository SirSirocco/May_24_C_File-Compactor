# May_24_C_File-Compactor

[🇧🇷 Leia em Português](#português) | [🇺🇸 Read in English](#english)

## Português

**Data:** Maio, 2024

**Autores:**

- Pedro de Almeida Barizon
- Guilherme Riechert Senko

## RELATÓRIO DE IMPLEMENTAÇÃO DE COMPACTAÇÃO E DESCOMPACTAÇÃO USANDO CÓDIGOS LIVRES DE PREFIXO

### INTRODUÇÃO

Este trabalho foi desenvolvido para a disciplina de Software Básico com o objetivo de implementar um sistema de compactação e descompactação de texto usando códigos livres de prefixo. Este método permite uma compressão de dados sem perda utilizando códigos de comprimento variável — cuja eficiência sobressai especialmente em contextos em que certos símbolos aparecem com mais frequência do que outros.

### METODOLOGIA

A estrutura principal utilizada foi a compactadora, que mapeia cada símbolo a um código binário e ao tamanho desse código.

```c
struct compactadora {
    char simbolo;
    unsigned int codigo;
    int tamanho;
};
```

### FUNÇÕES IMPLEMENTADAS

- `compacta(FILE *arqTexto, FILE *arqBin, struct compactadora *v)`: Compacta o texto lido de arqTexto usando a tabela fornecida em forma de vetor e grava o resultado binário em arqBin.
- `descompacta(FILE *arqBin, FILE *arqTexto, struct compactadora *v)`: Lê o binário de arqBin e reconstrói o texto original em arqTexto usando a tabela fornecida.

### TESTES IMPLEMENTADOS

Para assegurar a eficácia e a eficiência das funções de compactação e descompactação implementadas, realizamos uma série de testes rigorosos. Cada teste foi projetado para avaliar aspectos específicos da funcionalidade e robustez das operações.

#### 1. Teste de Compactação Básica

- **Objetivo:** Verificar a capacidade da função compacta de transformar corretamente um texto simples em sua forma binária usando o código fornecido no enunciado.
- **Procedimento:** Utilizamos uma string definida como "A, B, C, ..., Z\n" para representar uma sequência simples e previsível.
- **Verificação:** Após a compactação, fizemos um dump do arquivo binário resultante e comparamos manualmente este output com a saída esperada segundo a tabela fornecida no enunciado.

#### 2. Teste de Descompactação e Integridade

- **Objetivo:** Assegurar que a função descompacta pode reverter o processo de compactação, restaurando o texto original a partir do binário.
- **Procedimento:** Após a compactação dos dados, utilizamos a função descompacta para recriar o texto a partir do binário gerado e comparar com o texto original.
- **Verificação:** A saída de texto foi verificada para corresponder exatamente ao texto de entrada, garantindo a integridade dos dados.

#### 3. Testes com Diferentes Padrões de Texto

- **Objetivo:** Testar a robustez das funções com diferentes padrões de texto que incluem repetições e espaços, como em "\n\nAABBCCDD...,,\n\n".
- **Procedimento:** Compactamos e descompactamos este texto complexo para verificar se os códigos sem prefixos tratam corretamente os símbolos e espaços repetidos.
- **Verificação:** Analisamos o texto descompactado para confirmar que todos os caracteres e símbolos estavam corretamente posicionados e representados.

#### 4. Teste com Arquivos de Texto Reais

- **Objetivo:** Avaliar o desempenho das funções em um cenário de uso mais realista, usando arquivos de texto de maior porte.
- **Procedimento:** Utilizamos arquivos de texto como o "BOM\nDIA\n" e um texto mais longo de 30 linhas para testar a compactação e descompactação.
- **Verificação:** O foco estava em verificar a eficiência da compactação em termos de tamanho do arquivo e a precisão da descompactação.

#### 5. Teste de Conformidade com o Enunciado

- **Objetivo:** Garantir que as implementações seguem as especificações dadas no enunciado do trabalho, utilizando os códigos e estruturas fornecidos.
- **Procedimento:** Seguimos estritamente as instruções e o exemplo de código do enunciado para desenvolver e testar as funções.
- **Verificação:** A implementação foi revisada para assegurar que todas as especificações do enunciado foram cumpridas, incluindo a maneira correta de abertura e manuseio dos arquivos.

#### 6. Teste com Tabela Qualquer

- **Objetivo:** Garantir que as funções operam com sucesso independentemente da tabela de códigos livres de prefixo fornecida.
- **Procedimento:** Definimos uma tabela diferente da fornecida pelo enunciado. Em seguida, compactamos "LUKE, EU SOU SEU PAI\n", vindo de um arquivo de texto, e fizemos um dump do binário gerado. Logo após, descompactamo-lo, escrevendo o resultado em um outro arquivo de texto.
- **Verificação:** Verificamos tanto que o dump correspondia ao esperado quanto que o conteúdo de ambos os arquivos de texto era idêntico, o que atestou o bom desempenho das funções envolvidas.
- **Observação**: O método empregado para definir os códigos sem prefixos foi dos mais simples: consideramos a árvore de prefixos mais desbalanceada possível, de modo que todo nó à esquerda fosse uma folha. Dessa forma, foram gerados os códigos 0, 10, 110, 1110, e assim sucessivamente, que correspondem às somas 2^(n + 1) – 2, com n natural. Tal propriedade facilitou a criação da tabela de compactação.

Estes testes, todos exitosos, foram essenciais para confirmar que tanto a compactação quanto a descompactação funcionam de maneira confiável e eficiente, tratando diferentes tipos de entrada e garantindo a integridade dos dados após o processo.

### CONCLUSÃO

A implementação do algoritmo para compactação e descompactação de textos em C alcançou sucesso, atendendo a todos os requisitos e objetivos estabelecidos pelo enunciado do trabalho. Os resultados obtidos nas diversas fases de teste demonstram a eficiência do algoritmo em compressão de dados sem perda, validando a escolha de técnicas de codificação livre de prefixo para este propósito.

## English

**Date:** May, 2024

**Authors:**

- Pedro de Almeida Barizon
- Guilherme Riechert Senko

## IMPLEMENTATION REPORT: TEXT COMPRESSION AND DECOMPRESSION USING PREFIX-FREE CODES

### INTRODUCTION

This project was developed for the Basic Software course with the goal of implementing a text compression and decompression system using prefix-free codes. This method enables lossless data compression using variable-length codes, particularly efficient in contexts where certain symbols appear more frequently than others.

### METHODOLOGY

The main structure used was the `compactadora`, which maps each symbol to a binary code and its length.

```c
struct compactadora {
    char simbolo;
    unsigned int codigo;
    int tamanho;
};
```

### IMPLEMENTED FUNCTIONS

- `compacta(FILE *arqTexto, FILE *arqBin, struct compactadora *v)`: Compresses the text read from `arqTexto` using the provided table (in vector form) and writes the binary result to `arqBin`.
- `descompacta(FILE *arqBin, FILE *arqTexto, struct compactadora *v)`: Reads the binary data from `arqBin` and reconstructs the original text in `arqTexto` using the provided table.

### IMPLEMENTED TESTS

To ensure the effectiveness and efficiency of the implemented compression and decompression functions, we conducted a series of rigorous tests. Each test was designed to evaluate specific aspects of the functionality and robustness of the operations.

#### 1. Basic Compression Test

- **Objective:** Verify the ability of the `compacta` function to correctly transform simple text into its binary form using the code provided in the assignment.
- **Procedure:** A predefined string "A, B, C, ..., Z\n" was used to represent a simple and predictable sequence.
- **Verification:** After compression, the resulting binary file was dumped and manually compared to the expected output according to the table provided in the assignment.

#### 2. Decompression and Integrity Test

- **Objective:** Ensure that the `descompacta` function can reverse the compression process, restoring the original text from the binary data.
- **Procedure:** After data compression, the `descompacta` function was used to recreate the text from the generated binary and compare it to the original text.
- **Verification:** The decompressed text was verified to match the input text exactly, ensuring data integrity.

#### 3. Tests with Different Text Patterns

- **Objective:** Test the robustness of the functions with different text patterns, including repetitions and spaces, such as "\n\nAABBCCDD...,\n\n".
- **Procedure:** This complex text was compressed and decompressed to verify that prefix-free codes correctly handled repeated symbols and spaces.
- **Verification:** The decompressed text was analyzed to confirm that all characters and symbols were correctly positioned and represented.

#### 4. Real Text File Tests

- **Objective:** Evaluate the performance of the functions in a more realistic usage scenario using larger text files.
- **Procedure:** Text files like "BOM\nDIA\n" and a longer text with 30 lines were used to test compression and decompression.
- **Verification:** The focus was on verifying the compression efficiency in terms of file size and the accuracy of the decompression.

#### 5. Compliance Test with the Assignment

- **Objective:** Ensure the implementations follow the specifications outlined in the assignment, using the provided codes and structures.
- **Procedure:** The instructions and example code from the assignment were strictly followed during development and testing.
- **Verification:** The implementation was reviewed to ensure that all the specifications were met, including the correct way to open and handle files.

#### 6. Test with Custom Table

- **Objective:** Ensure that the functions operate successfully regardless of the prefix-free code table provided.
- **Procedure:** A table different from the one provided in the assignment was defined. The text "LUKE, I AM YOUR FATHER\n" from a text file was compressed, and the resulting binary was dumped. It was then decompressed, and the result was written to another text file.
- **Verification:** Both the binary dump and the content of the text files were verified to ensure that the functions performed as expected.
- **Observation:** The method used to define the prefix-free codes was straightforward: the most unbalanced prefix tree possible was considered, with every left node being a leaf. This generated codes like 0, 10, 110, 1110, and so on, corresponding to sums of 2^(n + 1) – 2, with n as a natural number. This property simplified the creation of the compression table.

These successful tests confirmed that both compression and decompression work reliably and efficiently, handling various input types and ensuring data integrity throughout the process.

### CONCLUSION

The implementation of the text compression and decompression algorithm in C was successful, meeting all the requirements and objectives outlined in the assignment. The results obtained during the various testing phases demonstrate the algorithm's efficiency in lossless data compression, validating the use of prefix-free encoding techniques for this purpose.
