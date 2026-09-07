# Game Input Compatibility QA

Game media values by its controls and interactivity, marking a difference from films. Therefore a slight bad input device support, or bad control correlates towards a bad game, but they could be fixed easily.
Although bad controls don't result in plane crash (or maybe...), the player gets tortured by them throughout the gameplay session, this means a more frustrated player base, more middle quitters / refunds, and less review positivity
Here is a non-negotiable, fundamental checklist that covers the minimum input and controls for games.
All points here are critical but minimum, try to do better than these lists, or ignore depending what your focuses.

| Controller Support              | Requirement                                                                                                                                                                     | Present (Y/N/-) |
|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| Joystick bounce back mitigation | Joystick bounce back overshoot does not cause unintended direction reverse                                                                                                      |                 |
| Controller UI                   | The UI menus are manipulated via joystick movement, LT/RT triggers, not indirectly manipulated by a cursor moved by joystick (mouse/touch UI)                                   |                 |
| Controller direction inverse    | No quick chaining of instantaneous direction reverse in gameplay (↔ or ↕), the long travel time of joystick does not allow it, games usually fail this on key-combo platforming |                 |

**Strongly Recommended, if development time allows:**
- Turn off controller vibration (then consider intensity adjustment)
- Supports both XBOX and PlayStation controller types
- Drift mitigation / re-calibration settings
- Joystick angle quantization customization (remap joystick angle to game character angle)
- Dead-zone customization to mitigate hardware/driver bugs

| Mouse Support             | Requirement                                                                                                                                                                                                                      | Present (Y/N/-) |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| Mouse Look                | If the game character turns slowly, then mouse look should be free from character look/aim direction (character catches up to look direction), the player do not have to move mouse constantly to remain turning (joystick look) |                 |
| Mouse Acceleration toggle | The game demands correct, accurate aiming, and in-game mouse acceleration can at least be turned off                                                                                                                             |                 |
| Mouse Smoothing toggle    | The game demands correct, accurate aiming, and in-game mouse smoothing can at least be turned off                                                                                                                                |                 |
| Mouse Sensitivity         | The game demands correct, accurate aiming, and at least provides mouse sensitivity adjustments                                                                                                                                   |                 |
| Mouse-wheel Consistency   | Mouse-wheel scrolling does not trigger key-press, nor changing game settings, unless the player binds it manually                                                                                                                |                 |
| DPI Compatibility         | Mouse sensitivity setting step size is <= 2, ideally 2-decimal float point, so mice ranging at least 400~16000 DPI (40x gap) are supported, 3-decimal for e-Sport games (requires fast & precise aiming)                         |                 |

**Strongly Recommended, if development time allows:**
- Raw mouse input, if demands accurate aiming
- Mouse icon color is enough different from background, or having border/shadow to differentiate

**Cut corners**
- On PC or personal-computer based consoles, game control settings UI can remain simple or never coded, that's ok——all the player need is a `.json`/`.ini` file to write into, and maybe a default file to reset

| Keyboard Support         | Requirement                                                                                                                                                                                                       | Present (Y/N/-) |
|--------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| Keyboard Sprint          | If the player character can sprint (run or move faster), then keyboard sprint (i.e., hold shift key or other combined input) must be implemented. Not only supporting joystick sprint (push joystick to furthest) |                 |
| Exit Key Consistency     | Exit key (i.e., ESC on keyboard) could exit menus that shows up more than once, pause game. i.e., not a second exit key, or a menu with close/cancel button that isn't exit-able by pressing exit key             |                 |
| Robust key bindings      | (Self-test, but ideally watch a player performs) Default keybinding can beat the highest difficulty gameplay consistently                                                                                         |                 |

## Latency & Responsiveness

| L-&-R                           | Requirement                                                                                                                                                                                          | Present (Y/N/-) |
|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| Input Buffer                    | The game has action-chaining / combo mechanic, and provided a reasonable buffer (pre-input) context to cache an pending action, or overrides the current blocking action                             |                 |
| Priority of action (overriding) | The game has action-chaining / combo mechanic, and has action prioritization capability, i.e., dodge/heal can override attack action, with or without transition animations present                  |                 |
| Key-blocking Indication         | Input blocking only occurs when visually obvious (e.g., reload animation) or with clear, immediate, and specific audio/visual feedback indicating why and which input is blocked                     |                 |
| Delay Indication                | Minimal delay between input and action. Any intentional delay (e.g., charge attack, charge jump) must be visually obvious and predictable                                                            |                 |
| Toggle/Hold Indication          | State changing key actions (sprint, ADS, crouch, scope, etc.) can be set to Toggle or Hold individually                                                                                              |                 |
| Interaction Animation Sync      | Avoid finishing the interaction later than animation finishes (preferably 300~500ms before), i.e., player sees animation finishes and sprints to next target——accidentally cancelled the interaction |                 |

## Low Priority Requirements

| Universal Control Support       | Requirement                                                                                                                                                                                                         | Present (Y/N/-) |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------- |
| No Menu Key-blocking            | No key-blocking anywhere in the menu, including menu animations and startup logos                                                                                                                                   |                 |
| Movement Context Prioritization | The primary game mechanic should have the highest movement-state priority. For example, in a game centered around parkour, combat-state transitions should not unnecessarily override or interrupt player movement. |                 |
| Movement Context Disambiguation | Avoid over-generalizing the movement system. Its complexity should correspond to the complexity of the intended environment and traversal mechanics.                                                                |                 |

### Counterexample: Movement Context Prioritization Failure

1. The player uses a stealth mechanic to move across an NPC-guarded field, waiting for each enemy NPC to reposition and carefully looking for opportunities to sneak through.
2. One enemy NPC notices the player. The player wants to roll/dodge toward a hiding spot and wait for the enemy to lose interest.
3. Instead, the player character immediately enters combat mode, draws their weapons, stands up, and turns to face the enemy NPC, effectively becoming locked into combat behavior.
4. Due to the forced combat-oriented turn, the player's roll/dodge is redirected and accidentally carries them into a second enemy NPC.
5. The second NPC immediately notices the player and attacks.
6. All nearby enemy NPCs are alerted and begin attacking the player.
7. The player throws the controller away and calls it a day.

### Counterexample: Movement Context Disambiguation Failure

1. A parkour game implements crossbar-traversal movement. These bars connect roofs to roofs and cliffs to cliffs, and some require a long jump to reach the next bar.
2. Because these crossbars are positioned high above the ground and often require long jumps, the traversal system prioritizes actions such as climbing down and jumping toward distant bars.
3. During normal gameplay, a player climbs onto a short barn fence and now simply wants to get back down.
4. The movement system recognizes the fence as the same type of traversal object as the high-altitude crossbars.
5. Instead of simply stepping or jumping down, the character enters the more complex traversal behavior, such as hesitating, attempting to climb down, preparing for a long jump, or jump to the bar nearby
6. The player is forced to fight against the traversal system to perform what should be a trivial movement action.
