# Motion Model-2

---

## Motion Model-1
Explanation:

Let's consider again what the summation above is doing - calculating the probability that the vehicle is now at a given location, $x_t$	.

How is the summation doing that?
It's looking at each prior location where the vehicle could have been, $x_{t-1}$. Then the summation iterates over every possible prior location, $x_{t-1}^{(1)}$…$x_{t-1}^{(n)}$. **For each possible prior location in that list, $x_{t-1}^{(i)}$, the summation yields the total probability that the vehicle really did start at that prior location and that it wound up at $x_t$.**

That now raises the question, how do we calculate the individual probability that the vehicle really did start at that prior location and that it wound up at $x_t$, for each possible starting position $x_{t-1}$ ?

That's where each individual element of the summation contributes. **The likelihood of starting at $x_{t-1}$ and arriving at $x_{t}$ is simply $p(x_t|x_{t-1}) * p(x_{t-1})$.**

We can say the same thing, using different notation and incorporating all of our knowledge about the world, by writing: $p(x_t|x_{t-1}^{(i)}, u_t, m) * bel(x_{t-1}^{(i)})$

From the equation above we can see that our final position probability is the sum of n discretized motion model calculations, where each calculation is the product of the 'i'th transition probability, $p(x_t|x_{t-1}^{(i)}, u_t, m)$ and 'i'th belief state, $bel(x_{t-1}^{(i)})$.

**'i'th Motion Model Probabiity:**
$p(x_t|x_{t-1}^{(i)}, u_t, m) * bel(x_{t-1}^{(i)})$

## Note
- Transition probability, $P(transition)$ can be calculated by normalised pdf function.
- Table of discretized calculation for each ith position probability value. To determine the final probability returned by the motion model, we must sum the probabilities.
- Example:
<table>
  <tr>
    <th>pseudo_position(x)</th>
    <th>pre-pseudo_position</th>
    <th>delta position</th>
    <th>P(transition)</th>
    <th>bel(x_{t-1})</th>
    <th>P(position)</th>
  </tr>
  <tr>
    <td>7</td>
    <td>1</td>
    <td>6</td>
    <td>1.49E-06</td>
    <td>5.56E-02</td>
    <td>8.27E-08 </td>
  </tr>
  <tr>
    <td>7</td>
    <td>2</td>
    <td>5</td>
    <td>1.34E-04</td>
    <td>5.56E-02</td>
    <td>7.44E-06</td>
  </tr>
</table>

Reference Equations:
- Discretized Motion Model:
$\sum\limits_{i} p(x_t|x_{t-1}^{(i)}, u_t, m)bel(x_{t-1}^{(i)})$
- Transition Model:
$p(x_t|x_{t-1}^{(i)}, u_t, m)$
- 'i'th Motion Model Probability:
$p(x_t|x_{t-1}^{(i)} u_t, m) *bel(x_{t-1}^{(i)})$
