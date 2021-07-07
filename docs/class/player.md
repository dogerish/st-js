# STPlayer extends [STAsync](async.md)
Class representing a player.

## Constructor
```js
constructor(/*String*/ name)
```
### Arguments
1. `/*String*/ name`
	* The name of the player, clan tag included if appropriate.

## Properties
### name
String<br/>
The name of the player.
### country
[STCountry](../struct/country.md)<br/>
The country the player is from.
### clan
?[STClan](clan.md)<br/>
The clan the player is in, if the player is in a clan.
### rank
Number<br/>
The player's rank.
### elo
Number<br/>
The player's elo. In the [SauerTracker code on GitHub](https://github.com/AngrySnout/SauerTracker), I found what I assume to be the [elo calculating function](https://github.com/AngrySnout/SauerTracker/blob/e20132fb6cacbf6d680f068d7e92d83382b3c32f/src/tracker/game.js#L104).
```js
export function calcEloChange(eloSelf, eloOther, fragsSelf, fragsOther) {
  if (fragsSelf < 1 || fragsOther < 1) return 0;
  return Math.round(
    10 *
      (Math.log(fragsSelf / fragsOther) + Math.log(eloOther / eloSelf)) *
      (eloSelf / config.tracker.baseElo)
  );
}
```
What I interpret from this:
1. Every player starts with a base elo (1200 by default), and this elo is then mutated after duels.
2. Only duels where both players have at least one frag impact elo.
3. The elo is changed depending on the ratio of frags and elo between the player and opponent, as well as the base elo.
4. Assuming the game passed the above checks and the `frags` property of `self` and `opp` is for this particular game, the new elo of `self` after dueling `opp` is increased or decreased by the rounded result of
```js
10 * (log(self.frags / opp.frags) + log(opp.elo / self.elo)) * (self.elo / baseElo)
```
### totalGames
?Number<br/>
The total number of games this player has played.
### duels
[STDuels](../struct/duels.md)<br/>
Information about the player's duelling history.
### stats
[STPlayerStats](../struct/playerstats.md)<br/>
The player's statistics.
### online
Boolean<br/>
True if the player is on a server.
### latestGames
Array<[STGame](game.md)><br/>
An array of the last ten games played.

## Methods
Up to [STAsync](async.md) specifications.