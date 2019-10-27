# Bayes Filter Summary

---

- The Bayes Localization Filter Markov Localization is a general framework for recursive state estimation.
- That means this framework allows us to use the previous state (state at t-1) to estimate a new state (state at t) using only current observations and controls (observations and control at t), rather than the entire data history (data from 0:t).

![](Screenshots/14.png)

- The motion model describes the prediction step of the filter while the observation model is the update step.
