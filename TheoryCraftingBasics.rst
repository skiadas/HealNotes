So you want to Healycraft?
===========================

This is what I hope to be the first in a series of posts aimed at introducing people to the wonderful world of healycrafting, namely theorycrafting for healer classes. This first post will attempt to define theorycrafting, and to introduce some of the basics of spells and stats. Later posts will discuss the nuances of particular specs.

So let's get started!

What is this Theorycrafting thing anyway?
-----------------------------------------

Theorycrafting is simply the study of the various spells and mechanics in World of Warcraft (and other similar games I suppose), with an emphasis in the details and numbers behind the spells. A common goal of theorycrafting is to determine the importance of each of your secondary stats for your class, as well as the overall performance of the class. But there's a lot of fun to be had on the way there!

As an example, consider a spell like Holy Light. Most people might just care that it is a cheap and small heal, and that they should use it at times with low incoming damage. A theorycrafter would focus on the exact amount that the spell heals, how much Illuminated Healing shield you'd get from it, how much of it would transfer to the beacon, whether the shield part would transfer to the beacon, exactly how haste would improve its cast time, exactly how stronger 200 more spellpower would make it, etc.

If you are happy just knowing that Holy Light is your cheap efficient heal, and that getting more spellpower will make it stronger, this article is probably not for you. Everyone else, follow me! 

You, yourself, and your stats
-----------------------------
In this post we will do a review of the core stats that affect our character's abilities. Each of these has a considerable effect in our healing.

Spellpower
~~~~~~~~~~
Spellpower is a stat that directly increases the size of your heals. Each heal has a base amount, and we add to that a multiple of our Spellpower by a specific coefficient. When you look up a spell in `WoWHead <http://www.wowhead.com>`_, its description usually contains these two numbers, and often a whole lot more.

We obtain Spellpower from the following sources:

1. Our weapon has a hefty amount of Spellpower on it.
2. Each point of Intellect past the first 10 adds one point of Spellpower.
3. There is a 10% Spellpower raid buff that is provided by `Mages <http://www.wowhead.com/spell=1459>`_, `Shamans <http://www.wowhead.com/spell=77747>`_, `Warlocks <http://www.wowhead.com/spell=109773>`_, or `Hunter Water Strider pets <http://www.wowhead.com/spell=126309>`_.
4. Some classes have their own abilities that boost it further, namely `Priest's Inner Fire <http://www.wowhead.com/spell=588/inner-fire>`_ and `Shaman's Earthliving Weapon <http://www.wowhead.com/spell=51730/earthliving-weapon>`_.

As a quick example, suppose a Priest has 15000 Intellect, a weapon with 6600 Spellpower on it, has `Inner Fire <http://www.wowhead.com/spell=588/inner-fire>`_ active and receives the raid buff, their effective Spellpower would be:

.. math:: \left(15000 - 10 + 6600\right) \times 1.1 \times 1.1 = 26124

Intellect
~~~~~~~~~
Intellect is our primary stat. Not as glorious as in the old days where it was increasing our mana pool, but it essentially does two things:

1. It provides us with `Spellpower`_ at a rate of 1 spellpower for every Intellect point past 10.
2. It increases our `Critical Strike Chance`_ at a rate of 0.0003951% per point of Intellect. This translates to roughly 2531 Intellect for 1% Crit Chance.

Intellect appears in all our gear, and some enchants, and we can gem for it using a gem containing red (i.e. red, purple or orange). More on that in our Gemming section however. Also, a lot of proc effects from trinkets or profession enchants provide Intellect.

Our standard sources of Intellect are as follows:

1. Every class has a base Intellect, that can further vary by at most 1 by race (and I will choose to ignore it). They are as follows: 

    :Priest: 206
    :Paladin: 108
    :Druid: 169
    :Shaman: 138
    :Monk: 143

2. We get an amount of Intellect from our gear, that varies with the gear's item level.
3. We can receive Int boosts from `flask <http://www.wowhead.com/item=76085>`_ or `food <http://www.wowhead.com/item=74650>`_, most usually in the form of the `banquet <http://www.wowhead.com/item=74919>`_.
4. A raidwide "all stats" buff provides a 5% boost. This boost does NOT however include the base Intellect amounts described above. This buff is provided by `Paladins <http://www.wowhead.com/item=74919>`_, `Monks <http://www.wowhead.com/spell=115921>`_, `Druids <http://www.wowhead.com/spell=1126>`_, or `Hunter Shale Spider pets <http://www.wowhead.com/spell=90363>`_.
5. All classes receive a further 5% multiplier if they are wearing only gear appropriate to the class: cloth for `priests <http://www.wowhead.com/spell=89745>`_, leather for `druids <http://www.wowhead.com/spell=86093>`_ and `monks <http://www.wowhead.com/spell=120224>`_, mail for `shamans <http://www.wowhead.com/spell=86100>`_ and plate for `pallies <http://www.wowhead.com/spell=86103>`_.
6. Druids would receive an extra 6% to their Intellect if they talent into `Heart of the Wild <http://www.wowhead.com/spell=108288>`_.
7. Lost of effects give you temporary Intellect boosts, but we don't usually take those into account when computing someone's Intellect. *You do however need to keep the multiplier factors in mind when evaluating those effects*.

