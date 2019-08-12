# Reinforcement Lecture 2

## Recap Lecture 1

- General Setup:
  - Agent observes Environment
  - Agent influences Environment with actions
  - Additionally there is usually a reward signal
- In Reinforcement Learning the agent learns to make decisions
- Different ways:
  - policy
  - value function
  - model
- In general time and consequences are taken into account
- Decisions affect the reward, the agent state and the environment state

## Lecture 2 - Exploration and Exploitation

- Simplified Setup: Actions do not influence the state (no sequential structure)
- Multiarm bandit
- Goal: Optimize reward across complete lifetime including while we learn
- The true value of an action is the expected reward of an action
- Possible choices for an estimated value
  - averaging
  - incremental: $Q_t = Q_{t-1} + \alpha_t(R_t-Q_{t-1})$
    - $Q_t$ is estimate at timestep $t$, $R_t$ is reward at timestep $t$ (both depend on the chosen action)
    - $\alpha_t$ being $\frac{1}{N_{t-1}+1}$ is the same as averaging
    - $\alpha_t$ being constant tracks the last rewards
- Take into account that estimates are uncertain
- Definition: $v_*$ is the optimal value
- Definition: Regret is the difference between the optimal value and the reward for a chosen action
- Reformulated Goal: minimize regret across complete lifetime. Same as before.
- This is for analyzing algorithms. Try to minimize the asymptotic of the expected regret.
  - Rat example: Greedy algorithm -> expected regret grows linearly
- Can rewrite regret over lifetime: Instead of summing over timestep we can sum over possible actions
- \epsilon-greedy: Choose a random step with probability \epsilon (explore)
  - Example: Also grows linear, since probablity of choosing wrong action is fixed and greater than zero
- Theorem (Lai & Robbins): Expected regret grows at least logarithmically with a constant depending on the regrets of each action and the [KL-divergence](https://en.wikipedia.org/wiki/Kullback%E2%80%93Leibler_divergence)
- Definition Upper confidence bound ($U$): A value added to the estimated value of an action such that we are fairly certain that the real value is below it
- Greedily choose the value which has the highest estimated value plus upper confidence bound
- Theorem (Hoeffdings Inequality): $X_i$ iid in $[0,1]$: $\mathbb{P}(\mathbb{E}[X]\geq \overline{X}_n + u) \leq e^{-2nu^2}$
- From this. Choose $U=\sqrt{\frac{-\log(p)}{2N}}$, where $1-p$ is the probability "fairly certain"
- Choose p to decrease over time, i.e. $1/t$
- UCB algorithm
  - $a_t = argmax(Q(a)) + c\sqrt{\frac{\log(t)}{2N(a)}})$, where $c$ is a parameter
  - Theorem (Auer et al 2002): UCB with $c=\sqrt{2}$ achieves logarithmic regret
- Bayesian Bandits: $\mathbb{P}(R_t|\theta, a)$
- Example: Bernoulli reward: 0 or 1
- start with uniform distribution $[0, 1]$, same as $Beta(x_a=1, y_a=1)$
- Update $x_a++$, if reward is 0, $y_a++$ if reward is 1

1:11:11
