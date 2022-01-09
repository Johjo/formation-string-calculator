# Le squelette

Le processus TDD commence par l'étape RED. Nous devons donc mettre en place un test qui échoue.

Nous commençons par créer un fichier de test nommé `test_string_calculator.py`.

Dedans, nous créons la fonction suivante : 
```python
def test_calculate_zero_when_empty_string():  
    assert calculate("") == 0
```

Nous exécutons tous les tests et obtenons le résultat suivant :
```
FAILED  [100%]
test_string_calculator.py:0 (test_calculate_zero_when_empty_string)
def test_calculate_zero_when_empty_string():
>       assert calculate("") == 0
E       NameError: name 'calculate' is not defined
```

L'interpréteur nous explique que la méthode calculate n'existe pas. Nous allons donc la créer.

Toujours dans le fichier `test_string_calculator.py`, nous créons la méthode suivante : 

```python
def calculate():  
    pass
```

puis nous exécutons et obtenons le résultat suivant : 

```
FAILED  [100%]
test_string_calculator.py:3 (test_calculate_zero_when_empty_string)
def test_calculate_zero_when_empty_string():
>       assert calculate("") == 0
E       TypeError: calculate() takes 0 positional arguments but 1 was given

test_string_calculator.py:5: TypeError
```

Cette erreur nous indique que la fonction `calculate` n'accepte aucun paramètre alors que nous lui en passons un dans le test.

Modifions la fonction et rajoutons lui le paramètre :
```python
def calculate(expression):  
    pass
```

puis exécutons : 

```
FAILED  [100%]
test_string_calculator.py:3 (test_calculate_zero_when_empty_string)
None != 0

Expected :0
Actual   :None
<Click to see difference>

def test_calculate_zero_when_empty_string():
>       assert calculate("") == 0
E       assert None == 0

test_string_calculator.py:5: AssertionError
```

Cette erreur est particulière par rapport aux précédentes. Les deux premières étaient des erreurs d'exécution. Le programme plantait car notre code n'était pas écrit correctement. Il manquait quelque chose pour que le code soit complet. Notre code ne fonctionnait pas.

Dans cette dernière erreur, nous avons ce que l'on appelle une AssertionError. Ce genre d'erreur met en évidence que notre code n'a pas le bon comportement. Notre code fonctionne, mais il ne fait pas ce qu'il faut.

L'erreur indique que la valeur attendue est 0 (`Expected`), mais que nous avons obtenu None (`Actual`). Nous voyons aussi que l'erreur se situe au niveau de la valeur de retour de `calculate("")` dans la fonction de test `test_calculate_zero_when_empty_string`.

Cette erreur nous permet d'apprendre qu'une fonction Python renvoie par défaut la valeur `None` (`null` pour ceux qui viennent d'autres langages) si elle n'utilise pas le mot clé `return`.

Nous allons écrire le code nécessaire et minimal pour faire passer le test. Ainsi, nous validerons l'étape GREEN. Cette étape doit être le plus rapide possible.

Nous corrigeons donc la fonction : 
```python
def calculate(expression):  
    return 0
```

Cette correction peut surprendre, mais lorsqu'on pratique TDD, on va droit au but quitte à écrire un code improbable. Le code s'enrichira et deviendra de plus en générique au fur et à mesure que le nombre de tests augmentera.

**Grâce à cette première phase RED - GREEN (nous n'avons pas fait de refactoring), nous avons mis en place le squelette de notre programme. Dorénavant, notre code devrait toujours fonctionner, même s'il ne fait pas encore ce qu'il faut.**