As a quick example, let's consider a Priest in all cloth, who has flasked for Intellect and eaten the 250 food, and has 15100 Intellect in her gear (notice this is not the same as the value appearing in your character sheet!). She also is wearing only cloth gear (as if she had a choice!) and is receiving the raid buff. Then her Intellect amount would be:

.. math:: \Bigl(206 + \left(15100 + 1000 + 250 \right) \times 1.05\BigR) \times 1.05 = 18242

If this priest now gets a new piece of gear with 100 more Intellect on it, her Intellect amount would actually increase by :math:`100\times 1.05 \times 1.05 = 110.25`, as it would be affected by both her cloth specialization and the raid-wide buff.


Haste
~~~~~
Haste is a percent number that determines how fast your spells can be cast. The way it works is as follows:

1. Each spell has a default cast time, some times reduced by a talent. For example, `Nourish <http://www.wowhead.com/spell=50464>`_ has a 2.5 second cast time, but if we were using the `Glyph of Rejuvenation <http://www.wowhead.com/spell=17076>`_ it would be reduced by 30%, down to 1.75 seconds, when enough rejuvs are ticking. Haste can further reduce this cast time, essentially with the formula:

.. math:: \textrm{Cast Time} = \frac{\textrm{Base Cast Time}}{1 + \textrm{Haste}}

For example, if we had a haste of 15%, then the plain Nourish's cast time would become :math:`2.5/1.15 = 2.17` seconds. If it was a Nourish under the effect of the glyph, then its cast time would become :math:`1.75/1.15 = 1.52`.

2. Haste also reduces the *Global Cooldown (GCD)* by the same formula. The GCD is how much time you need to wait after using an instant cast, before you can cast something else. It has a base value of 1.5 seconds, and it is reduces by haste in the same way as spells, but it can never go below 1 second. This establishes a *soft cap* on haste percent, of 50%. Beyond that haste amount spell cast times still benefit from it, but the GCD does not.
3. Finally, and perhaps most importantly, Haste may affect the number of ticks that a *heal-over-time (HoT)* spell may have. But more on that later when we discuss HoTs.

Our haste percent is affected by the following factors:

1. First off, we receive *Haste Rating* from our gear. This is converted into a haste percentage at a rate of 1% for each 425 rating points. This will further be enhanced by the following multiplicative factors. We will discuss how those factors enter the equation at the end.
2. A raid buff provides a 5% multiplicative factor to haste. This buff can be brought by `Elemental Shamans <http://www.wowhead.com/spell=51470/>`_, `Balance Druids <http://www.wowhead.com/spell=24858>`_, `Shadow Priests <http://www.wowhead.com/spell=15473>`_, or a `Hunter's Sporebat pet <http://mop.wowhead.com/spell=135678>`_.
3. Shamans that have specced into `Ancestral Swiftness <http://www.wowhead.com/spell=16188>`_ receive an extra 5% multiplier.
4. Paladins receive a 10% multiplier from `Seal of Insight <http://www.wowhead.com/spell=20167>`_.
5. `Bloodlust <http://mop.wowhead.com/spell=2825>`_/Heroism would provide a 40 second 30% haste buff. This can be brought by `Shamans <http://mop.wowhead.com/spell=32182>`_, `Mages <http://mop.wowhead.com/spell=80353>`_, or `Hunters with a Core Hound pet <http://mop.wowhead.com/spell=90355>`_.

All these effects act *multiplicatively*. What we mean by that is the following: If you have say 13% haste from rating, and you want to factor in the 5% raid buff factor, you have to compute :math:`1.13\times 1.05 = 1.1865`, your new haste percent will therefore be 18.65%. As we would use the haste in computations as the 1.1865 factor anyway, this way of computing things sort of makes sense.

As an example, let's consider a Paladin with 2340 haste rating in her gear, and suppose she is in a raid where she receives the 5% buff. Her haste percent before any effects would have been :math:`2340/425 = 5.5%`. With the 5% buff, and the 10% that Paladins get, this becomes

.. math:: 1.055\times 1.05 \times 1.1 = 1.218525

or 21.85%. Now, if she further happens to be casting during Heroism, her haste percent would become :math:`1.218525\times 1.3 = 1.584`, or 58.4%.

Critical Strike Chance
~~~~~~~~~~~~~~~~~~~~~~
Critical Strike Chance is a percent value that determines the chance that your heal will be a *critical strike*. This means that it will heal for double the amount, with the exception of Discipline Priests where things are lot more complicated. However, critical strikes often have important side-effects:

