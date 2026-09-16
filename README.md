# Bingo Strategy Under Uncertainty — Monte Carlo Simulation

A stochastic simulation of repeated bingo games between four players who differ only in **how many cards they buy per game**. The goal is to explore how a buying strategy affects a player's money over time in a game with no real decision-making.

![Money evolution over 100 games](images/money_evolution.png)

## Game rules implemented

| Parameter | Value |
|---|---|
| Players | 4, starting with 100 units each |
| Cards bought per game | 1, 2, 3 and 4 (players 1–4) |
| Card | 4 × 9 grid of 36 distinct numbers from 1–99 |
| Card price | 5 units |
| Prizes | First line: 5 % of the pot · First full card: 95 % of the pot |
| Session | 100 consecutive games |

The pot is the total paid for all cards (50 units), so every unit paid is returned as prizes: the game has no house edge.

## How the simulation works

`Montercarlo_Bingo_Final.ipynb` is organised in four cells:

1. **Functions**
   - `Cartones(n)` generates *n* random cards.
   - `Busca(players, num)` marks a drawn number on every card by setting it to 0.
   - `Linea(...)` and `Bingo(...)` detect the first completed row or card.
2. **Setup.** Players are stored as dictionaries with their name, money and cards.
3. **Game loop.** For 100 games:
   - every player pays for new cards;
   - the 99 balls are shuffled and drawn one by one;
   - line and bingo are checked after each ball;
   - prizes are paid and each player's money is recorded.
4. **Plot.** The evolution of every player's money is drawn over the 100 games.

## Results

In the recorded run, the player with a single card finished with the most money and the player with four cards with the least. This is **one random trajectory** with no fixed seed, so a new run will give a different ranking.

A quick expected-value argument explains why: holding *k* of the 10 cards in play gives a winning chance of about *k*/10, which offsets the cost of the extra cards. The number of cards therefore mainly changes the **variability** of a player's results, rather than their expected outcome.

## Limitations

- **Tie-breaking.** When one ball completes several cards at once, the prize goes to the first player in the list instead of being shared. This happens often, especially for the bingo, and gives a systematic advantage to Player 1.
- **Single run.** Ranking strategies requires repeating the session many times and comparing average results with confidence intervals.
- **No fixed seed.** Results are not reproducible run to run.
- **No bankroll limit.** Money can go negative.
- **Simplified card.** The 4 × 9 card with 36 numbers is a simplification of real bingo cards.

## Run it

```bash
pip install -r requirements.txt
jupyter notebook Montercarlo_Bingo_Final.ipynb
```

Run the cells in order. Re-running the game cell without re-running the setup cell accumulates results from previous runs.

## Tech

Python · NumPy · Matplotlib · Jupyter
