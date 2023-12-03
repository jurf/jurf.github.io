---
title: "Naivná analýza Colemak-DH v slovenčine (vs. Qwertz/y, Dvorak, Colemak a Workman)"
layout: post
---

Už dlhšie sa zaujímam o alternatívne rozloženia klávesnice.

Prácou na počítači sa živím a už dlhšie ma sprevádza bolesť v rukách. Pri týchto rozloženiach ide o **minimalizáciu úsilia** (nie maximalizáciu rýchlosti, čo je častá miskoncepcia), vďaka čomu vedia s touto do dlhodoba bolesťou pomôcť.

Avšak žiadne z dostupných analýz sa nevyužíva slovenčinu, takže je ťažké povedať, ako veľmi a či vôbec sa dá profitovať z nejakého rozloženia v slovenčine. Preto som sa rozhodol spraviť vlastnú analýzu.

## Výsledky

| Rozloženie[^choice]      | Námaha (EN)[^alt] | Námaha (SK)[^alt] | Zlepšenie (EN) | Zlepšenie (SK) |
| ------------------------ | ----------------- | ----------------- | -------------- | -------------- |
| Qwerty                   | 2,383             | 2,389             | —              | —              |
| Qwertz[^qwertz]          | 2,363             | 2.392             | 0,8 %          | 0 %            |
| [Dvorak][dvorak]         | 1,931             | 2,055             | 19,0 %         | 14,0 %         |
| [Colemak][colemak]       | 1,836             | 1,981             | 23,0 %         | 17,1 %         |
| [Workman][workman]       | 1,806             | 2,087             | 24,2 %         | 12,6 %         |
| [Colemak-DH][colemak-dh] | 1,735             | 1,937             | 27,2 %         | 18,9 %         |

[^choice]: Z môjho výskumu sa mi nezdá, že by na Slovensku boli alterntatívne rozloženia nejak populárne, tak tu uvádzam iba zopár najznámejších. Ďalšie sú k dispozícii v interaktívnom nástroji.
[^alt]: Použil som alternatívne rozloženie prstov (viď nástroj), lebo neverím, že niekto skutočne píše s tradičným, ktoré má beztak horšie výsledky.
[^qwertz]: Qwertz je optimalizované pre nemčinu. Nechal som ho tu len aby som ukázal, aké zbytočné je používať ho v slovenčine.

Ako vidno, čim špecializovanejšie sú rozloženia na špecifiká angličtiny, tým menej sa prenášajú zlepšenia na slovenčinu.

## Pozorovania

- Z rozložení, čo som skúšal, mal Colemak-DH najlepšie výsledky
- Najčastejšie písmeno v slovenčine je `o`, ale v angličtine (a vo [veľkom množstve][common-letters] západných jazykov) je to `e`, čo je smola, lebo `e` má častokrát jedno z najlepších miest
- Medzi Colemak-om a Colemak-DH nie je v slovenčine prakticky žiaden rozdiel, pokiaľ sa aplikuje na oba [angle mod][angle-mod] (Colemak táto zmena zníži na 1,936)
- Aj keď oba majú pomerne dobré výsledky, majú značné využitie vnútorného stĺpca, čo sa prejavuje hlavne na ortogonálnych a stĺpcových klávesniciach

## Obmedzenia

- Táto analýza využíva model použitý na [analýzu Colemak-DH][upstream], takže ho (samozrejme) preferuje
- Využíva iba uni- a bi-gramy; nebeží na skutočnom texte
- Tieto dáta sú vytvorené [z textov Wikipédie][simia] (z 2012), nie z korpusu
- Iba top sto n-gramov bolo použitých (chýba archív dvojgramov, tak sú iba scrapenuté zo stránky)
- Chýbajú štatistiky interpunkcie, hlavne di-gramov s písmenami, ktoré nechýbajú v originálnom datasete

## Tepelné mapy

