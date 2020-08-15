

# Problema:

> *Given a sorted linked list, delete all duplicates such that each element appear only once.*


### Exemplo 1:

  Input: 1 -> 1 -> 2  
  Output: 1 -> 2

### Exemplo2:
  Input: 1 -> 1 -> 2 -> 3 -> 3  
  Output: 1 -> 2 -> 3  


## Resolução:

A classe *Solution* fornece a class *ListNode*, representando um nó da lista ligada:

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
```

Tratando-se de um problema de listas ligadas, pensei em começar por utilizar o clássico ciclo *while* para a travessia dos nós que compṍem a mesma:

```
while (node!= null) {
  .
  .
  .
}
```

O raciocínio foi o seguinte:  

Se o próximo nó (*head.next*) contiver um valor igual ao valor do nó corrente, esse nó é eliminado.

Para eliminar o nó,

![Remoção do nó]("RemoveNodeStackOverflow.png")
