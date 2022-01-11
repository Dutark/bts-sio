# POO

## La Programmation Orientée Objet

Par [Valentin Brosseau](https://github.com/c4software) / [@c4software](http://twitter.com/c4software)

---

Pourquoi la Programmation Orientée Objet ?

En groupe de 2 ou 3

- Que vous souvenez-vous ?
- Où faites-vous déjà de la POO ? Quels sont les avantages ?

---

## La POO c'est 3 concepts

---

**Concept de modélisation** à travers la notion de classe et d’instanciation de ces classes.

---

**Concept d’action** à travers la notion d’envoi de messages et de méthodes à l’intérieur des objets.

---

**Concept de construction** par réutilisation et amélioration par l’utilisation de la notion d’héritage.

---

### Mais surtout

Ça permet de représenter **informatiquement** quelque chose du monde réel.

---

### Deux notions

- Les classes
- Les objets

---

### Les classes

Représente une définition d'une problématique réelle.

- « Qu'est-ce que je souhaite représenter ? »
- « Comment déterminer ce que je souhaite représenter »
  - Spécifications client.
  - Mes connaissances du problème / de ce que je souhaite représenter

---

Serviront de moule pour créer des objets.

---

Une classe étant **une définition**, elle nous servira plus tard à créer **des objets**.

---

### Une classe est composée de :

- D'attributs (variable d'instance ou propriété).
- De méthodes (actions / opération au niveau de la classe).

---

### Nous avons donc deux types membres dans la classe

