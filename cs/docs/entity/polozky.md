
# Položky

## Definice položek

Položky entity lze nadefinovat dvěma způsoby: pomocí *anotací* a pomocí *metod*.

* [Definice pomocí anotací](definice-pomoci-anotaci.md)
* [Definice pomocí metod](definice-pomoci-metod.md)

Nepřehlédněte informaci o [prioritě definic](priorita-definic.md).


## Přístup k položkám

Následující ukázka demonstruje, jak lze k položkám entity přistupovat:

``` php
<?php

// $entity instanceof Model\Entity\DummyEntity

$entity->id;

$entity->title;

$entity->description;

$entity->getDescription();

$entity->title = 'New title';

$entity->setDescription('lorem ipsum');
```


