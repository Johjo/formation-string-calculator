# La triangulation
La triangulation consiste à mettre en place deux tests. Ces deux tests nous permettront de découvrir le code générique permettant de les faire passer. 

Commençons par écrire le test :
```python
def test_calculate_number_when_one_number():  
    assert calculate("1") == 1  
    assert calculate("54") == 54
```

et regardons le échouer : 
```
FAILED  [100%]
test_string_calculator.py:10 (test_calculate_number_when_one_number)
0 != 54

Expected :54
Actual   :0
<Click to see difference>

def test_calculate_number_when_one_number():
        assert calculate("1") == 1
>       assert calculate("54") == 54
E       assert 0 == 54

test_string_calculator.py:13: AssertionError
```

Dans l'idéal, on évite d'utiliser plusieurs `assert` dans le même test. Une technique serait d'utiliser les tests paramétrés. Nous verrons comment les mettre en place dans un prochain chapitre. En attendant, nous allons vivre avec cette mauvaise pratique.

Pour faire passer le test rapidement, nous pouvons tricher :
```python
def calculate(expression):  
    if expression == "1":  
        return int(expression)  
    if expression == "54":  
        return 54  
    return 0
```

Mais est-ce la bonne méthode ?

Dans le test précédent, nous avons clarifier le code, nous avons compris d'où venait le `1`. Nous pouvons en déduire le `54`. L'idéal aurait été de copier directement le bloc de code clarifié.

Recommençons : 
```python
def calculate(expression):  
    if expression == "1":  
        return int(expression)  
    if expression == "54":  
        return int(expression)  
    return 0
```

Et nos tests restent verts !

Ce code nous met en évidence que si expression vaut `"1"` ou `"54"`, il faut renvoyer `int(expression)`.  Nous devons donc trouver la propriété qui nous permette de réunir les deux blocs `if`. On cherche donc le code suivant : 

```python
def calculate(expression):  
    if ???:  
        return int(expression)  
    return 0
```

Si nous clarifions la situation, nous savons que nous devons renvoyer 0 si nous passons une chaîne vide. Essayons de tester cette hypothèse :
```python
def calculate(expression):  
    if expression == "":  
        return 0  
    if expression == "1":  
        return int(expression)  
    if expression == "54":  
        return int(expression)
```

Nous restons au vert. L'hypothèse semble bonne. Continuons dans cette direction et regardons si tous les autres cas ne devraient pas renvoyer `int(expression)`:

```python
def calculate(expression):  
    if expression == "":  
        return 0  
    return int(expression)
```

Essayons maintenant de trouver un test qui mette en évidence que la fonctionnalité n'est pas totalement implémentée.

Je n'en trouve pas... et toi ? 

Pour valider que le code est terminé, je rajoute un dernier test qui doit passer directement au vert : 
```python
def test_calculate_number_when_one_number():  
    assert calculate("1") == 1  
    assert calculate("54") == 54  
    assert calculate("205") == 205
```

Si un test passe directement au vert, cela signifie deux choses : 
- Soit mon test est faux, et je dois le corriger
- Soit mon test vérifie une fonctionnalité déjà implémentée

Prenons le temps de vérifier que nous sommes dans le second cas... C'est bon ? Cela signifie que le développement (de la fonctionnalité) est terminé.

