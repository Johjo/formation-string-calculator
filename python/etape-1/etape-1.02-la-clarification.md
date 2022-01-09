# La clarification

Suite au premier test, nous sommes sûrs que notre code renvoie toujours 0 lorsqu'on lui présente une chaîne vide. Cette chaîne vide correspond au fait de passer 0 nombre.

L'étape suivante est donc de passer 1 nombre.

Nous ajoutons le test suivant : 
```python
def test_calculate_number_when_one_number():  
    assert calculate("1") == 1
```

Pour le résultat d'exécution suivant : 

```
FAILED  [100%]
test_string_calculator.py:8 (test_calculate_number_when_one_number)
0 != 1

Expected :1
Actual   :0
<Click to see difference>

def test_calculate_number_when_one_number():
>       assert calculate("1") == 1
E       assert 0 == 1

test_string_calculator.py:10: AssertionError
```

Nous attendions la valeur `1` et nous recevons la valeur `0`. C'est logique puisque notre code renvoie spécifiquement `0`.

Tu noteras aussi que mon test part directement sur l'expression `"1"` et non `"0"`. En effet, cela permet d'avoir un test qui échoue directement. Dans le second cas, le test serait directement passer.

Corrigeons la fonction pour faire passer le test :
```python
def calculate(expression):  
    if expression == "1":  
        return 1  
    return 0
```

Et là, je t'invite à prendre votre inspiration et réfléchir à ce code. Il est probable que tu le trouves ridicule. Je viens de pratiquer ce que j'appelle la triche. Cette méthode vient de me faire gagner beaucoup de temps car désormais, je sais que tout fonctionne.

Tous mes tests passent, je viens de valider l'étape GREEN, et je peux maintenant passer à l'étape REFACTORING. Je peux améliorer mon code en toute sécurité et si jamais je casse quelque chose, je peux faire marche arrière.

Dans l'état du code, il y a deux lignes que je souhaite voir changer. La ligne ` if expression == "1":` et la ligne `return 1`. Je vais me focaliser d'abord sur la seconde. 

Nous allons devoir clarifier le code et comprendre ce que représente chaque mot que nous avons écrit. Que représente ce `1` ? 

Je te laisse réfléchir.......

Ce `1` correspond au caractère `'1'` qui se trouve dans la chaîne `"1"` contenue dans la variable `expression`.

Nous savons ce que c'est, corrigeons vite notre code:
```python
def calculate(expression):  
    if expression == "1":  
        return expression  
    return 0
```

Et lançons les tests :
```
FAILED  [100%]
test_string_calculator.py:10 (test_calculate_number_when_one_number)
1 != 1

Expected :1
Actual   :1
<Click to see difference>

def test_calculate_number_when_one_number():
>       assert calculate("1") == 1
E       AssertionError: assert '1' == 1

test_string_calculator.py:12: AssertionError
```

Notre test échoue, parce qu'on attendait `1` et que l'on reçoit `1`. Cette erreur est assez déconcertante. Il faut étudier avec minutie l'erreur pour voir la ligne `E       AssertionError: assert '1' == 1`. Cette ligne nous explique que l'on a reçu le caractère `'1'` au lieu de l'entier `1`.

Nous pouvons facilement corriger cela. Normalement, nous devrions faire marche arrière et repenser notre hypothèse, mais nous sommes proches du but. Tentons le code suivant : 
```python
def calculate(expression):  
    if expression == "1":  
        return int(expression)  
    return 0
```

Bingo, les tests passent ! Si ça n'avait pas été le cas, nous serions revenus au code précédent où tous les tests passaient.

La fonction `int` permet de convertir une chaîne de caractères en entier. 

Il nous reste encore la première ligne à supprimer. Nous pourrions continuer à clarifier, mais nous allons voir une seconde technique qui nous permettra de le faire plus facilement. On l'appelle : **la triangulation**.

