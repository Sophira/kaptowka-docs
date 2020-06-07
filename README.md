ʞɐdʇomʞɐ: An Unofficial Guide
==============================
By Sophie Hamilton (<https://twitch.tv/sophira/>)
Written 2020-06-07

ʞɐdʇomʞɐ (that is, "kaptowka" flipped vertically) is a one-shot multiplayer
Twitch game/interactive experience on Twitch, developed for the game jam Ludum
Dare 46 (<https://ldjam.com/events/ludum-dare/46/>) with the theme "Keep it
alive". It is available at <https://twitch.tv/kaptowkagame>. In order to play
you will require a Twitch.tv acccount, as the game is controlled via Twitch
chat.

It is developed by the following people:

* devantics/CruelMotivator (<https://devantics.itch.io/>)
* Felegz (<https://felegz.itch.io/>)
* Victory
* Aviktorov (<https://aviktorov.itch.io/>)

Premise
-------

The premise of the game itself is fairly simple. You control one of a number of
gardener bots in a spaceship which is on its way to some unspecified
destination, and your job is to maintain the oxygen level so that the ship will
reach its destination.

You do this by planting and watering trees in each of the ship's 15 sectors, and
the stream automatically switches to a different sector every 6 minutes. A
minimum of 100 healthy trees are required in order to keep the oxygen level from
depleting, and the less trees there are, the faster the oxygen level will
deplete. The game ends, forever, when either the oxygen level hits 0% or the
ship reaches its destination (which will happen at midnight GMT on March 21,
2021).

Each of the ship's 15 sectors can hold up to 45 trees; thus, there are a maximum
of 675 trees that can be planted.

Giving Commands
---------------

Interacting with your gardening bot is achieved by typing commands in chat, upon
which your bot will carry out the command as far as it is able to do so. The
commands are:

* `!water` (`!w`): Water a tree in the given cell.
* `!plant` (`!p`): Plant a tree in the given cell.
* `!cut` (`!c`): Cut down a tree in the given cell (to be used when a tree has
                 died and can no longer be watered).
* `!dye` (`!d`): Dye a tree in the given cell to be the given hex colour.
* `!help`: Show the available commands.

The `!water`, `!plant` and `!cut` commands expect one or more cell references to be
given. For example, "!water a1 b1" will command your bot to water the trees in
cells A1 and B1. Each player gets their own individual bot.

Each of the commands, apart from !help, has a delay associated with it, in
addition to a nominal delay incurred by having your bot move to a new location:

* `!water`: Delays 30 seconds if your bot successfully waters a tree,
* `!plant`: Delays 90 seconds (1:30) if your bot successfully plants a tree,
* `!cut`: Delays 30 or 90 seconds *before* your bot successfully cuts down a
          tree, depending on whether the tree is dead or alive. If another
          player manages to cut down the tree before your delay is finished, the
          delay will be cut short.
* `!dye`: Delays 45 seconds if your bot successfully dyes a tree.

In each of these cases, no additional delay will be added if it is impossible to
do the given operation. For example, if the command `!water a1 b1` is given but
there is no tree (or a dead tree) in cell A1 while there is a live tree in cell
B1, the bot will move to cell A1, and then immediately move to cell B1, water
it, and delay for 30 seconds.

During the delay period, your bot cannot carry out any additional commands.
However, commands will be queued and your bot will carry out any new commands
you give it as soon as it is able to do so. There is no way to "unqueue" or
"cancel" commands that have already been given for the current sector, but when
a sector switch occurs, all queues are cleared automatically and all ongoing
delays from the previous sector no longer apply.

To dye a tree, the command is slightly different: `!dye (hex color) (cells)`.
For example, to dye the trees in A1 and A2 red, you might use the command 
`!dye #ff0000 a1 a2`. The dye will last until either the tree is dyed again, or
the tree dies.

Particular notice must be given to the `!cut` command. Unlike each of the other
commands, the delay for this command occurs before it is actually carried out,
instead of afterwards. In addition, the delay is only 30 seconds if the tree is
already dead, but a full 90 seconds if the tree is still alive. This limits the
potential for trolls, but it does mean that if the sector switch timer is under
30 seconds, you will not be able to successfully cut a dead tree, even when you
could successfully plant or water a tree in another cell.

Note that the game will ignore any chat that doesn't appear to be a valid
command, so you can feel free to use the Twitch chat to talk to other players.

The Lifecycle of Trees
----------------------

Upon being planted or watered, a tree will be "healthy" and contribute to the
ship's oxygen for the next 5 hours (about 3-4 complete ship rotations), at which
point it will become "unhealthy", start shedding leaves, and stop contributing
to the ship's oxygen. It will stay in this state until it either dies or is
watered. An unhealthy tree will take about 7 hours to die from when it first
becomes unhealthy, and the age of an unhealthy tree can be gauged by the colour
of the leaves on the branches, which turn a brown colour over time. (If the tree
has no visible leaves on its branches, but can still be seen shedding leaves, it
is about to die and should be watered as soon as possible.)

Once a tree dies, it can no longer be watered and needs to be cut before another
tree can be planted in its spot. As the process of cutting and replanting takes
a full 2 minutes of time - as opposed to 30 seconds for watering a tree - it is
highly preferable to water trees instead of waiting for them to die.

A dead tree is represented as a bare tree trunk with no leaves on its branches
and no leaf falling animation. Please note that as long as the leaf falling
animation is still playing, *the tree is alive and should be watered*, even if
it looks like there are no leaves on the branches! If in doubt, always attempt
to water first - if the tree is dead after all, there will not be any delay
incurred beyond the time spent moving to the cell.

The Oxygen Level
----------------

When the number of trees falls below 100, the oxygen level will start to fall,
and a timer will appear showing how long it would take for the oxygen level to
fully deplete if there were no healthy trees left. (Note that this timer will
not be correct as long as there are healthy trees remaining; the more healthy
trees there are, the slower it will take for the oxygen level to deplete.)

If the number of healthy trees goes back above 100, the depletion timer will
disappear and the oxygen level will start to rise again. The more healthy trees
above 100 that there are, the faster the oxygen level will replenish.

If the oxygen level falls to 0%, the game will end.

Playing with Multiple Players
-----------------------------

As mentioned earlier, the game is multiplayer and each player gets their own
gardening bot to control. This can lead to situations where multiple players
queue up the same commands, trolls attempt to ruin the game, etc.

In the case of multiple commands issuing the same commands, what each bot will
do depends on what state the cell is in after the bot moves there, when it
attempts to carry out the command; as long as the conditions are right to carry
out the command, it will be carried out and the associated delay incurred,
regardless of whether other players are or will be attempting to do the same.

The delay does *not* get shortened in the case of multiple players doing the
same operation, except where this involves cutting a tree; in this case, any
player in the process of cutting a tree will stop as soon as the cell no longer
contains a tree to cut, with any remaining delay being cancelled.

for example, if two players attempt to `!cut` the same dead tree, and the cell
is not empty for either player at the moment their bot arrives at the cell, both
will start to incur a delay of 30 seconds. However, as soon as the first player
finishes their cut, the second player's remaining delay will be cancelled and
the bot will go on to carry out any commands queued for it.

Occasionally, someone will accidentally (or deliberately) cut a live tree. More
than likely, it will have been a mistake, but in any case, the additional delay
for cutting a live tree - and the fact that this delay occurs before the cut
actually happens - ensures that a troll will have a significant disadvantage in
actual play against even a solo player. As always, the best method to defeat a
troll is to ignore them, if possible.

Strategies for Optimal Play
---------------------------

There are certain strategies which are worth bearing in mind:

1.  First, and most important - relax! The game is deliberately balanced so that
    even a solo player can successfully maintain the ship's oxygen level in most
    cases, and the oxygen timer is very generous. There's a reason that the
    stream plays calming music - it's intended to be fun and relaxing, not
    stressful.

    You do not have to dedicate hours to the game, or play optimally, in order
    to make a difference; it's okay to take breaks, and the game has plenty of
    regular players. I myself frequently go several days without participating,
    despite being a regular player, because I can see that the players in chat
    already have things well in hand.

2.  On the same note, while the strategies below are useful, they are not
    required to play. Again, the idea is to have fun. If anybody berates you for
    not following these strategies, they are being toxic and you should try to
    ignore them if you can. (I have never seen this happen, however - everyone
    seems to be pretty chill.)

3.  Unless you're short on time, it can sometimes be best to start off with just
    one instruction; for example, if you intend on watering trees A1 through A5,
    start off with just a single `!w a1`. This has several benefits:
 
    * Your bot can carry out the first command while you're typing the others.
    * When playing with multiple players, it can signal to the other players
      where you're thinking of moving next, making it easier to avoid stepping
      on each other's toes.
    * When playing with multiple players, it also lets you see where other
      people are moving. It may be that someone had the same idea as you but
      starts off with `!w a1 a2 a3 a4 a5`. If you had started off with this too,
      you would have both been stuck watering the same trees. By doing just `!w
      a1` first, you can avoid this situation and know to target other cells.

4.  Since you get 6 minutes of time in each sector, and each delay (apart from
    `!dye`) is a multiple of 30 seconds, it can be helpful to think of delays in
    30-second blocks, with each sector giving you 12 blocks of time to do your
    commands. With this frame of reference:
 
    * Watering a tree will delay 1 block of time,
    * Planting a tree will delay 3 blocks of time,
    * Cutting a tree takes either 1 or 3 blocks of time,
    * Dyeing a tree will delay 1.5 blocks of time.

5.  Remember that the delay period for everything (except for cutting) only
    applies after the associated action has already taken place, meaning that
    even if there's only 10 seconds left on the timer, that's still enough time
    for your bot to successfully plant a tree! Plan your commands around this.

6.  My own personal strategy is that assuming that I start issuing commands
    within the first 30 seconds of a sector appearing, and queue subsequent
    commands so that they're executed without breaks, I tend to use one of four
    command structures, depending on the situation (note: a "short" command
    means watering a tree/cutting a dead tree, while a "long" command means
    planting a tree or accidentally cutting a live tree):
 
    1. 1 short command first, followed by 4 long commands
    2. 4 short commands first, followed by 3 long commands
    3. 7 short commands first, followed by 2 long commands
    4. 10 short commands first, followed by 1 long command
 
    These structures are not always the most optimal, but they account for the
    time spent by the bot moving between squares, as well as taking advantage of
    the fact that delay periods occur after commands have been carried out in
    most cases, allowing me to sneak in a long command even when the timer has
    less than 1:30 left. They also mean that I only have four things I need to
    remember.

7.  When following the above structures, it is best to ensure that each of your
    6-minute turns ends with planting a tree, even if there are trees left to
    water.

8.  Taking into account the above two strategies, it is best for the rest of
    your commands to be to water trees first, then cut any that need cut, and
    then plant. That way, if you accidentally cut a live tree, there is a
    possibility that the increased delay caused by doing so means that it might
    not take effect before the sector switch occurs.

9.  Pay attention to the chat, if you can. The current version of the game does
    not highlight cells that other players are targeting in their queues
    (although this is planned for a future version), so optimal play involves
    looking at chat to see which commands are being queued. If you're so
    inclined, you can even calculate whether there's enough time for the
    commands made by other players to be carried out.

10. You can always see the entirety of the next sector coming up at any given
    time. You can use this to plan out your moves before the sector switches,
    but beware of other players doing this at the same time, as you may end up
    doing the same things as them. It may be worth agreeing with them first in
    chat as to what each of you will do.

Frequently Asked Questions
--------------------------

1.  **Is there a way to "cancel" or "unqueue" commands?**

    As of the current time of writing, no, there isn't. The only current method
    of doing this is when a sector switch occurs; at that point, all queues are
    reset.

2.  **Is it worth watering trees without leaves?**

    If a tree has no leaves on it, and does not have the leaf falling animation,
    the tree is dead and cannot be watered. At that point the only thing you can
    do with it is to cut it, freeing the cell up ready to be replanted.
 
    If the tree is still shedding leaves, you should water it as soon as
    possible, even if it appears to have no leaves on its branches.

3.  **The oxygen depletion timer that appears when the number of healthy trees
    goes below 100 is wrong!**

    That timer measures how fast the oxygen would deplete if there were no
    healthy trees at all. As long as there are healthy trees, the oxygen will
    deplete slower than shown, and will deplete slower still the more healthy
    trees there are.

4.  **What does "kaptowka" mean?**

    In Russian, "kaptowka" (Картошки) means "potato".

Conclusion
----------

Although ʞɐdʇomʞɐ is only a one-shot experience, it can be very relaxing. I hope
that this guide helps you to enjoy it further! If you have something you'd like
me to add, please contact me on Twitch - I'm available as "Sophira". If you
mention my name in the Twitch chat channel, I will probably see it immediately,
even if I'm not actively playing.

This document is also available as a git repository at
<https://github.com/Sophira/kaptowka-docs/>, and pull requests would be greatly
appreciated!

Have fun!
