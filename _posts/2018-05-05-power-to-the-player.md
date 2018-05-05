---
layout: single
title:  "Power to the Player"

tags:
  - Power Grid
  - Board Games
  - Software
---
[Power Grid](https://boardgamegeek.com/boardgame/2651/power-grid) is a board game about growing and powering a network of cities. In order to compete you must be able to balance network growth, generation capacity, and fuel supplies on a limited budget. Some of these costs are very predictable such as the price to put infrastructure in a city. Others are not such as the auction price of a power plant. With this project I'll be building tools to help a player find optimal choices when possible or at the very least make informed choices.

From a technical perspective I'll be trying out putting splitting separations between four concerns based on the [OODA Loop](https://en.wikipedia.org/wiki/OODA_loop). This loop was conceived developed by a military strategist to organize rapid responses to situations. In the context of this application Observe handles the user input, Orient maps the input to the game's domain, Decide is the analysis, and Act is the output. By separating the concerns each area can evolve with minimal changes to the other pieces of code. For example, upgrading the user input to a camera that processes the board with computer vision would have no affect on how the analysis is done and relayed to the user.

|         | Observe         | Orient                            | Decide                                     | Act                  |
|---------|-----------------|-----------------------------------|--------------------------------------------|----------------------|
| Present | Static file     | Direct mapping                    | Inform player about current situation      | Display in a console |
| Next    | GUI             | Infer from incomplete information | Make recommendations to player             | Notify in an app     |
| Future  | Computer vision | Handle conflicting information    | Make all decisions as an autonomous player | Robot makes moves    |

To start, I worked through several iterations that just displayed basic information about the board. This allowed me to slowly figure out how the models in each subdomains and the interactions between them. What I came up with is that the messages would be Observations, Game State, and Actions.

!(/images/PowerGrid_OODA_Messages.svg)

For example, a Game File Observer can make Observations such as what Map is being used and what Cities have already been taken. Then the Orienter compiles these Observations into a single Game State model. The Decider then takes this model and performs analysis. This analysis results in a list of Actions such as giving the user information or making recommendations. These Actions are then performed by the Actor.
