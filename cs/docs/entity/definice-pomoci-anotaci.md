
# Definice pomocí anotací

Preferovaným (a stručnějším) způsobem, jak nadefinovat položky entity, je pomocí anotací. Tímto způsobem lze v praxi běžně nadefinovat naprostou většinu položek a vazeb. K [definici pomocí metod](definice-pomoci-metod.md) má obvykle smysl přistoupit pouze v případě několika málo specifických položek, jejichž nadefinování pomocí anotací není možné (z důvodu jejich nedostatečné vyjadřovací schopnosti).

Možnosti anotací nejsnáze popíšeme ukázkou:

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

[Příznakům](priznaky-anotaci.md) `m:hasOne` a `m:hasMany` nemusíte nyní věnovat pozornost, jejich význam si brzy vysvětlíme.

Definice každé položky se sestává z anotace `@property` následované typem položky, názvem a případnými volitelnými příznaky týkajících se vazeb a [filtrů](../filtry.md). Součástí definice typu může být volitelně i [příznak](priznaky-anotaci.md), zda může položka obsahovat hodnotu `null`.

Všimněte si použitého `use` statementu. Lean Mapper rozumí nejen definici jmenného prostoru, ale i použitým `use` statementům. Snad jediná záludnost, se kterou si neporadí, je přítomnost více jmenných prostorů v jednom souboru. Máte-li potřebu této vlastnosti PHP využít, nadefinujte typy položek v `@property` anotacích jako „fully qualified“ (tj. uvozených zpětným lomítkem).

Nepřehlédněte také, jakým způsobem se definují „kolekce“ (pole s hodnotami určitého typu) – pomocí prázdných hranatých závorek bezprostředně za typem položky (`v naší ukázce Bar[]`).


## Vazby v anotacích

Lean Mapper rozumí celkem čtyřem [příznakům](priznaky-anotaci.md) pro vyjádření vazeb mezi entitami: `m:hasOne`, `m:hasMany`, `m:belongsToOne`, `m:belongsToMany`.

Tyto příznaky se vepisují za název položky a volitelným dodatkem v závorce lze upřesnit, přes jaké sloupce a tabulky má Lean Mapper při získávání související entity postupovat. Pokud dodatek chybí, Lean Mapper si potřebné názvy odvozuje podle daných [konvencí](../konvence.md). Pokud vaše databáze tyto konvence dodržuje, v naprosté většině případů se bez těchto dodatků obejdete.

| Příznak | Tvar dodatku | Význam | Příklad použití
|---------|--------------|--------|-------------------
| m:hasOne | (sloupec odkazující na cílovou tabulku:cílová tabulka) | Vazba N:1 | Máme knihu a chceme načíst jejího autora.
| m:hasMany | (sloupec odkazující na zdrojovou tabulku:vazební tabulka:sloupec odkazující na cílovou tabulku:cílová tabulka) | Vazba M:N | Máme knihu a chceme získat kolekci tagů, kterými je označena.
| m:belongsToOne | (sloupec odkazující na zdrojovou tabulku:cílová tabulka) | Vazba 1:1 | Máme objednávku a chceme získat detail objednávky uložený v samostatné tabulce. Každý detail patří právě jedné objednávce.
| m:belongsToMany | (sloupec odkazující na zdrojovou tabulku:cílová tabulka) | Vazba 1:N | Máme autora a chceme získat kolekci knih, kterých je autorem.

U dovětků platí, že jejich jednotlivé části jsou odděleny dvojtečkou a vynechání libovolné části vede k jejímu odvození podle [konvencí](../konvence.md).


### Příklady definice vazeb

Pro dokonalé pochopení následuje ještě pár příkladů:

| Nejstručnější zápis | Příklad (ekvivalentního zápisu|ekvivalentních zápisů)
|---------------------|------------------------------------------------------
| Author $author m:hasOne | Author $author m:hasOne(author_id:author)
| Author $author m:hasOne(reviewer_id) | Author $author m:hasOne(reviewer_id:author)
| Tag[] $tags m:hasMany | Tag[] $tags m:hasMany(book_id:book_tag:tag_id:tag)
| Tag[] $tags m:hasMany(book_id:::tag)
| Tag[] $tags m:hasMany(book_id::tag_id:tag)
| Tag[] $tags m:hasMany(book_id::tag_id)
| Tag[] $tags m:hasMany(::supertag_id:supertag) | Tag[] $tags m:hasMany(book_id:book_tag:supertag_id:supertag)
| Book[] $books m:belongsToMany | Book[] $books m:belongsToMany(author_id:author)
| OrderDetail $detail m:belongsToOne | OrderDetail $detail m:belongsToOne(order_id:orderdetail)

