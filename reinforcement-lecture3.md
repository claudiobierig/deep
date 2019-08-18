# Reinforcement Lecture 3

## Markov Decision Processes (MDPs) and Dynamic Programming

- Formalizing the RL interface
- Assume the Environment is fully observable
- Markov: Future is independent of the history, i.e. $\mathbb{P}(R_{t+1}=r, S_{t+1}=s' | S_t=s) = \mathbb{P}(R_{t+1}=r, S_{t+1}=s' | S_1, \ldots, S_{t-1}, S_t=s)$
- Example: Robot MDP
- $G_t = \sum_{k=0}^\infty \gamma^k R_k$, where $\gamma$ is a discount factor
- $G_t$ finite if rewards are finite as well as $\gamma < 1$
- $v_{\pi}(s) = \mathbb{E}[G_t|S_t=s,\pi]$
- Can be reformulated recursively (22:11)
- Define state action value $q_\pi(s, a)$ where we also condition the Expectation value on choosing the action $a$
- $v_{\pi}(s)=\sum_a \pi(a|s)q_\pi(s,a)=\mathbb{E}[q_\pi(S_t,A_t)|S_t=s, \pi]$
- Bellman Equation in Matrix form. Can rewrite with Matrix, Vector Notation: $v=r+\gamma P^{\pi}v$
- Can be theoretical solved directly in $\mathcal{O}(|\mathcal{S}|^3)$
- $v^*(s) = max_\pi v_\pi(s)$ and $q^*(s, a) = max_\pi q_\pi(s, a)$
- Theorem: For any MDP there exists an optimal policy $\pi^*$ such that $v^*(s) = v_{\pi^*}(s)$

41:30
