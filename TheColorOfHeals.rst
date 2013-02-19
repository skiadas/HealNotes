The Color Of Heals
==================

Excuse the title, but I've been reading about CSS3 color schemes lately. In our :doc:`first installment <TheoryCraftingBasics>` we briefly described what theorycrafting and healycrafting are, and then went into a detailed description of the various stats that affect their heals, and how to compute them.

In this, more *colorful* (yes, I went there), installment, we'll tackle the age-old question: How do your heals grow? How is the amount of a heal computed exactly, and how do the various stats enter the picture? How do we measure the effectiveness of each stat?

Heals on Wheels
---------------
Okay I might be getting a bit out of hand with my section titles, but let's push on. First off, how is the heal amount determined, and what things do we measure on spells?

Every spell has 3.5 key parts to it, by which I mean 3 main parts and 1 secondary part (yes yes, I know you are probably all aware of these parts, but it's still worth mentioning them isn't it?):

1. First off, the *Heal amount*, exactly how many hit points it would recover. Affected mostly by spellpower, but also by mastery. We often consider however the *Average Heal amount*, which tends to include the effects of crit.
2. *Cast time*, how long it takes to cast the spell. Affected by haste, and occasionally special spell effects.
3. *Mana cost*, how much of a drain on our resources casting the spell is. Just like a dead DPS does no damage, a *manaless healer does not healing*. Mana costs tends to remain unaffected by stats, but on occasion some other spell effects might affect it. `Inner Will <http://www.wowhead.com/spell=73413>`_ for instance makes instant cast spells cheaper for priests.

One thing to note is that in `WoWHead <http://www.wowhead.com>` tooltips, the spell costs are expressed as a percent of your "base mana". This total mana amount would be usually 300k, except for classes that have non-intellect-based specs. In that case, those percentages refer to a 60k mana pool, as that is the mana pool for non-intellect-based specs. For example druids have feral forms, so looking at regrowth with a cost of 29.7% of base mana translates to :math:`0.297\times 60000 = 17820`. These classes seem to be inconsistent in how they deal with spells that are specialization only, so just be aware of this possibility when examining spell costs.

3.5. *Spell side-effects*, a catchall phrase for all the other things the spell does that we might care for. For instance mastery often causes the spell to produce a shield, or an extra hot etc. Other times the spell triggers another healing effect, for instance Shaman single target critical heals trigger `Ancestral Awakening <http://www.wowhead.com/spell=51558>`_.

When evaluating a spell's effectiveness, there are a number of different metrics we can use:

1. *Average Healing amount*: How much does the spell heal *on average*, ideally including its possible side-effects.
2. *HPS (Healing per Second)*: This is the average healing amount divided by the spell's cast time. It is what we often use to measure a spell's throughput, or when we want to just evaluate how haste affects things.
3. *HPM (Healing per Mana)*: This is the average healing amount divided by the spell's mana cost. It is of paramount importance when we consider a spell's efficiency. It tells you how much healing the spell provides per point of mana. Since we have limited mana resources in most cases, this places limits on how much we can effectively heal.
4. *MPS (Mana per Second)*: The spell's mana cost divided by its cast time. While not directly related to a spell's healing output, it is a factor when we consider how quickly we'll deplete our mana pool. This is often compared to the *incoming mana per second* that we get from the various mana sources at our disposal.

It's Formula Time!
------------------

Let's take a look at the basic formulas around our healing. First of all, we've got the basic heal number that we see when we hover over a spell. If you view a spell in WoWHead, you may see something like this (this is the values for Nourish):

    Heals a friendly target for 6151 to 7148 (+ 61.4% of SpellPower).

This has two components: The first is a *base amount*, typically denoted by B. In our case it is actually a range, from 6151 to 7148. What this means is that when we cast the spell, a number in this range is randomly selected to be used, all those numbers having an equal chance to occur. This is the only reason you see slight variations in the amounts your spells heal. In order to simplify matters, we tend to go with the average of those values as our B. In Nourish's case, that would be 6649.5.

Then we've got the spellpower coefficient, usually denoted by c. It is 61.4% in this case. What this means (duh!) is that the base heal amount is further increased by that percentage of our spellpower. For example if a druid has 21435 spellpower, then the actual average base heal amount of a Nourish would be :math:`6649.5 + 0.614\times 21435 = 19810.6`. In practice, the heal would actually vary from :math:`6151 + 0.614\times 21435 = 19312.1` to :math:`7148 + 0.614\times 21435 = 20309.1`.

