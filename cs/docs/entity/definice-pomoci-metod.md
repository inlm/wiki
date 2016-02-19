
# Definice pomocí metod

Mějme entitu, která má své položky [definovány pomocí anotací](definice-pomoci-anotaci.md):

``` php
<?php

namespace Model\Entity;

use DateTime as PlaceInTime;

/**
 * @property int $id
 * @property PlaceInTime $published
 * @property Foo|null $foo m:hasOne
 * @property Bar[] $bars m:hasMany(:::bartable)
 * @property string $title
 * @property string|null $description
 * @property null|int $number
 * @property bool $active
 */
class DummyEntity extends \LeanMapper\Entity
{
}
```

Tuto entitu můžeme kompletně přepsat do následující podoby:

``` php
<?php

namespace Model\Entity;

use DibiDateTime as PlaceInTime;

class DummyEntity extends \LeanMapper\Entity
{

	public function getId()
	{
		return (int) $this->row->id;
	}

	public function setId($id)
	{
		$this->row->id = (int) $id;
	}

	public function getPublished()
	{
		return $this->row->published;
	}

	public function setPublished(PlaceInTime $published)
	{
		$this->row->published = $published;
	}

	public function getFoo()
	{
		$row = $this->row->referenced('foo');
		return $row !== null ? new Foo($row) : null;
	}

	public function setFoo(Foo $foo = null)
	{
		$this->row->foo_id = $foo !== null ? $foo->id : null;
		$this->row->cleanReferencedRowsCache('foo', 'foo_id');
	}

	public function getBars()
	{
		$value = array();
		foreach ($this->row->referencing('dummy_bar') as $row) {
			$value[] = new Bar($row->referenced('bartable'));
		}
		return $value;
	}

	public function getTitle()
	{
		return (string) $this->row->title;
	}

	public function setTitle($title)
	{
		$this->row->title = (string) $title;
	}

	public function getDescription()
	{
		$description = $this->row->description;
		return $description !== null ? (string) $description : null;
	}

	public function setDescription($description)
	{
		$this->row->description = $description !== null ? (string) $description : null;
	}

	public function getNumber()
	{
		$number = $this->row->number;
		return $number !== null ? (int) $number : null;
	}

	public function setNumber($number)
	{
		$this->row->number = $number !== null ? (int) $number : null;
	}

	public function getActive()
	{
		return (bool) $this->row->active;
	}

	public function setActive($active)
	{
		$this->row->active = (bool) $active;
	}

}
```

Jedná se o transparentní, „nemagickou“ variantu, avšak patřičně upovídanou. Na druhou stranu, vyjadřovací schopnosti metod jsou větší než anotací, a proto občas není jiného východiska, než metody použít. Oba způsoby definic položek lze samozřejmě kombinovat, dokonce i v rámci jedné entity.

Všimněte si, že ve všech předvedených metodách se přistupuje k protected proměnné `$row`. Entity v Lean Mapperu totiž vlastní data neudržují. Udržují jen instanci třídy `LeanMapper\Row`, která vlastní data zapouzdřuje. Pro zájemce uveďme, že vlastní data neudržuje ani instance `LeanMapper\Row`. Ta vystupuje jen jako ukazatel na konkrétní sadu hodnot uvnitř instance `LeanMapper\Result`. Vlastní data musíme hledat až v ní.

Toto zdánlivě kostrbaté řešené umožňuje pokládat efektivní dotazy do databáze (ve stylu „NotORM“). Při typickém používání vás ale zmíněné interní záležitosti Lean Mapperu vůbec nemusí trápit. Seznamte se jen s veřejným rozhraním třídy `LeanMapper\Row`, abyste měli představu, co všechno se s jejími instancemi v entitách dá dělat.

