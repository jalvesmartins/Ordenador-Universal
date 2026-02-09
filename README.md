# Ordenador Universal - Algoritmo de Ordenação Adaptativo

## Descrição do Problema

Este projeto implementa um **Ordenador Universal** que seleciona adaptativamente o algoritmo de ordenação ideal com base nas características da entrada e parâmetros de custo. O sistema analisa o vetor de entrada e determina dinamicamente:

1. **Detecção de Quebras**: Conta o número de "quebras" no vetor (posições onde `V[i] > V[i+1]`)
2. **Limiar de Partição**: Encontra o tamanho mínimo ideal de partição para QuickSort vs InsertionSort
3. **Limiar de Quebras**: Determina o número máximo de quebras onde o InsertionSort supera o QuickSort

O problema é modelado da seguinte forma:
- Entrada: Vetor de inteiros com pesos de calibração (a, b, c), limiar de custo e seed
- Saída: Parâmetros ideais de ordenação e estatísticas de desempenho (comparações, movimentações, chamadas)

## Abordagem da Solução

A solução implementa uma **estratégia de ordenação híbrida adaptativa** que combina QuickSort e InsertionSort. A implementação utiliza:

- **Seleção de Pivô pela Mediana de Três**: Reduz os piores casos no QuickSort
- **Ordenação Híbrida**: Alterna para InsertionSort em partições pequenas ou vetores quase ordenados
- **Otimização por Função de Custo**: Usa função de custo ponderada `Custo = a*comparações + b*movimentações + c*chamadas`
- **Refinamento Iterativo**: Abordagem similar à busca binária para encontrar limiares ideais

Para informações detalhadas sobre a implementação do algoritmo, análise experimental e análise de complexidade, consulte a documentação na pasta `docs/`.

## Como Executar

### Pré-requisitos

- Compilador GCC
- Sistema de build Make
- Biblioteca padrão C

### Compilando o Projeto

Compile o projeto usando Make:

```bash
make
```

Isso criará o executável em `bin/tp1.out`.

### Executando o Programa

Execute o programa principal com um arquivo de entrada:

```bash
./bin/tp1.out <arquivo_entrada>
```

Ou use o comando run do Make:

```bash
make run FILE=<arquivo_entrada>
```

### Formato de Entrada

```
seed limiarCusto a b c tamanho
v1 v2 v3 ... vn
```

Onde:
- `seed`: Semente aleatória para reprodutibilidade
- `limiarCusto`: Diferença máxima de custo aceitável entre iterações
- `a, b, c`: Pesos de calibração para comparações, movimentações e chamadas respectivamente
- `tamanho`: Número de elementos no vetor
- `v1, v2, ..., vn`: Elementos do vetor (inteiros)

### Formato de Saída

```
size N seed S breaks B

iter 0
mps X cost C cmp Y move Z calls W
...

best mps X

iter 0
mbs X cost C cmp Y move Z calls W
...

best mbs X
```

Onde:
- **size, seed, breaks**: Características do vetor de entrada
- **iter**: Número da iteração durante a otimização de limiares
- **mps**: Tamanho Mínimo de Partição sendo testado
- **mbs**: Tamanho Máximo de Quebras sendo testado
- **cost**: Custo ponderado da operação de ordenação
- **cmp, move, calls**: Número de comparações, movimentações e chamadas recursivas

### Limpando Arquivos de Build

```bash
make clean
```

## Estrutura do Projeto

```
.
├── Makefile                # Configuração de build
├── README.md               # Este arquivo
├── include/
│   ├── estatisticas.h      # Estruturas e funções de rastreamento de estatísticas
│   ├── ordenador.h         # Interface do ordenador universal
│   └── sort.h              # Interface dos algoritmos de ordenação
├── src/
│   ├── estatisticas.c      # Implementação das estatísticas
│   ├── main.c              # Ponto de entrada principal
│   ├── ordenador.c         # Implementação do ordenador universal
│   └── sort.c              # Algoritmos de ordenação (QuickSort, InsertionSort)
└── docs/                   # Documentação (análise experimental e de complexidade)
```

## Autor

João Henrique Alves Martins  
Universidade Federal de Minas Gerais (UFMG)  
jalvesmartins16@ufmg.br
