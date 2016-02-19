
# Mapper

Mapper je třída implementující rozhraní `LeanMapper\IMapper`. Mapper definuje výchozí [konvence](konvence.md) používané systémem. Jedná se např. o tvar názvu vazební tabulky, převod názvu entitu na název tabulky, apod.

Výchozí implementací je třída `LeanMapper\DefaultMapper`.

**Poznámka:** Mapper je dostupný až od verze [2.0.0](changelog.md#2.0.0). Ve starších verzích sloužily k částečnému ovlivnění konvencí metody `LeanMapper\Entity::getEntityClass` a `LeanMapper\Repository::getEntityClass`.

