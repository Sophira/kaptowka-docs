ʞɐdʇomʞɐ: An Unofficial Guide
==============================
By Sophie Hamilton (<https://twitch.tv/sophira/>)  
Last updated: March 21, 2021

ʞɐdʇomʞɐ (that is, "kaptowka" flipped vertically) was a one-shot multiplayer
Twitch game/interactive experience on Twitch, developed for the game jam Ludum
Dare 46 (<https://ldjam.com/events/ludum-dare/46/>) with the theme "Keep it
alive". It was available at <https://twitch.tv/kaptowkagame>. In order to play,
players required a Twitch.tv acccount, as the game was controlled via Twitch
chat.

It was developed by the following people:

* devantics/CruelMotivator (<https://devantics.itch.io/>)
* Felegz (<https://felegz.itch.io/>)
* Victory (<https://www.facebook.com/aitova.victory>)
* Andrey Viktorov/aviktorov (<https://twitter.com/aviktorov>)
* vrumie (<https://www.facebook.com/vrumie>)

**The game ended on March 21, 2021, with the ship arriving at its destination
with 666 healthy trees.** However, after the ending, players were allowed to
continue watering the ship until it got to 675 healthy trees, at which point the
game entered a 'museum mode', where it will stay for about a month. It is
currently no longer necessary to water any trees, and cutting is disabled,
leaving players free to use the `!dye` command as they desire.

Premise
-------

The premise of the game itself was fairly simple. Players controlled one of a
number of gardener bots in a spaceship which was on its way to some unspecified
destination, and their job was to maintain the oxygen level so that the ship
would reach its destination.

To do this, players planted and watered trees in each of the ship's 15 sectors,
with the stream automatically switching to a different sector every 6 minutes. A
minimum of 100 healthy trees were required in order to keep the oxygen level
from depleting, and the less trees there are, the faster the oxygen level would
deplete. The game would end, forever, if the oxygen level hit 0%, or if the ship
managed to reach its destination. On March 21, 2021, at midnight GMT, the ship
successfully reached its destination and the game ended.

Each of the ship's 15 sectors could hold up to 45 trees; thus, there were a
maximum of 675 trees that could be planted.

Giving Commands
---------------

Interacting with your gardening bot was achieved by typing commands in chat,
upon which your bot would carry out the command as far as it was able to do so.
The commands were:

* `!water` (`!w`): Water a tree in the given cell.
* `!plant` (`!p`): Plant a tree in the given cell.
* `!cut` (`!c`): Cut down a tree in the given cell (to be used when a tree had
                 died and could no longer be watered).
* `!dye` (`!d`): Dye a tree in the given cell to be the given hex colour.
* `!cancel`: Stops your current wait time and clears your command queue. Could
             only be used once per sector switch.
* `!help`: Show the available commands.

The `!water`, `!plant` and `!cut` commands expected one or more cell references
to be given. For example, `!water a1 b1` would command your bot to water the
trees in cells A1 and B1. Each player had their own individual bot.

Each of the commands, apart from `!cancel` and `!help`, had a delay associated
with it (during which an appropriately coloured wait timer would be shown with
an icon in the middle), in addition to a nominal delay incurred by having your
bot move to a new location:

* `!water`: Delayed 30 seconds if your bot successfully watered a tree,
* `!plant`: Delayed 90 seconds (1:30) if your bot successfully planted a tree,
* `!cut`: Delayed 30 or 90 seconds *before* your bot successfully cut down a
          tree, depending on whether the tree was dead or alive. If another
          player managed to cut down the tree before your delay was finished,
          the delay would be cut short.
* `!dye`: Delayed 45 seconds if your bot successfully dyes a tree.

(Of these commands, only the `!dye` command is still usable in museum mode, and
the delay has been reduced to 15 seconds.)

In each of these cases, no additional delay would be added if it was impossible
to do the given operation. For example, if the command `!water a1 b1` was given
but there was no tree (or a dead tree) in cell A1 while there was a live tree in
cell B1, the bot would move to cell A1, and then immediately move to cell B1,
water it, and delay for 30 seconds.

During the delay period, your bot could not carry out any additional commands.
However, commands would be queued and your bot would carry out any new commands
you give it as soon as it was able to do so.

Players could use the `!cancel` command once per sector switch to stop their
current wait time and clear their command queue.  This did not reverse the
action that took place, and so could be used to work in an extra `!plant`,
`!water` or `!dye`. In addition, when a sector switch occured, all queues were
cleared automatically and all ongoing delays from the previous sector no longer
applied.

To dye a tree, the command was slightly different: `!dye (hex color) (cells)`.
For example, to dye the trees in A1 and A2 red, you might use the command
`!dye #ff0000 a1 a2`. The dye would last until either the tree was dyed again, or
the tree died.

Particular notice must be given to the `!cut` command. Unlike each of the other
commands, the delay for this command occured before it was actually carried out,
instead of afterwards. In addition, the delay was only 30 seconds if the tree
was already dead, but a full 90 seconds if the tree was still alive. This
limited the potential for trolls, but it did mean that if the sector switch
timer was under 30 seconds, you would not be able to successfully cut a dead
tree, even when you could successfully plant or water a tree in another cell.

The game would ignore any chat that didn't appear to be a valid command, so
players could feel free to use the Twitch chat to talk to other players.

The Lifecycle of Trees
----------------------

**(note: This section may be outdated; I have not yet been able to confirm that
the game still works this way as of the update on August 18, 2020.)**

Upon being planted or watered, a tree would be "healthy" and contribute to the
ship's oxygen for the next 5 hours (about 3-4 complete ship rotations), at which
point it would become "unhealthy", start shedding leaves, and stop contributing
to the ship's oxygen. It would stay in this state until it either died or was
watered. An unhealthy tree would take about 7 hours to die from when it first
becomes unhealthy, and the age of an unhealthy tree could be gauged by the colour
of the leaves on the branches, which would turn a brown colour over time. (If the tree
had no visible leaves on its branches, but could still be seen shedding leaves, it
was about to die and thus needed watering as soon as possible.)

Once a tree died, it could no longer be watered and needed to be cut before
another tree could be planted in its spot. As the process of cutting and
replanting took a full 2 minutes of time - as opposed to 30 seconds for watering
a tree - it was highly preferable to water trees instead of waiting for them to
die.

A dead tree was represented as a bare tree trunk with no leaves on its branches
and no leaf falling animation.

The Oxygen Level
----------------

When the number of trees fell below 100, the oxygen level would start to fall,
and a timer would appear showing how long it would take for the oxygen level to
fully deplete if there were no healthy trees left. (This timer would not be
correct as long as there are healthy trees remaining; the more healthy trees
there were, the slower it would take for the oxygen level to deplete.)

If the number of healthy trees went back above 100, the depletion timer would
disappear and the oxygen level would start to rise again. The more healthy trees
above 100 that there were, the faster the oxygen level would replenish.

If the oxygen level fell to 0%, the game would have ended.

Playing with Multiple Players
-----------------------------

As mentioned earlier, the game was multiplayer and each player had their own
gardening bot to control. This could lead to situations where multiple players
queued up the same commands, trolls attempt to ruin the game, etc.

In the case of multiple players issuing the same commands, what each bot would
do depended on what state the cell was in after the bot moves there, when it
attempted to carry out the command; as long as the conditions were right to
carry out the command, it would be carried out and the associated delay
incurred, regardless of whether other players were or would be attempting to do
the same.

The delay did *not* get shortened in the case of multiple players doing the same
operation, except where this involved cutting a tree; in this case, any player
in the process of cutting a tree would stop as soon as the cell no longer
contains a tree to cut, with any remaining delay being cancelled.

For example, if two players attempted to `!cut` the same dead tree, and the cell
was not empty for either player at the moment their bot arrives at the cell,
both would start to incur a delay of 30 seconds. However, as soon as the first
player finished their cut, the second player's remaining delay would be
cancelled and the bot would go on to carry out any commands queued for it.

Occasionally, someone would accidentally (or deliberately) cut a live tree. In
most cases, this was a mistake, but in any case, the additional delay for
cutting a live tree - and the fact that this delay occured before the cut
actually happens - ensured that a troll would have a significant disadvantage in
actual play against even a solo player. As always, the best method to defeat a
troll was to ignore them, if possible.

Strategies for Optimal Play
---------------------------

As the game is no longer running, this section has been removed. However, it is
still available to view in the [commit archives on
GitHub](https://github.com/Sophira/kaptowka-docs/commits/master).

Frequently Asked Questions
--------------------------

Note: A few questions have been removed from this document as they no longer
apply in 'museum mode'. As with the above section, however, previous FAQs are
available to view in the [commit archives on
GitHub](https://github.com/Sophira/kaptowka-docs/commits/master).

1.  **My bot isn't showing up on some sectors, even when I give it commands.
    What gives?**

    Occasionally the game does this, and it can be annoying. My personal theory
    was that the game spawns your bot in the previous sector but the bot gets
    stuck on something sometimes, and the pathfinding algorithm can't figure a
    way out to the cell you told it to go to.

    The bot always seems to recover by the next sector somehow, but recently I
    discovereed a trick to work around it: If you use the `!cancel` command, and
    then direct the bot to go to the opposite side (left/right) of the board,
    the bot always seems to manage to make it there. For example, if you
    initially tried going to cell A1 and it didn't work, then you should
    `!cancel` and tell it to go to cell A5 instead (or another cell that's on
    the opposite side). Chance are good that it'll work.

    The downside, of course, was that you lose your one cancel for the sector,
    but it's better than not doing anything at all!

2.  **What does "kaptowka" mean?**

    "kaptowka" is the Russian word "картошка" represented by ASCII-only
    characters. The word means "potato" and would properly be transliterated as
    "kartoshka".

3.  **Has the maximum of 675 healthy trees ever been reached?**

    Yes! The maximum of 675 healthy trees has been reached three times now, and
    they all have clips!

    * [June 21, 2020 at 22:00:43 GMT](https://www.twitch.tv/kaptowkagame/clip/TentativeAgitatedBillDatBoi)
    * [January 17, 2021 at 03:16:22 GMT](https://clips.twitch.tv/AggressiveYummyFennelWholeWheat)
    * [February 27, 2021 at 19:53:27 GMT](https://www.twitch.tv/kaptowkagame/clip/SuaveFragileFloofFrankerZ-6BSujAxo8-FB-zO7)

    To the knowledge of this guide's creator, these are the only times this has
    happened thus far (as of February 28, 2021). If any are missing, please let
    me know!

Game Update History
-------------------

Note that there may have been other updates to the game which I did not notice;
this section details only the major changes.

* **July 20-21, 2020 (approx)**: The number of healthy trees required for the
                                 oxygen level to be stable was raised from 100 to
                                 200.

* **August 18, 2020**: The UI was refreshed (colours and icons for wait times,
                       fans on both sides of the ship and a visual update for
                       the ship, plus a new skybox) and some rebalancing occurs.
                       The `!cancel` command was added. The number of healthy
                       trees required for the oxygen level to be stable was set
                       back to 100 again.

* **March 21, 2021**: The ending was added to the game. In addition, new
                      graphics and graphical effects were added, including
                      dynamic shadows, a rotating planet in the background, and
                      (for the museum mode) a swarm of gardener bots, one for
                      each player who participated in the game.

Conclusion
----------

Although ʞɐdʇomʞɐ was only a one-shot experience, it was very relaxing for the
people who played it. Thank you to everybody who participated!

Particular thanks must go to the developers of the game: **CruelMotivator, felegz,
Victory, aviktorov and vrumie**. Thank you for creating an experience where
people could hang out, relax, and enjoy themselves while helping to keep a
spaceship alive!

If you have anything you'd like me to add to this document, please contact me on
Twitch - I'm available as "Sophira". If you mention my name in the Twitch chat
channel, I'll probably see it immediately, even if I'm not actively playing.

This document is also available as a git repository at
<https://github.com/Sophira/kaptowka-docs/>.
