# Hromadné přiřazování

Užitečnou metodou je metoda `assign(array $values, array $whitelist = null)`, kterou entity dědí z `LeanMapper\Entity`. Umožňuje hromadně přiřadit hodnoty do více položek:

``` php
<?php

$entity->assign(array(
	'title' => 'Modified title',
	'description' => 'lorem ipsum',
	'number' => 42,
));

$entity->assign($newValues, array('title', 'description'));
```

Prvním parametrem je pole ve formátu položka => nová hodnota a druhým, volitelným, je „whitelist“ položek, které se berou v úvahu. Pokud je metoda volána se dvěma parametry, pozměněné hodnoty položek, které nejsou vyjmenovány ve „whitelistu“, se ignorují.

Pokud vámi používaný framework například umí vracet hodnoty z formulářů v podobě pole, váš kód může být takto stručný:

``` php
<?php

$author->assign($form->getValues(), array('title', 'name', 'web');
```

Nutno zdůraznit, že se jedná jen o jakýsi syntaktický cukr a pod pokličkou se volají jednotlivé settery entity, které obvykle obsahují validační pravidla. Jedná se tedy o naprosto bezpečný a legitimní způsob práce s entitou.
