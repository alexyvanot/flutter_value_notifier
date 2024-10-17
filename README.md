# flutter_value_notifier

Ce projet Flutter est une démonstration de l'utilisation de `ValueNotifier` combiné avec `Provider` pour gérer et mettre à jour l'état dans une simple application de compteur.

## Fonctionnalités

- **ValueNotifier** : Utilisé pour gérer l'état local d'un compteur dans le widget principal.
- **Provider** : Utilisé pour gérer l'état global via un `ChangeNotifier`, permettant d'accéder et de modifier l'état à travers toute l'application.
- Mise à jour dynamique de l'interface utilisateur lorsque le compteur est incrémenté.

## Concepts Clés

### ValueNotifier
- `ValueNotifier` est une classe qui hérite de `ChangeNotifier`, et permet de notifier ses auditeurs lorsqu'une valeur change.
- Dans ce projet, il gère la valeur du compteur localement et permet de mettre à jour l'interface utilisateur chaque fois que la valeur change.

### Provider
- `Provider` permet de gérer l'état global à l'aide de `ChangeNotifier`. Dans ce projet, il gère l'incrémentation du compteur et notifie les widgets écoutant ces changements pour mettre à jour l'affichage du compteur.

## Détails de l'implémentation

### CountNotifier
Cette classe hérite de `ChangeNotifier` et contient la logique d'incrémentation du compteur. Chaque fois que la méthode `incrementCounter` est appelée, le compteur est incrémenté et les widgets qui écoutent sont notifiés pour mettre à jour l'affichage.

class CountNotifier extends ChangeNotifier {
  int counter = 0;

  void incrementCounter() {
    counter++;
    notifyListeners();
  }
}

### Utilisation de ValueNotifier
Dans la classe `_MyHomePageState`, `ValueNotifier<int>` est utilisé pour gérer localement l'état du compteur. Un `ValueListenableBuilder` (commenté) permet d'écouter les changements de la valeur et de mettre à jour l'interface utilisateur automatiquement.

final ValueNotifier<int> _counter = ValueNotifier(0);

### Utilisation de Provider
Le `ChangeNotifierProvider` est utilisé pour fournir le `CountNotifier` à l'ensemble de l'arbre des widgets. Le `CountWidget` utilise `context.watch<CountNotifier>().counter` pour écouter les changements du compteur et afficher sa valeur actualisée.

int value = context.watch<CountNotifier>().counter;

## Comment exécuter le projet

1. Clonez ce dépôt.
2. Exécutez `flutter pub get` pour installer les dépendances.
3. Lancez l'application avec `flutter run`.

## Aperçu du Code

### `CountNotifier`
Cette classe gère l'état du compteur globalement, et notifie les auditeurs lorsque le compteur change grâce à `notifyListeners()`.

### `MyHomePage`
Ce widget représente la page principale de l'application. Il utilise à la fois `ValueNotifier` et `Provider` pour gérer et afficher l'état du compteur.

### `CountWidget`
Ce widget affiche la valeur du compteur en temps réel, en se basant sur les données fournies par `Provider`.

## Licence

Ce projet est sous licence MIT.