- Des **propriétés** (le données de l'objet) **avec une visibilité**
- Des **méthodes** (les actions possibles : accélérer, freiner, etc.) **avec une visibilité**

---

### La visibilité ?

- Privée : accessible que dans l'objet.
- Public : accessible hors de l'objet.
- Protected : **accessible** aux enfants (héritage) mais **pas en dehors**.

---

![Visiblité d'un objet](./res/visibilite.jpg)

---

### Les méthodes

- Comme une fonction, mais **encapsulé** dans la classe.
- Possède une visibilité.
- Possède des paramètres.
- Surcharge: plusieurs **méthodes** peuvent avoir le même nom et des paramètres différents (type et/ou ordre).

---

### Les type de méthodes

- Le constructeur.
- Les méthodes d'actions.
- Les méthodes accesseurs / mutateurs.

---

### Un exemple

![Exemple modélisation](./res/modelisation-personne.png)

---

```php
class Personne
{

    // Attribut
    public $nom;
    public $prenom;
    private $dateNaissance;
    private $salaire;
    public $nbEnfant;


    // Constructeur
    function __construct($nom, $prenom, $dateNaissance, $nbEnfant = 0)
    {
        $this->nom = $nom;
        $this->prenom = $prenom;
        $this->dateNaissance = $dateNaissance;
        $this->nbEnfant = $nbEnfant;
    }

    // Mutateurs
    public function setSalaire($valeur)
    {
        $this->salaire = $valeur;
    }

    // Accesseur
    public function getSalaire($valeur)
    {
        return $this->salaire;
    }


    // Méthode
    public function identite(){
        return $this->nom . " " . $this->prenom;
    }

    // Méthode
    public function age()
    {
        $date = new DateTime($this->dateNaissance);
        $now = new DateTime();
        $interval = $now->diff($date);
        return $interval->y;
    }

    // Méthode
    public function argentPoche()
    {
        return $this->salaire / $this->nbEnfant;
    }
}
```

---

### Surcharges

```php

<?php
class SimpleClass
{
    // déclaration d'une propriété
    public $var = 'une valeur par défaut';
    public $var2 = 'une valeur par défaut';

    // Constructeur
    function __construct($var, $var2)
    {
        $this->var = $var;
        $this->var2 = $var2;
    }

    // déclaration des méthodes
    public function displayVar() {
        echo $this->var;
    }

    public function setVar($var){
        $this->var = $var;
    }

    public function setVar($var, $var2){
        $this->var = $var;
        $this->var2 = $var2;
    }
}
?>

```

---

### Ce qu'il faut retenir

- Les classes sont instanciables (création d'objets, `new Personne(…)`).
- Les propriétés sont les « variables » de l'objet.
- Les méthodes sont les « actions » de l'objet.
- Les méthodes **et** les propriétés _**ont des visiblités**_.
- Les méthodes peuvent être surchargées.

---

### Les objets

Chaque objet représente un objet du monde réel

exemple :

- une personne **précise**
- une voiture **spécifique**
- Un élément de menu.

---

⚠️ Utilise les classes précédemment définies ⚠️

```php
$personne1 = new Personne("Valentin", "Brosseau", "28/02/1987", 0);
$personne2 = new Personne("John", "Doe", "01/01/1970", 12);
```

👀 Créer un objet == Instancier 👀

---

### À faire

Nous souhaitons modéliser la problématique d'un vendeur de voitures.

---

Supposons que chaque Voiture possède :

- les « paramètres » suivant :
  - Une vitesse.
  - Un nombre de km.
  - Une année de fabrication.
- Les actions suivantes :
  - Calcul du nombre de km moyen par an depuis la fabrication.
  - Accélérer.

C'est à vous 🤓

---

_Une solution possible_

![Visiblité d'un objet](./res/modelisationVoiture.jpg)

---

Aide mémoire écriture

[Aide mémoire POO](/cheatsheets/poo/)

---

![Exemple modélisation](./res/modelisation-personne.png)

```php
$personne1 = new Personne("Valentin", "Brosseau", "28/02/1987", 0);
$personne2 = new Personne("John", "Doe", "01/01/1970", 12);
```

---

## Les collections d'objets

---

Regrouper plusieurs objets « dans une liste »

---

Exemple, comment gérer le cas de :

« Une entreprise contient des personnes (employés) »

---

![UML Basique](./res/collections_1.png)

---

_Définition_ : Une collection est un ensemble d'objets qui sont
regroupés ensemble sous un même nom.

---

![Aggregation](./res/UML_Rel_aggregation.jpg)

---

PHP

```php
$lesPersonnes = [];
```

---

### Ajouter en liste

```php
$unePersonne = new Personne("Doe", "John", "01/01/1970", 10);

array_push($lesPersonnes, new Personne("Brosseau", "Valentin", "28/02/1987", 0));
array_push($lesPersonnes, $unePersonne);
```

---

### Vider la liste

```php
$lesPersonnes = [];
```

---

### Mais également

```php
sizeof($lesPersonnes);
```

---

### En résumé

Un parallèle intéressant.

---

![Liste en PHP](./res/liste-php.png)

PHP

---

![Liste en Java](./res/liste-java.png)

Java

---

### Parcourir une collection

---

En PHP :

```php
foreach($lesPersonne as $laPersonne){
    // $laPersonne contient « un pointeur » vers une des personne de la liste
    // À chaque tour de boucle nous avons la personne suivante.
}
```

---

En Java :

```java
// Version moderne
lesPersonnes.forEach(laPersonne -> {
    // laPersonne contient « un pointeur » vers une des personne de la liste
    // À chaque tour de boucle nous avons la personne suivante.
});

// Version « à l'ancienne »
for (Personne laPersonne : lesPersonnes) {
    // laPersonne contient « un pointeur » vers une des personne de la liste
    // À chaque tour de boucle nous avons la personne suivante.
}
```

---

Aide mémoire écriture et comparaison

[Aide mémoire POO](/cheatsheets/poo/)

---

### La modélisation

![Rappel modélisations](./res/collections_2.png)

---

## L'héritage

Ça vous évoque quoi ?

---

L’héritage permet, lors de la déclaration d’une nouvelle classe, d'y inclure les caractéristiques d’une autre classe.

---

## On observe…

### Que constatez-vous ?

---

```php
class Mammifere {
    protected $vertebre = true;
    protected $espece = "";

    public print() {
        echo "Je suis un mammifère";
    }

    public function manger(){
        return "";
    }
}

class Humain extends mammifere {
    private $prenom = "";

    function __construct($prenom)
    {
        parent::__construct();
        this->$prenom = $prenom;
    }

    public function manger(){
        return "Je suis omnivore";
    }
}

$unHumain = new Humain("Valentin");
$unHumain->print(); // Je suis un mammifère.
$unHumain->manger(); // Je suis omnivore.
```

---

### La visibilité !

- Privée : accessible que dans l'objet.
- Public : accessible hors de l'objet.
- Protected : **accessible** aux enfants (héritage) mais **pas en dehors**.

---

[Héritage](./res/heritage_chat_animal.png)

- Est-ce que le chien et le chat peuvent avoir un nom ?
- Pourquoi l'héritage est intéressant ici ?
- Écrire la définition de classe correspondant au diagrame UML.

---

[Héritage 2](./res/heritage_personne.png)

- Que constatez-vous ?
- Pourquoi avons-nous décidé de découper la logique comme ceci ?
- Pourquoi l'héritage est intéressant ici ?
- Écrire la définition de classe correspondant au diagrame UML.

---

## C'est à vous

### Seul ou en groupe, trouvez des exemples d'héritages pertinents

---

## Mais nous pratiquons un exemple déjà

### La structure MVC

---

## Démo !

### À vous de me dire là où se trouve l'héritage, et pourquoi c'est intéressant…

---

## Synthèse

- La classe mère contient la logique **partagée**.
- La classe fille contient la logique **spécifique**.
- Un mot-clé Extends `class Humain extends Mammifere`.
- **Vous devez** construire le parent dans le constructeur de l'enfant.
- **Permets de généraliser un objet afin de partager des propriétés communes.**.
- **mais** il est également possible de spécialiser / redéfinir un objet.
  - Redéfinition, comme la surcharge, mais entre la classe fille et la classe mère.

---

Mise en pratique

---

## Surcharge & Redéfinition

- Qui peut me rappeler la différence ?

---

![Surcharge](./res/surcharge.png)

- Quel est l'intérêt ?
- À vos crayons ! Est-ce optimisable ?

---

![Redéfinition](./res/redefinition.png)

- Quel est l'intérêt ?

---

## Les classes Static

- Méthode & Propriété accessible **sans besoin d'un new**
- Permets d'encapsuler une logique.

---

```php
class Greeting {
  public static function welcome() {
    echo "Hello World!";
  }
}

Greeting::welcome();
```

- Que constatez vous ?
- Avez-vous des exemples d'usage en tête ?

---

## Classes Abstraites & Interfaces

### Touchons du doigt le véritable intérêt de la POO

---

## Les classes abstraites

Classe dont l'implémentation n'est pas complète et qui **n'est pas instanciable**.

---

## STOP !

Non instanciable ? Qu-est-ce que ça veux dire ?

---

## Donc pas de `new MaClassAbstraite()`

---

<iframe src="https://giphy.com/embed/MZQkUm97KTI1gI8sUj" width="480" height="480" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>

---

- Sers de base à d'autres classes dérivées (héritées).
- Ne peut pas être instanciée (pas de new).
- Permets de factoriser du code.
- Dois être héritée depuis une classe fille.

---

Avez-vous déjà vu des classes asbtraites ?

---

[Mise en pratique](/cours/exercices/poo/les-classes-abstraites.html)

---

```php
abstract class EtudiantAbstrait
{
    // Force les classes filles à définir cette méthode
    abstract protected function getSpecificite();
    abstract protected function setSpecificite($valeur);

    // méthode commune
    public function parler() {
        print "Je suis " . $this->getSpecificite() . "\n";
    }
}

class EtudiantSIO extends AbstractClass
{
    $option = "";

    function __construct($option){
        $this->option = $option;
    }

    protected function getSpecificite() {
       return $this->option;
    }

    protected function setSpecificite($valeur) {
       $this->option = $valeur
    }
}
```

---

## Les interfaces

Une interface ressemble à une classe abstraite dans laquelle aucune méthode ne serait implémentée.

- Ne contiens que des méthodes publiques.
- Ne contiens aucun code.
- N'est pas instanciable.
- Son « un contrat » que les classes filles devront **implémenter**.

---

[Entrons dans le détail](/cours/revealjs/index.html?source=les_interfaces)

---

[Mise en pratique](/cours/exercices/poo/les-interfaces-1.html)

---

## Classe abstraite ou Interface ?

---

- Quelle(s) différence(s) avez-vous constatez ?

---

Classes abstraites et interfaces ont chacune une fonction bien distincte :

- Les classes abstraites servent à factoriser du code.
- Tandis que les interfaces servent à définir des contrats de service.

---

## Des questions ?
