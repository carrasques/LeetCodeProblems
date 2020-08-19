

# Problema:

> *Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.*

> *__Note__: For the purpose of this problem, we define empty string as valid palindrome.*


### Exemplo 1:
__Input__: "A man, a plan, a canal: Panama"  
__Output__: true  

### Exemplo2:
__Input__: "race a car"  
__Output__: false  


## Resolução:
Tentei basear-me no procedimento para verificar se uma *string* é um palíndromo: percorrer a string começando pelos extremos opostos e ir verificando se os caracteres são iguais:

```
for(int begin = 0, end = s.length()-1; end>=begin; end--, begin++) {
    if(s.charAt(begin)) != s.charAt(end))
        return false;
}
return true;
```

Para utilizar esta abordagem nas strings de input deste problema que contêm espaços e outros caracteres não relevantes, é necessário primeiro remover estes mesmos caracteres deixando apenas os alfanuméricos.


Para isso pensei em utilizar uma expressão regular. A expressão regular para detectar um caracter alfanumérico é a seguinte:

```
[a-zA-Z0-9]+
```

Se utilizarmos a expressão inversa (dada pelo símbolo "^") é possível detectar todos os caracteres que não sejam alfanuméricos:

```
[^a-zA-Z0-9]+
```

Fazendo uso do método *.replaceAll()* podemos usar a expressão regular e substituir os caracteres não alfanuméricos pelo caracter vazio:

```
s = s.replaceAll("[^a-zA-Z0-9]+", "");
```
Porém, ainda existe um problema: a comparação entre caracteres tem de ser *case insensitive*. A abordagem utilizada foi aquando da comparação entre caracteres colocá-los a *lowercase*:

```
if(Character.toLowerCase(s.charAt(begin)) != Character.toLowerCase(s.charAt(end)))
```

O código completo fica então:

```
s = s.replaceAll("[^a-zA-Z0-9]+", "");

for(int begin = 0, end = s.length()-1; end>=begin; end--, begin++) {
    if(Character.toLowerCase(s.charAt(begin)) != Character.toLowerCase(s.charAt(end)))
        return false;
}

return true;
```

A primeira submissão:

![Primeira submissão](Images/FirstSubmission.png)

Não ficando contente com os resultados da submissão decidi usar uma nova abordagem: fazer o teste de palíndromo sem a "limpeza" da string.

Se os índices *begin* e *end* consistirem em caracteres alfanuméricos é feita a sua comparação. Caso contrário, o caracter que não é alfanumérico é ignorado e o índice correspondente avança (begin++ ou end--).

```
while (begin<=end){
  se forem os dois alfanuméricos:
    testar para palindromo

  else {
    apenas avançar com o indice que não é alfanumérico
  }
}
```

O método para verificar se um caracter é um alfanumérico foi tirado do StackOverflow:

```
public boolean isAlphaNumeric(char c) {
    return (c >= 'a' && c <= 'z') ||
       (c >= 'A' && c <= 'Z') ||
       (c >= '0' && c <= '9');
}
```

O novo código da solução fica então:

```
int begin = 0;
int end = s.length()-1;

while(end>=begin) {
    char beginChar = s.charAt(begin);
    char endChar = s.charAt(end);

    if(isAlphaNumeric(beginChar) && isAlphaNumeric(endChar)){
        if(Character.toLowerCase(beginChar) != Character.toLowerCase(endChar))
            return false;

        begin++;
        end--;
    }

    else {
        begin += (isAlphaNumeric(beginChar)) ? 0 : 1;
        end -= (isAlphaNumeric(endChar)) ? 0: 1;
    }
}

return true;
```

Depois da submissão:

![Segunda submissão](Images/FinalSubmission.png)
