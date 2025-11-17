# Árvores AVL - Remoção de Elementos
---

## Objetivos

Ao concluir esta atividade você deverá estender sua compreensão dos seguintes conceitos:
* Remoção de elementos em árvores binárias
* Manutenção das propriedades da árvore após remoção
* Tratamento dos diferentes casos de remoção

---

## Fundamentos Teóricos

### Como Funciona a Remoção em Árvores Binárias

A remoção de um elemento em uma árvore binária é mais complexa que a inserção, pois precisamos manter a estrutura e as propriedades da árvore após remover um nó. O processo pode ser dividido em **três casos principais**, dependendo da quantidade de filhos que o nó a ser removido possui.

#### **Caso 1: Nó Folha (Sem Filhos)**

Este é o caso mais simples. Quando o nó a ser removido não possui filhos (é uma folha):

1. Localize o nó a ser removido percorrendo a árvore
2. Identifique se ele é filho esquerdo ou direito de seu pai
3. Ajuste o ponteiro do pai para apontar para NULL (removendo a ligação)
4. Libere a memória do nó removido

**Exemplo visual:**
```
     10                    10
    /  \     remove 5     /  \
   5   15   --------->  NULL  15
```

#### **Caso 2: Nó com Um Filho**

Quando o nó a ser removido possui apenas um filho (esquerdo OU direito):

1. Localize o nó a ser removido
2. Identifique qual filho existe (esquerdo ou direito)
3. Conecte o pai do nó removido diretamente ao filho do nó removido
4. O filho "sobe" uma posição na árvore, ocupando o lugar do pai
5. Libere a memória do nó removido

**Exemplo visual:**
```
     10                    10
    /  \     remove 15    /  \
   5   15   --------->   5   20
        \
        20
```

#### **Caso 3: Nó com Dois Filhos**

Este é o caso mais complexo. Quando o nó possui ambos os filhos:

1. Localize o nó a ser removido
2. **Escolha o sucessor ou predecessor:**
   - **Sucessor:** o menor valor da subárvore direita (mais à esquerda)
   - **Predecessor:** o maior valor da subárvore esquerda (mais à direita)
3. Copie o valor do sucessor/predecessor para o nó a ser removido
4. Remova o sucessor/predecessor de sua posição original
   - Note que o sucessor/predecessor terá no máximo um filho (Casos 1 ou 2)
5. A remoção recursiva garante que a propriedade de busca seja mantida

**Exemplo visual usando sucessor:**
```
     10                    12
    /  \     remove 10    /  \
   5   15   --------->   5   15
      /  \                     \
     12  20                    20
     
O sucessor (12) substitui o nó removido (10)
```

### Por Que Usar o Sucessor ou Predecessor?

O sucessor (menor valor à direita) ou o predecessor (maior valor à esquerda) são escolhidos porque:
- Mantêm a propriedade de ordenação da árvore binária de busca
- O sucessor é maior que todos os valores da subárvore esquerda
- O predecessor é menor que todos os valores da subárvore direita
- Ambos têm no máximo um filho, simplificando sua remoção

### Considerações Importantes para Árvores AVL

Em árvores AVL, após qualquer remoção, é necessário:
1. Recalcular as alturas dos nós no caminho de volta
2. Verificar o fator de balanceamento de cada nó ancestral
3. Realizar rotações se necessário para manter o balanceamento
4. A árvore deve manter a propriedade AVL: |altura(esquerda) - altura(direita)| ≤ 1

---

## Atividade Proposta

Faça um fork deste repositório e realize as seguintes atividades: 

- [ ] **Implemente a função `removerElementoArvore`** que deve remover um elemento da árvore mantendo suas propriedades de busca e balanceamento
- [ ] **Trate corretamente os três casos de remoção:**
  - Nó folha (sem filhos)
  - Nó com um filho (esquerdo ou direito)
  - Nó com dois filhos (usando sucessor ou predecessor)
- [ ] **Teste sua implementação** com diferentes cenários:
  - Remover folhas
  - Remover nós intermediários com um filho
  - Remover nós com dois filhos
  - Remover a raiz da árvore
- [ ] **Verifique o balanceamento** da árvore após cada remoção (para árvores AVL)

### Dicas de Implementação

- Comece implementando a busca do nó a ser removido
- Identifique qual dos três casos se aplica
- Para o caso de dois filhos, implemente primeiro a busca do sucessor/predecessor
- Lembre-se de atualizar os ponteiros corretamente
- Não se esqueça de liberar a memória do nó removido
- Teste cada caso individualmente antes de integrar tudo
