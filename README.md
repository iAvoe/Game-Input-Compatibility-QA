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

| Universal Control Support                  | Requirement                                                                                                                                                                                                             | Present (Y/N/-) |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |-----------------|
| Key-blocking Mechanic                      | Input blocking only occurs when visually obvious (e.g., reload animation) or with clear, immediate, and specific audio/visual feedback indicating why and which input is blocked                                        |                 |
| Input-delay Mechanic                       | Minimal delay between input and action. Any intentional delay (e.g., charge attack, charge jump) must be visually obvious and predictable                                                                               |                 |
| Toggle/Hold Controls                       | State changing key actions (sprint, ADS, crouch, scope, etc.) can be set to Toggle or Hold individually                                                                                                                 |                 |
| Action Synchronization                     | All player-controlled action that takes time finishes honestly in the same time, or before the action animation completes                                                                                               |                 |
| Input Buffer / Priority-of-action Mechanic | The game has enemies that prevents player to complete an action (i.e., reloading, re-healing), implements a reasonable buffer (pre-input) context to cache an pending action, or overrides the current blocking action  |                 |
| No Menu Key-blocking                       | No key-blocking anywhere in the menu, including menu-animations and startup logos                                                                                                                                       |                 |
| Movement context prioritization            | The main game mechanic should have the highest movement state priority. i.e., A game features parkour should consider combat mode a distraction to avoid                                                                |                 |

**Counter example on movement context ambiguity**
1. The player is using stealth mechanic to move across an NPC-guarded field
2. One emeny NPC noticed player character, the player wants to roll/dodge to a hiding spot to wait for enemy forgets him/her
3. The player character instead enters combat mode, pulled weapons out, stands up, turned around facing enemy NPC (combat lock-in)
4. Due to the previous direction change, the player rolled/dodged into the second enemy NPC
5. The second NPC immediately noticed the player, and stabbed the player character
6. All enemy NPC now knows the player is right there and attacks
7. The player reloads saved file or call it a day