Generované pomocou interaktívneho nástroja. Ak chcete skúsiť iné rozhrania alebo nastavenia, nájdete ho [nižšie](#nstroj).

<figure>

![Qwerty (angličtina)](/assets/img/slovak-layout-analysis/en-qwerty.png)
![Qwerty (slovenčina)](/assets/img/slovak-layout-analysis/sk-qwerty.png)

  <figcaption>
    Qwerty (angličtina vs. slovenčina)
  </figcaption>
</figure>
<figure>

![Dvorak (angličtina)](/assets/img/slovak-layout-analysis/en-dvorak.png)
![Dvorak (slovenčina)](/assets/img/slovak-layout-analysis/sk-dvorak.png)

  <figcaption>
    Dvorak (angličtina vs. slovenčina)
  </figcaption>
</figure>
<figure>

![Workman (angličtina)](/assets/img/slovak-layout-analysis/en-workman.png)
![Workman (slovenčina)](/assets/img/slovak-layout-analysis/sk-workman.png)

  <figcaption>
    Workman (angličtina vs. slovenčina)
  </figcaption>
</figure>
<figure>

![Colemak (angličtina)](/assets/img/slovak-layout-analysis/en-colemak.png)
![Colemak (slovenčina)](/assets/img/slovak-layout-analysis/sk-colemak.png)

  <figcaption>
    Colemak (angličtina vs. slovenčina)
  </figcaption>
</figure>
<figure>

![Colemak-DH (angličtina)](/assets/img/slovak-layout-analysis/en-colemak-dh.png)
![Colemak-DH (slovenčina)](/assets/img/slovak-layout-analysis/sk-colemak-dh.png)

  <figcaption>
    Colemak-DH (angličtina vs. slovenčina)
  </figcaption>
</figure>

## Čo ďalej

Pre mňa asi nič, ale pre záujemcov je viacero možností:

- SAV má k dispozícii [korpus slovenského jazyka][sav-corpus], ktorý by sa dal použiť na vytvorenie lepšej analýzy. Na jeho použitie ale treba ale poslať podpísaný list
- Podobne by sa dal spraviť lepší korpus z Wikipédie, ktorý by obsahoval aj interpunkciu a nový obsah za posledných 11 rokov
- [bclnr/kb-layout-evaluation][kb-layout-evaluation] a [engram][engram] obsahujú mnohojazyčné analýzy, do ktorých by bolo zaujímavé napojiť slovenčinu

## Záver

Túto analýzu som začal, lebo som sa naučil Colemak-DH kvôli angličtine, a chcel som zistiť, či mi to nezhoršilo písanie po slovensky. Myslím, že aj takáto jednoduchá analýza stačí, aby sa dalo povedať, že nie -- možno dokonca až to, že to stojí za to.

Budem ešte písať o tom, prečo práve Colemak-DH, ale v skratke:

- Hociaké optimalizované rozloženie je lepšie ako Qwerty
- Colemak-DH je dostatočne dobrý; má veľmi slušné výsledky vo väčšine analýz, čo som videl
- Netreba podceniť námahu potrebná na prechod. Tu má Colemak-DH veľkú výhodu vďaka množstvu zdieľaných kláves (a ich prideleniu k rukám) s Qwerty
- Vďaka prechodovým rozhraniam [Tarmak][tarmak] sa dá naučiť aj popri práci
- Má širokú komunitu

## Nástroj

Výsledky môžete porovnať s [originálnou verziou][upstream].

<iframe id="iframe" style="border: medium none; height: 860px;" src="/slovak-layout-analyzer/index.html?undefined" width="680" height="860" frameborder="0">
</iframe>

[dvorak]: https://en.wikipedia.org/wiki/Dvorak_keyboard_layout
[colemak]: https://colemak.com/
[workman]: https://workmanlayout.org/
[colemak-dh]: https://colemakmods.github.io/mod-dh/
[common-letters]: https://www.reddit.com/r/europe/comments/7jsyv3/the_most_common_letters_in_different_european/
[angle-mod]: https://colemakmods.github.io/mod-dh/#angle-mod
[upstream]: https://colemakmods.github.io/mod-dh/analyze.html
[simia]: http://simia.net/letters/
[sav-corpus]: https://korpus.sk
[kb-layout-evaluation]: https://github.com/bclnr/kb-layout-evaluation/
[engram]: https://github.com/binarybottle/engram
[tarmak]: https://forum.colemak.com/topic/1858-learn-colemak-in-steps-with-the-tarmak-layouts/
