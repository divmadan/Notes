# Markov Localisation-2

---

## Bayes' Filter for Localisation
With respect to localization, the terms are:
1. $P(location|observation)$: This is P(a|b), the normalized probability of a position given an observation (posterior).
2. $P(observation|location)$: This is P(b|a), the probability of an observation given a position (likelihood)
3. $P(location)$: This is P(a), the prior probability of a position
4. $P(observation)$: This is P(b), the total probability of an observation

- P(location) is determined by the motion model
- The probability returned by the motion model is the product of the transition model probability (the probability of moving from $x_{t-1}$ --> $x_t$ and the probability of the state $x_{t-1}$)

## Note
- The normalized P(location|observation) is the result of raw P(location|observation) dividing by P(observation).
- To determine the normalized posterior probability, first sum the raw P(Posterior) to get the total. Next, divide the P(Posterior) by the sum.


## Initialise belief state
- What value should our intial belief state take for each possible position
-
  - 1D map extending from 0 to 25 meters.
  - We have landmarks at x = 5.0, 10.0, and 20.0 meters, with position standard deviation of 1.0 meter.
  - If we know that our car's initial position is at one of these three landmarks, how should we define our initial belief state?
- Accounting for a position precision of +/- 1.0 meters, this places our car at an initial position in the range 4 - 6 , 9 - 11 , or 19 - 21.
- Then normalize by dividing by no of positions that are occupied (9 positions in our case) (= 1/9).
- All other positions, mark as 0

## How much data in $z_{1:t}$
1. lidar sends 100,000 data points with each refresh rate
2. each observation contains 5 pieces of data (points id, range, 2 angles and reflectivity)
3. each piece requires 4 bytes
4. drive for 6 hrs
5. lidar refreshes 10 times per sec

- per sec data from lidar = 100,000 * 10 = 1,000,000 = 1mil
- 6 hrs =6\*60\*60 = 21,600
- total data = 21,600 * 1mil = 21.6bil
- 5 pieces * 4 bytes = 20 bytes for each observation
- 20 * 21.6bil = 432bil bytes = 432 GB

**This is the amount of data if it took all historical data into account**