This is the basic mechanic for most spells. There are exceptions, and HoTs behave somewhat differently, but those would be topics for later. For now, let's just summarize the formula for the base healing amount:

.. math:: H = B + c \times S

where S represents our spellpower, and H represents the healing amount.

This number is the number you typically see in-game when you hover over a spell. That's not always the case however. For instance if you are on a Disc Priest and you've just used `Archangel <http://www.wowhead.com/spell=81700>`_, then you're likely to see those numbers increased by 25%, i.e. by a factor of 1.25. There's often similar "constant factor" effects, that we collectively represent as a constant factor at the beginning of the formula, like so:

.. math:: H = k( B + c \times S )

Now, for some specs, their mastery provides them with an extra heal to an amount equal to a percentage of the base heal. For example let's say that a Druid as 16.8% mastery. This would mean that their direct heals like Nourish would in fact be 16.8% stronger, so we would have to multiply the above formula by 1.168. Or the effect might be more like the pally's mastery, which adds that extra percent as a shield instead of increasing the base heal. But the net effect is the same, the overall healing amount needs to be multiplied by 1+M, where M is the mastery percent. We therefore arrive at:

.. math:: H = k( B + c \times S ) ( 1 + M )

Of course different masteries work differently, but this will give us some basic understanding of how to compare things.

This is essentially the general formula for the base healing effect. The next step is to consider the effect of critical strike chance. Excluding side-effects for the moment, a critical heal provides double the amount of healing. If C represents our healing percentage, then this is what would happen C of the times, while the remaining 1-C of the times our heals would be regular. To get a combined effect therefore we could do:

.. math:: \textrm{AvgH} = (1-C) H + C 2 H = (1 + C) H

So critical strike has a similar 1 + C factor effect, and gives us a formula for the average heal:

.. math:: \textrm{AvgH} = k( B + c \times S ) ( 1 + M ) ( 1 + C )

This is in essence the key formula used to compare different stats, and we'll discuss the basics of this comparison in the next section. but before we do so, let's consider how this would change if we want to switch to HPS: Remember that HPS is the average healing amount, but divided by our cast time. Our cast time in turn is a base cast time, divided by 1 + H where H is our healing percent. When we put this all together, that 1 + H factor in the denominator ends up in the numerator of the whole thing, and the final formula looks like this:

.. math:: \textrm{HPS} = \frac{k}{\textrm{Base CT}}( B + c \times S ) ( 1 + M ) ( 1 + C ) ( 1 + H )

Stat Weights, or something like it
----------------------------------

If you got lost in the previous section, the last two formulas are the key ones to remember. They express our average healing amount and our HPS in terms of our spellpower, mastery, crit chance, haste, and the spell's characteristics, the base amount B and spell coefficient c.

Now, on to the real question we should be asking ourselves: How do we determine which stat is best? Should we get 100 more crit or 100 more mastery? or 100 more haste? We need a convenient way to see how much each of these stat increases benefits us.

At first glance, this shouldn't be that hard: If you want to see how much for instance 1% extra mastery would increase your spell, just add and amount :math:`\Delta M = 0.01` to the mastery M in the above formula, and you'd get:

.. math:: \textrm{New AvgH} = k( B + c \times S ) ( 1 + M + \Delta M ) ( 1 + C )

If we look at the difference between the new and old, we get:

.. math:: \textrm{New AvgH} - \textrm{Old AvgH} = k( B + c \times S ) (\Delta M) ( 1 + C )

So as you can see to get the actual amount of increase, we essentially multiply the increase in mastery with all the other factors in the equation, that basically remain unchanged. This is all fine and swell, and we could for instance do the same thing for crit and compare the two effects. But as it stands, this has a number of limitations, the most important of those being that it depends on the heal we consider. Different heals would give us different, um, differences.

This is where the wonderful world of *relative increases* enters. Instead of just looking at the difference in Average Healing (or HPS), look at that difference relative to the old amount:

.. math:: \textrm{Relative AvgH increase (RI)} = \frac{\textrm{New AvgH} - \textrm{Old AvgH}}{\textrm{Old AvgH}}

When we do this, all the extra factors will cancel out, and we are left with:

.. math:: \textrm{RI} = \frac{\Delta M}{1+M} = \frac{1}{1+M}\Delta M

