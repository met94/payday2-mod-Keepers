# Keepers - Menu Options Guide

**Where:** Mod Options (SuperBLT) -> **Keepers**.

Settings are saved to `...\PAYDAY 2\mods\saves\keepers.txt`. Most changes apply
live; a few (keybinds) may need the options menu to be reopened.

## Order modes

The two interaction controls can each apply one of these modes to the bot you
shout at:

| Mode | Behaviour |
| --- | --- |
| **Nothing** | No order; the vanilla shout/interaction happens. |
| **Stationary** | The bot holds the marked position even under fire, returns if pushed away, and crouches to reload. |
| **Use cover** | The bot holds the position but withdraws while badly hurt and returns after regenerating above 50% health. |
| **Patrol** | The bot moves between random covers inside the nav segment it was assigned to (usually 5-30 m). |

Mode icons appear next to the bot's name.

## Order controls

- **On control 'Shout'** (`primary_mode`) - mode applied by the primary
  interaction control, i.e. shout/interact. Default: **Use cover**.
- **On control 'Stop AI'** (`secondary_mode`) - mode applied by the secondary
  interaction control, i.e. stop AI. Default: **Patrol**.
- **Keybind mode** - mode applied by the "Order all bots to hold their
  position" keybind. Default: **Use cover**.

## Options

### Filter shouts

Prevents accidental orders when you shout at cops or interact with the world.
Modes:

- **None** - no filtering.
- **Only blocks** - orders are blocked unless you hold the filter key.
- **All** - all shouts are filtered; useful when you spam shout to mark cops.

The default filter key is **left shift**. It can be changed in
`mods\saves\keepers.txt`. Filtering applies to the primary interaction control
only.

### Delayed input to awaken bot in stealth

In stealth, the host can wake a bot by calling it with the secondary "Stop AI"
control. When enabled, the key must be held for 0.5 s so a bot is not woken by
accident. In loud, the same input applies the behaviour that is not assigned to
the primary and secondary controls.

### Emulate 'stop AI' input

For VR players without a dedicated "Stop AI" button. Holding the interact
control for 0.5 s issues a "stop AI" event.

### TeamAIs can do interactions

Lets bots be sent to use anything accessible that does not require special
equipment. This relies on custom waypoints; see "Using GoonMod's Custom
Waypoints" below. In exchange, bot regeneration is weaker: health comes back in
chunks and the grace period is reduced.

### Faster but weaker while carrying

Halves the movement penalty while carrying a heavy bag, but also reduces the
regeneration rate. See the regeneration table below.

### Interaction timer multiplier

Slows down bot interactions. A value of 2 means a bot takes twice the normal
time to interact.

### Show jokers' health

Displays the joker's health bar to the right of its name.

### Show my jokers' name

Uses a custom name for your jokers.

### My jokers' name

The name itself. Applies to all of your jokers.

### Send my jokers' name

Shares your jokers' custom name with other players.

### Show other jokers' names

Displays the custom names other players gave to their jokers.

### Jokers move like TeamAIs

Jokers use the speed and suppression settings used by AI teammates.

## Keybinds

- **Order all bots to follow** - every bot returns to following you.
- **Order all bots to hold their position** - every bot holds its current
  position using the keybind mode.

## Using GoonMod's Custom Waypoints

Place a mark, shout at a bot, and it moves to the mark. Interaction targets work
the same way: mark an object, shout at a bot, and it walks there and interacts.

Whether the bot stays near the object afterwards depends on whether you keep or
remove the waypoint.

## Regeneration trade-offs

The interaction features reduce bot survivability on purpose. Regeneration per
event, by option combination:

| Objective | Vanilla | TeamAIs can do interactions | Faster but weaker while carrying |
| --- | --- | --- | --- |
| Follow player | 100% | 10% | 10% |
| Hold position | 100% | 10% | 10% |
| Revive teammate | 100% | 10% | 10% |
| Interact with an object | - | 5% | 5% |
| Take a bag | - | 5% | 5% |
| Carry/deliver a light bag | - | 10% | 10% |
| Carry/deliver a heavy bag | - | 10% | 5% |

The grace period drops from 0.35 s to 0.05 s when bots can do interactions
(SWAT van turrets keep the original value). These changes do not apply in
Holdout.
