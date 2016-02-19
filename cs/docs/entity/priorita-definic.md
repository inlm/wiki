# Priorita definic

**POZOR!** Ve verzi [2.0.0](../changelog.md#verze-2.0.0) došlo ke změně priority.

## Od verze 2.0.0

Při přístupu k položce mají metody vždy přednost před anotacemi (pokud metoda existuje).

[Informace na fóru](https://forum.dibiphp.com/cs/14592-lean-mapper-tenke-orm-nad-dibi?p=8#p107950)


## Před verzí 2.0.0

Při přístupu k `$book->title` se postupuje následovně:

1. Hledá se anotace `@property string $title`. Pokud existuje, Lean Mapper ji použije a vrátí relevantní hodnotu.
2. Pokud anotace neexistuje, Lean Mapper hledá metodu `getTitle()`. Pokud existuje, zavolá ji a vrátí její návratovou hodnotu.
3. Pokud ani tato metoda neexistuje, Lean Mapper vyvolá výjimku `LeanMapper\Exception\MemberAccessException`.

Při přístupu k `$book->getTitle()` se postupuje následovně:

1. Hledá se metoda `getTitle()`. Pokud existuje, Lean Mapper ji zavolá a vrátí její návratovou hodnotu.
2. Pokud metoda neexistuje, Lean Mapper hledá anotaci `@property string $title`. Pokud existuje, použije ji a vrátí relevantní hodnotu.
3. Pokud ani tato anotace neexistuje, Lean Mapper vyvolá výjimku `LeanMapper\Exception\MemberAccessException`.

Při volání `$book->title = 'New title'` se postupuje následovně:

1. Hledá se anotace `@property string $title`. Pokud existuje, Lean Mapper ji použije a nastaví požadovanou hodnotu.
2. Pokud anotace neexistuje, Lean Mapper hledá metodu `setTitle($title)` (parametr může mít libovolný název). Pokud existuje, zavolá ji a přiřazovanou hodnotu jí předá jako argument.
3. Pokud ani tato metoda neexistuje, Lean Mapper vyvolá výjimku `LeanMapper\Exception\MemberAccessException`.

Při volání `$book->setTitle('New title')` se postupuje následovně:

1. Hledá se metoda `setTitle($title)` (parametr může mít libovolný název). Pokud existuje, Lean Mapper ji zavolá a přiřazovanou hodnotu jí předá jako argument.
2. Pokud metoda neexistuje, Lean Mapper hledá anotaci `@property string $title`. Pokud existuje, použije ji a nastaví požadovanou hodnotu.
3. Pokud ani tato anotace neexistuje, Lean Mapper vyvolá výjimku `LeanMapper\Exception\MemberAccessException`.

Jak je z pravidel vidět, při přístupu přes magickou metodu `__get` mají přednost anotace, při přístupu přes metody mají přednost metody.
