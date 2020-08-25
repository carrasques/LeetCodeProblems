

# Problema:

> *Given a singly linked list, determine if it is a palindrome.*

> __Follow up:__  
- Could you do it in O(n) time and O(1) space?

### Exemplo 1:
__Input__: 1 -> 1 -> 2  
__Output__: 1 -> 2

### Exemplo2:
__Input__: 1->2->2->1  
__Output__: true  


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

A abordagem mais simples é armazenar os valores de cada nó da lista num array/lista. Deste modo podemos utilizar o algoritmo para testar se um número é um palíndromo: começa-se pelos extremos opostos do número e verifica-se se os algoritmos de cada extremo são iguais. Se não forem iguais, então o número não é um palíndromo. Caso contrário, comparam-se os algoritmos seguintes. Este processo continua.

O primeiro passo é a criação desta lista/array. Utilizei um *ArrayList* pela sua volatibilidade no número de elementos e pelo facto de que os elementos poderem ser acedidos pelo seu índice com uma complexidade O(1).

```
ArrayList<Integer> arrayList = new ArrayList<Integer>();
```
O passo seguinte foi preencher a *ArrayList* com os valores dos nós da lista ligada. Isto é feito com recurso a um ciclo *while* que percorre a lista ligada:

```
while (head!=null) {
  arrayList.add(head.val);
  head = head.next;
}
```

Por fim, podemos utilizar o algoritmo previamente mencionado:

```
for(int begin = 0, end = arrayList.size()-1; begin<=end; begin++, end--) {

  if(!arrayList.get(begin).equals(arrayList.get(end)))
      return false;
}

return true;
```

O código completo fica então:

```
ArrayList<Integer> arrayList = new ArrayList<Integer>();

while(head != null) {
    arrayList.add(head.val);
    head = head.next;
}

for(int begin = 0, end = arrayList.size()-1; begin<=end; begin++, end--) {

    if(!arrayList.get(begin).equals(arrayList.get(end)))
        return false;
}

return true;
```

Depois da submissão:

![Primeira submissão](Images/FirstSubmission.png)

Esta solução não segue o desafio de ser computada com uma complexidade temporal e especial de O(n) e de O(1) respectivamente.

Teve de ser então usada outra estratégia para que resolução do problema fosse de encontro com estas restrições.

Uma das propriedades de um palíndromo é que este é igual ao seu inverso.

Se conseguirmos criar o inverso do número representado pela lista ligada percorrendo apenas uma vez a mesma, conseguiremos depois comparar os dois valores.

O código fica então:

```
String regular = "";
String inverse = "";

while(head != null) {
    int val = head.val;
    regular += val;
    inverse = val + inverse;
    head = head.next;
}
return (inverse.equals(normal));
```

![Primeira falha](Images/FirstFail.png)

Comparar duas strings pode ser um processo custoso. Pelo que
