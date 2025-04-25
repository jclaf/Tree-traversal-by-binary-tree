# Tree traversal by binary tree

- **Ce code implémente un arbre binaire de recherche (BST) avec insertion, recherche, suppression et parcours infixe.**
- **Il permet de stocker, retrouver, supprimer et lister des valeurs de manière efficace.**
- **C’est une structure de données fondamentale en algorithmique, utilisée dans de nombreux domaines (bases de données, indexation, etc.).**

## Description du Code

### 1. **Classe `TreeNode`**

```python
class TreeNode:
    def __init__(self, key):
        self.key = key
        self.left = None
        self.right = None

    def __str__(self):
        return str(self.key)
```
- **But** : Représente un nœud de l’arbre.
- **Attributs** :
  - `key` : La valeur stockée dans le nœud.
  - `left` : Sous-arbre gauche (nœud ou None).
  - `right` : Sous-arbre droit (nœud ou None).
- **Méthode spéciale** : `__str__` permet d’afficher la clé du nœud.

---

### 2. **Classe `BinarySearchTree`**

#### a. **Initialisation**

```python
def __init__(self):
    self.root = None
```
- **But** : Initialise un arbre vide.

---

#### b. **Insertion d’une valeur**

```python
def _insert(self, node, key):
    if node is None:
        return TreeNode(key)
    if key  node.key:
        node.right = self._insert(node.right, key)
    return node

def insert(self, key):
    self.root = self._insert(self.root, key)
```
- **Principe** :
  - On compare la valeur à insérer avec la clé du nœud courant.
  - Si elle est inférieure, on va à gauche ; supérieure, à droite.
  - On s’arrête lorsqu’on atteint un emplacement vide (`None`), où l’on crée un nouveau nœud.
- **Appel public** : `insert(key)` insère la valeur dans l’arbre.

---

#### c. **Recherche d’une valeur**

```python
def _search(self, node, key):
    if node is None or node.key == key:
        return node
    if key  node.key:
        node.right = self._delete(node.right, key)
    else:
        if node.left is None:
            return node.right
        elif node.right is None:
            return node.left
        node.key = self._min_value(node.right)
        node.right = self._delete(node.right, node.key)
    return node

def delete(self, key):
    self.root = self._delete(self.root, key)
```
- **Principe** :
  - On recherche le nœud à supprimer.
  - **Trois cas possibles** :
    1. **Aucune branche** : On retourne `None`.
    2. **Une seule branche** : On retourne la branche non vide.
    3. **Deux branches** : On remplace la clé du nœud par la plus petite valeur du sous-arbre droit (successeur), puis on supprime ce successeur.
- **Appel public** : `delete(key)` supprime la valeur de l’arbre.

---

#### e. **Recherche de la valeur minimale d’un sous-arbre**

```python
def _min_value(self, node):
    while node.left is not None:
        node = node.left
    return node.key
```
- **But** : Trouver la valeur la plus à gauche (la plus petite) d’un sous-arbre.

---

#### f. **Parcours infixe (inorder traversal)**

```python
def _inorder_traversal(self, node, result):
    if node:
        self._inorder_traversal(node.left, result)
        result.append(node.key)
        self._inorder_traversal(node.right, result)

def inorder_traversal(self):
    result = []
    self._inorder_traversal(self.root, result)
    return result
```
- **Principe** :
  - Parcourt l’arbre de gauche à droite (gauche, racine, droite).
  - Retourne une liste triée des valeurs de l’arbre.

---

### 3. **Exemple d’utilisation**

```python
if __name__=="__main__":
    bst = BinarySearchTree()
    nodes = [50, 30, 20, 40, 70, 60, 80]
    for node in nodes:
        bst.insert(node)
    print('Search for 80:', bst.search(80))
    print("Inorder traversal:", bst.inorder_traversal())
    bst.delete(40)
    print("Search for 40:", bst.search(40))
    print('Inorder traversal after deleting 40:', bst.inorder_traversal())
```
- **Création** d’un arbre binaire de recherche.
- **Insertion** de plusieurs valeurs.
- **Recherche** d’une valeur présente (`80`).
- **Affichage** du parcours infixe (valeurs triées).
- **Suppression** d’une valeur (`40`), puis nouvelle recherche et parcours infixe.

---

## Algorithme Utilisé

### **Arbre Binaire de Recherche (BST)**

- **Insertion, recherche, suppression** : Complexité moyenne O(log n) si l’arbre est équilibré, O(n) dans le pire des cas (arbre dégénéré).
- **Parcours infixe** : Permet d’obtenir les valeurs triées.
- **Suppression** : Gère tous les cas (feuille, un enfant, deux enfants).
