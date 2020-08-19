

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
