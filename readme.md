
# Red Light / Green Light in KrunkScript

```cs
# ======================================================
# HOST KNOBS

# Stage 1: Red/Green light
num MS_MINREDLIGHT = 2000;     num MS_MAXREDLIGHT = 2000;
num MS_MINGREENLIGHT = 2000;   num MS_MAXGREENLIGHT = 3000;
num MS_CLOCKTIMER_LIGHT = 60000; 
num MS_INTERVAL_CLOCKSYNC = 5000;

num VEL_NOTMOVING = 0.01; # how fast can a player move before we start shooting it (pixels/ms)
num MS_FIRERATE = 1000; # how fast to shoot
num MS_RELAXEDSHOOT = 500; # some buffer for red light to show before shooting
num GUNDAMAGE = 200; # how much damage per shot

# Stage 2: honeycomb
obj[] honeycombstart = obj[ # randomly teleports to one of the positions below
    {x: -1034, y: 73, z: 742}, # position 1
    {x: -831.5, y: 73, z: 948.5}, # position 2
    {x: -622, y: 73, z: 742} # position 3
];
obj honeycombWinArea = {x:-830,y:101,z:753};

num MS_CLOCKTIMER_HONEYCOMB = 60000;

# Stage 3: Marbles
obj[] marblestart = obj[ # randomly teleports to one of the positions below
    {x: -1796, y: 1011, z: 2280} # position 1
];
num MS_CLOCKTIMER_MARBLES = 60000;
# num MS_INTERVALMARBLEDROP = 3000;
num MS_INTERVALMARBLEDROP = 1000;
num NUM_DROPS = 8;
num CHANCE_DROP = 0.2;
num CHANCEBOOST_MAX = 0.8;
num MAXLOBBYSIZE = 40;
num MAX_ITEMS_INGAME = 40;

num CHANCE_STARTDROP = 1;

# Stage 4: Bridge 
obj[] bridgestart = obj[ # randomly teleports to one of the positions below
    {x: -488.86, y: 244, z: 2343} # position 1
];
num MS_CLOCKTIMER_BRIDGE = 60000;

# Stage 5: squid game
obj[] squidstart = obj[ # randomly teleports to one of the positions below
    
    {x: -443, y: 115, z: 96},
    {x: -594, y: 115, z: 96},
    {x: -594, y: 115, z: -30},
    {x: -443, y: 115, z: -30},
    {x: -717, y: 115, z: 28}
];
num MS_CLOCKTIMER_SQUID = 60000;

# Stage END: Win area
obj[] win_area = obj[ # randomly teleports to one of the positions below
    {x: -568, y: 86, z: -94} # position 1
];
# ======================================================
# CLIENT KNOBS
num MS_DURATION_SONG = 3000; # change if the soundfile length is changed
num MS_DURATION_BOTSCAN = 1000; # change if the soundfile length is changed
num MSDURATION_RAGDOLL = 1000; num MS_DURATIONDEATH = 3000;
num MS_DURATION_WINROUNDMSG = 3000;
num MS_DURATION_ROUNDSTARTMSG = 5000;
# ======================================================
```

# Road Map
1. Red/Green light (additional features)
	- 🤖 robot head will PAUSE AND POINT LASER 😱 if it detects movement, & wait to DETECT MORE MOVEMENT 😣 before shooting
	- bullets will 🗡️PIERCE players and damage others behind them (requires raycasting (WIP) from KS, or my already made custom collision code 😏)
	- players can 😈 HIDE behind other players and continue moving (also requires raycasting (WIP) from KS, or my already made custom collision code 😏)
2. Honeycomb stage
	- parkour stage (randomly dropped into cirle, triangle, umbrella...)
	- timer for death
3. tug-of-war stage
	- clicker / left right key tapper in teams 
4. marbles
	- collect 20 marbles (spawn randomly)
5.  glass stepping stones
	- triggers for stepping (randomized left/right)
	- turn off/flicker environment lighting halfway through
6. Final Round - squid game
	- melee last man standing

## V2.0.2 - Bugs / optimizations
- some fix for red/greenlight script - will not change status until network message is sent properly
- debug tool added to client (only works for map owners
- applause only at end of game fixed (swapped sounds)

## V2.0.1 - Fixes
- you can still pick up marbles when carrying > 20
- win applause sound only for last stage
- fix drop broadcast overflow (not reset everyround)

## V2.0 - First Map Release
- Marbles Game
- squid game (teleport to squid zone)
- Winning messages
- fog setting for last game 
- many more sounds, background music
- images for win/red/greenlight
- updated death system to accomodate spectators


## V1.2 
- doll now plays sound when turning head
- honeycomb random 3 spawn locations
- endgame trigger -> displays winner text & plays sound to everyone

## V1.1.1
- soldier shoot animation
- timer countdown
	- teleport to honeycomb after round end
- death animation

## V1.1  
- 🔫 Gun will take time shooting the NEAREST marked players (start shooting the nearest player, after nearest marked player dies, start shooting next nearest player)
	- ⏱️❎ green light phase will only start when all marked players are dead
- 🎥 Animations done for 🎎 doll
- 🔊 Sounds for 🎵 Song and 💥Gunshot for death
- ▶️ Trigger added for 🏃🏠leaving gameroom
- 🔴 🟢 Simple Overlay indicating light is red/green 




## V1.0 - redlight/greenlight functionality. 

https://streamable.com/dlyfa5

![video](2021-10-13_23-03-07.gif)

If a player moves during redlight phase, they will get fired at until they are dead or the mark is removed.
- Determine firing range by using onenter trigger w/ customParam "inrange", "outrange"
- redlight starts by sending customParam message "redlight"
- redlight ends (greenlight starts) by sending customParam message "greenlight"
- to fine-tune, change values of KNOBS in the host.krnk file.

### Tips:
1. player always spawns out of range of firing
2. customParam messages are caps sensitive ("redlight" works, "ReDlIgHt" does not work)