1. For Discipline Priests they will trigger their `Mastery <http://www.wowhead.com/spell=47515>`_.
2. A critical strike with `Holy Shock <http://www.wowhead.com/spell=20473>`_ will trigger `Infusion of Light <http://www.wowhead.com/spell=53576>`, which in turn reduces the cast time of other spells.
3. A critical strike for a Resto Shaman will proc both `Resurgence <http://www.wowhead.com/spell=16196>`_ for some mana back and `Ancestral Awakening <http://www.wowhead.com/spell=51558>`_ for 40% of the heal being copied to a nearby player.

There are many more effects, but those are some of the most striking ones. One further thing to keep in mind is that the popular `Burning Primal Diamond <http://www.wowhead.com/item=76885>`_ increases the effect by 3%: In addition to the heal being doubled, it is further multiplied by an extra 1.03 factor.

Critical Strike Chance is determined as follows:

1. Each class has a base crit chance:

    :Priest: 1.235%
    :Paladin: 3.335%
    :Druid: 1.85%
    :Shaman: 1.235%
    :Monk: 2.19%

2. Our gear provides us with *Critical Strike Rating*, which is converted to a percentage at rate of 600 rating points for 1% of crit chance.
3. Our `Intellect`_ provides us with crit chance at a rate of roughly 1% for every 2531.
4. A raid buff can provide us an additive extra 5% crit rating. This buff is provided by `Guardian and Feral Druids <http://mop.wowhead.com/spell=17007>`_, `Mages <http://mop.wowhead.com/spell=1459>`_, `Windwalker Monks <http://mop.wowhead.com/spell=116781>`_ or `any <http://mop.wowhead.com/spell=97229>`_ `number <http://mop.wowhead.com/spell=24604>`_ `of <http://mop.wowhead.com/spell=90309>`_ `Hunter <http://mop.wowhead.com/spell=126373>`_ `pets <http://mop.wowhead.com/spell=126309>`_.

For example, let us suppose a Resto Druid has 18467 Intellect after all effects are accounted for, and she has 1340 crit rating in her gear. And suppose she receives the raid buff as well. Then her critical strike chance would be:

.. math:: 1.85 + 1340/600 + 18467/2531 + 5 = 16.38%

It is worth noting that a few spells, notably `Holy Shock <http://www.wowhead.com/spell=20473>`_ and `Regrowth <http://www.wowhead.com/spell=8936>`_ have considerably higher chance to crit, as does `Healing Surge <http://www.wowhead.com/spell=8004>`_ under the effects of `Tidal Waves <http://www.wowhead.com/spell=51564>`_. All these effects are additive.

Mastery
~~~~~~~
Mastery is a relatively new stat, and it is unusual in the sense that it behaves extremely differently for each class. We accumulate mastery in the form of mastery rating, and this is converted into a percentage effect for each class. In the old days there used to be an intermediate step *Mastery Points*, which was independent of the spec, and I will use this same system here, even though Blizzard effectively skips this step when showing our mastery in the character sheet. So our discussion of Mastery has two parts: One part is how the Mastery Points are computed, an the second part explains what those points translate to in the various specs.

Mastery Points come from the following sources:

1. Everyone receives 8 mastery points to start with.
2. Our gear provides us with Mastery Rating, which gets converted to Mastery Points at a rate of 600 Rating for 1 Mastery Point.
3. A raid buff provides us with another 3000 Mastery Rating, or equivalently 5 Mastery Points.

These are all added together. For example, someone with 2145 Mastery Rating in their gear, and receiving the raid-wide mastery buff, would have in terms of Mastery Points:

.. math:: 8 + 2145/600 + 5 = 16.575

Different classes use Mastery in different ways. We'll provide only a brief mention here, as masteries will be examined in greater detail when we analyze each class individually.

    :Disc: Increases all heals by 0.8% for each Mastery Point, and all shield effects by 1.6% for each Mastery Point.
    :Holy: Places a 6 second hot equal to a percent of the original heal, 1.25% for each Mastery Point.
    :Paladin: Places a stacking shield equal to a percent of the heal, 1.5% for each Mastery Point.
    :Druid: Increases the effect of heals by a percent, 1.25% for each Mastery Point.
    :Shaman: Increases the amount of healing based on the target's health deficit and a involving a percent computation based on Mastery, 3% for each Mastery Point.
    :Monk: Heals give a chance to spawn a Healing Sphere next to an injured ally.

Spirit
~~~~~~
Though not directly affecting the strength of our spells, Spirit affects our `Mana Regeneration`_, which affects our ability to keep casting spells without running out of mana.

Mana Regeneration
~~~~~~~~~~~~~~~~~
In Mist of Pandaria, we have a fixed initial mana pool of 300,000 mana. Almost all our spells cost mana to cast, and we have various sources of mana generation to make up for that loss. The difference between the outgoing mana and the incoming mana can determine how long we can go on casting before we run out of mana. All this will be the subject of a future post.

What's Next
-----------
Thus ends our first journey into the wonderful world of theorycrafting. You've learned what the various stats do and how to compute them. :doc:`Next up <TheColorOfHeals>`, we'll tackle more specifically how these stats affect spells, and how to measure how well each stat performs.