This is absolutely brilliant! If we want to consider the relative increase that a stat provides, all that matters (with few exceptions) is how much of that stat we have!

Say that out loud with me again: If we want to consider the relative increase that a stat provides, all that matters (with few exceptions) is how much of that stat we have!

Say it a third time: Ok maybe not, but it's just that brilliant!

For example let's suppose our healer in the above example has 20% mastery. Then if she were to get another 1%, her spells would all increase by

.. math:: \frac{0.01}{1.2} = 0.0083 = 0.83%

No matter what spell we look at (almost), no matter what the other stats are, 1% mastery will give us the same increase of 0.83%. One other consequence of this formula however is this:

    The more of a stat we have, the less our relative benefit from more of it.

Before we move on with comparison, let's not forget ratings. Mastery does not come in percents in our gear, it comes in ratings. Recall that 600 rating provides us with 1 mastery point, which then translates to a percent depending on the spec. If we look at a druid for instance, each mastery point is 1.25% mastery percent, so 600 rating translates to 1.25%. If we want to account for that in the above formula, we can factor it in:

.. math:: \textrm{RI} = \frac{1}{1+M}\times \frac{0.0125}{600} \Delta \textrm{MRating}

Therefore a druid with 20% mastery would be getting 0.001736% per point of rating, or 0.1736% relative increase for 100 points of rating.

Finally, some stat weights
~~~~~~~~~~~~~~~~~~~~~~~~~~

The reason this is useful is because we can establish a relation between the different stats using it. For instance, suppose that 100 mastery rating increases our healing by 0.2%, but 100 crit rating, worked out the same way, increases our healing by only 0.15%. Then we could assign weights to those two spells, indicating their relative significance, namely 1 mastery rating would equal 1.33 crit rating.

Typically we standardize things by assigning a weight of 1 to 1 point of spellpower, and computing everything else relative to that.

One thing to not forget is how the various buffs might affect things. For instance, 1 point of Intellect gives a lot more than 1 point of spellpower, so it's important to take that into account. On the other hand, the multiplicative haste effects end up not mattering, because they can all be thought of as extra constant factors in the main equation (the reason being the multiplicative nature of the haste calculations).

Fine I lied, I won't actually show you any stat weights yet. The above paragraphs do however describe how you would obtain stat weights in many cases. The only thing missing is a more detailed description of the effect of spellpower:

Putting the c in BC
-------------------

Most of the factors above have a simple form: (1 + M). Spellpower is different, it enters the question in the form:

.. math:: B + c\times S

It would seem at first that spellpower would be affecting different spells in different ways, and to some extent that's true, but to a smaller extend than you would think. Let's rewrite that last equation for a second:

.. math:: c\left(\frac{B}{c} + S\right)

Writing it this way makes it look a bit more like the others. That factor of c can be thought of as part of the constant k we put in front, representing all constant factors the spell might have going for it. The important part however, the one that determines how spellpower affects things, is the quotient :math:`\frac{B}{c}`. In fact, if we wanted to compute the relative increase from an added amount :math:`\Delta S` of spellpower, we would end up with:

.. math:: \textrm{RI} = \frac{1}{\frac{B}{c} + S}\times \Delta S

So the multiplying factor that determines the effect of spellpower depends on :math:`\frac{B}{c}` alone, and not on the individual values of B and c. Moreover, when we start computing these quotients for various spells, we find something very interesting:

    Each class has a B/c value unique to it, that most spells follow closely.

Therefore spellpower has a different value for each class, but that value tends to be consistent across all spells of that class (with few notable exceptions). We'll discuss this factor more closely when we consider each spec on its own.

Don't forget the multiplicative factors that affect spellpower, they would need to be taken into account.

Quick Wrap-up
-------------
Here's the key things to take from all this discussion:

1. The average healing or hps provided by a spell is typically a product of factors, each representing a stat.
2. When considering *relative increases* to hps from a stat increase, this often ends up related to only one of those factors. Stat benefits therefore can be isolated from the other stats when considering relative increases.
3. Comparing relative increases to each other provides us with a way to compare stats: Something that boosts your relative healing by 1% is twice as good as something that boosts it by only 0.5%.
4. Don't forget to account for multiplicative factors on all stats except haste, where they end up canceling out.
5. Look at Average Healing or HPS when looking for throughput, HPM when looking for efficiency.

In our :doc:`next installment <TheHoTFactor>`, we'll talk about HoTs and how haste affects them.