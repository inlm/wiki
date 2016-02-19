
# Co je LeanMapper

* **Tenké ORM pro PHP postavené nad knihovnou [dibi](https://dibiphp.com/)**

	Prověřená a výkonná knihovna dibi poskytuje Lean Mapperu *stabilní půdu pod nohama* a umožňuje psát kód pro *širokou řadu databázových systémů*.

* **ORM, které sestavuje elegantní a efektivní SQL dotazy**

	Lean Mapper je silně inspirován knihovnou [NotORM](http://www.notorm.com/) a obsahuje vlastní minimalistickou implementaci „NotORM principu“ (stahování souvisejících záznamů pro celý výsledek najednou místo jednotlivě).

* **Stabilní konzervativní knihovna**

	Stabilita a bezchybná funkčnost má při vývoji Lean Mapperu *nejvyšší prioritu*. Každá vydaná verze je označena kódem ve tvaru X.Y.Z a platí, že *změny v rámci řady Z jsou vždy zpětně kompatibilní*. Opravné balíčky jsou *vždy portovány do všech chybou dotčených řad X a Y*.
	
* **Knihovna s minimem závislostí**

	Jedinou závislostí Lean Mapperu je [dibi](https://dibiphp.com/).


# Co LeanMapper není

* **Moloch**

	Jádro ORM tvoří zhruba deset relativně jednoduchých tříd. Pro mírně pokročilého PHP programátora by měl být vlastní zdrojový kód ORM *snadno pochopitelný*.

* **Revoluční knihovna**

	Lean Mapper není v ničem převratný - převážně jen integruje osvědčené postupy a návrhové vzory a vyhýbá se těm, které se jinde ukázaly jako problematické.

* **Nezdokumentované cosi**


# Jak začít

1. Přečtete si [quick start](quick-start/)
2. Podle potřeby nastudujte [podrobnou dokumentaci](docs/)
3. Nepřehlédněte [dokumentaci API](api.md)
