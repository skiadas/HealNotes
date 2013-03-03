Popping Archangel while Atonement Healing
=========================================

It is common belief that when we Smite heal we want to keep Evangelism going, rather than popping Archangel. I decided to put this to the test. But before we do that, let's get some things straight: I am not discussing situations where you are going to switch between Atonement Healing and other things like PoH spam. In such an eventuality, and especially if those are going to happen with some regularity, it is unquestionably better to use Archangel with those. What I am interested in here is:

    If all we will be doing is Atonement, then is it still worth it using Archangel.

I will be measuring "worth it" in terms of total HPM over a 30 second window, which is Archangel's CD, as well as average HPS during that same window.

`TL;DR`_ at the bottom if you get bored.

The key issue
-------------
What is the big deal here? Popping Archangel gives us 25% increased healing for the next 18 seconds. What we pay for that is the loss of all our Evangelism stacks, which we will now have to rebuild. Evangelism gives us 4% more healing and 6% cheaper spells per stack, up to 5. The question basically is: does the 25% healing buff for 18 seconds make up for the loss of Evangelism for a few seconds? The 5 spells you cast right after Archangel will be costing considerably more than they otherwise would, but they would also be a bit stronger, and the buff lasts for about 4-5 spells after we've built our stacks again. It's a tradeoff, we'll see if it is worth it or not.

So let's get started. I will assume minimal haste, which brings our GCD and Smite cast time down to 1.4 seconds, and Penance cast time down to 1.85 seconds. I also will not be using the t14 4set bonus, and will therefore assume Penance has a 9 second CD.

Math time
---------
In order to make the comparison as much independent of our spellpower as possible, I will use the fact that my penances are on average 3.4 times stronger than my smites, and my holy fires are 1.25 times stronger, all this assuming the 20% buff that smite gets for being cast while the HF dot is up. I will therefore use the Smite Heal amount, heretofore abbreviated as SH, as my measuring unit.

To get warmed up, let's consider this 30 second window. Because of the current situation where Penance's CD does not align with Holy Fire's, I will try to simplify things a bit and assume that we'll be casting one Penance, one Holy Fire and 4 Smites on every 10 second cycle, then possibly wait up to a second. This same rotation would be valid even at 0 haste. So our basic cycle would be:

Penance > HF > 4 x Smite

and you can fill the odd time with a filler, like PW:S which then speeds up the next cast or Divine Star. But let's keep things simple for now.

Recall that each penance heals for 3.4 times a smite, and each holy fire for 1.25 times a smite, and we'll be getting 3 sets of these 6 spells in a 30 second window. Accounting for the 20% buff that these spells get from Evangelism, we'll be looking at:

.. math::

    \textrm{Healing} = 1.2\times 3\times (3.4+1.25+4\times 1) SH = 31.14 \textrm{SH}

In terms of mana cost, I will measure things as a percent of our total mana pool (TM). Smite costs 2.7%, Holy Fire costs 1.8%, Penance costs 3.1%, and Evangelism discounts those by 30%, so our total mana cost would be:

.. math::

    \textrm{Mana} = 0.7\times 3\times(3.1+1.8+4\times 2.7) = 32.97% \textrm{TM}

So it normal Atonement healing with Evangelism up full time costs us a total of 98910 mana every 30 seconds, to produce healing equal to 31.14 times our average Smite heal.

Archangel in the mix
--------------------

We will now compare this to what happens when we consider Archangel. There are three different approaches to when we could pop Archangel during the above rotation. The one approach is to pop it right before a penance, a second is to pop it right before Holy Fire, and the third is to pop it right before we start our 4 Smites. They all differ slightly in their costs and benefits, but essentially not enough to make much of a difference.

Let's stick to the first approach: Archangel right before the first Penance. Then the buff will last us through the 3rd Smite of the second set, and so Archangel will buff two penances, 2 holy fires and 7 smites. However the first few of those will not be buffed with archangel, so let's start adding things up. The healing of the spells affected by Archangel would be:

.. math::

    1.25\times (3.4+1.25\times 1.04+ 1.08+ 1.12+ 1.16+ 1.2 + (3.4 + 1.25 + 3)\times 1.2) \times  SH

or 23.05 times our average smite heal. We need to add to that the remaining spells, that are unaffected by Archangel but with a full effect of Evangelism, and that would be one penance, one holy fire and 5 smites, for total added healing of:

.. math:: 

    1.2\times (3.4+1.25+5) \times SH = 11.58 \times SH

Our total overall healing has therefore increased to 34.63 times our average Smite heal. This is an increase of about 11.2% in our healing.

In terms of mana costs now, the only difference is at the first 5 casts. We would need to use

.. math::

    (3.1 + 1.8 \times  0.94 + 2.7\times (0.88 + 0.82 + 0.76 + 0.7)) + 0.7\times 2\times (3.1+1.8+4\times 2.7)

or 35.304% of our total mana pool, or 105912 mana. This is an increase of 7% in our mana consumption.

TL;DR
-----
In total, our "healing per mana" would increase by 4%, and our "average healing per second" would increase by 11.2% respectively, if we use Archangel on CD while sticking to a basic Atonement rotation. These percentages only get better if you occasionally use other spells along the way (e.g. a Cascade or Divine Star buffed by that 25% of Archangel can make a big difference). Bottom line is:

    Archangel is worth using even if all you do is Atonement Spamming.

Also keep in mind that all you are trading is a few spells being more expensive, right after you've popped Archangel, for all your spells for the next 18 seconds being stronger, even more so after you have built your back stacks up. In other words, you want to pop Archangel about 5-6 seconds *before* you expect the damage to start getting a harder, if you plan to stick to Atonement as opposed to say Greater Heals.


I am not advocating using Atonement Healing right after you have popped Archangel, in fact you should be using our full arsenal of spells. But I am advocating that it is worth using Archangel even when all you are doing is Atonement Healing.
