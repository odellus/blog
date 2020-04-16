---
layout: post
title: Welcome to Planet Motherfucker
---

I'm not sure why I think it's a good idea to have a public facing journal honestly. I guess I can't get quite the same lick from putting up an article on medium as _hosting the code to my blog on Github pages_ yeah that's right. I was hip and new in 2012. Now it's just common best practice.

### *Deep Reinforcment Learning*

Anyway I've been taking the Udacity Nanodegree on Deep Reinforcement Learning and two out of three of the projects have kicked my butt. This last one especially. Train an agent to play tennis. Fuck I wish I knew what to tell you. I'm just not having any luck applying DDPG or TD3PG to this problem.

Thinking I should back up and try A2C or PPO. Have to fiddle to get the noise parameters just right? Why are we not learning $$\mu$$ and $$\sigma$$ for the actions _from the data/environment_? Then I would have what I needed to compute a Kullbach-Liebler divergence score between steps to update the actors (maybe critics too?) in a continuous state space. Not sure how I could do that now. And it does feel like this is a catastrophic forgetting problem.

How does one keep from taking a step that goes towards erasing your previously learned knowledge? Put in a cutoff for a metric that measures how much your knowledge has changed. If it has changed too much, then reject that update. Don't make that step.

_**THAT**_ is going to stabilize the algorithm more than just only updating the weights every $$N$$ steps.

Here's the learning step. It's pretty self-contained as far as the intuition behind what everything means:

{% highlight python %}
def learn(self, experiences):
        """Update policy and value parameters given batch of experience tuples.
        Q_targets = r + gamma * cirtic_target(next_state, actor_state(next)state)
        where:
            actor_target(state) -> action
            critic_target(state, action) -> Q-value

        Params
        ======
            experiences (Tuple[torch.Tensor]): tuple of (s, a, r, s', done) tuples
            gamma (float): discount factor
        """
        states, actions, rewards, next_states, dones = experiences

        # Update critic
        # Get predicted next-state actions and Q-values from target models.
        self.actor_target.eval()
        self.critic_target.eval()

        actions_next = self.actor_target(next_states)
        Q_targets_next = self.critic_target(next_states, actions_next)
        # Compute Q targets for current states (y_i)
        Q_targets = rewards + (self.gamma * Q_targets_next * (1 - dones))

        # We didn't want actor_target or critc_target showing up in the graph.
        self.actor_target.train()
        self.critic_target.train()

        # Compute critic loss
        Q_expected = self.critic_local(states, actions)

        critic_loss = F.mse_loss(Q_expected, Q_targets)


        # Minimize the loss
        self.critic_optimizer.zero_grad() # Clear gradient
        critic_loss.backward()            # Backpropagation
        torch.nn.utils.clip_grad_norm_(self.critic_local.parameters(), 1)
        self.critic_optimizer.step()      # Update parameters

        # Update actor
        actions_pred = self.actor_local(states)
        actor_loss = -self.critic_local(states, actions_pred).mean()
        # Minimize the loss
        self.actor_optimizer.zero_grad() # Clear gradient
        actor_loss.backward()            # Backpropagation
        # torch.nn.utils.clip_grad_norm_(self.actor_local.parameters(), 1)
        self.actor_optimizer.step()      # Update parameters

        # Now we update the target networks
        self.soft_update(self.critic_local, self.critic_target, self.tau)
        self.soft_update(self.actor_local, self.actor_target, self.tau)

{% endhighlight %}

The critic network `self.critic_local` tries to learn to estimate $$Q$$ from the current $$(s,a)$$ pair based on the actual current discounted reward, the target critic's opinion on the next state, and the action picked by the target actor.

The actor network `self.actor_local` is just trying to minimize `self.critic_local(state, action_pred).mean()` at every update. Meaning it's a separate but coupled optimization problem compared to learning to estimate $$Q(s,a)$$. So you're jointly trying to guide $$Q(s,a) \rightarrow Q^*(s,a)$$ and $$\pi(s) \rightarrow \pi^*(s)$$ because while the critic network is trying to predict the return based on our current action and state, the actor is learning to pick actions to maximize returns based on the output of the critic.

Anyway it's great and all that I understand the fucking algorithm up one side and down the other now but I can't get it to work as advertised. I've asked a question on the forum and I'm waiting for a response. I don't really care if I never get the certification (I'm lying I want it) but I've already gotten my money's worth. Figuring out what I was doing wrong and learning to train that pendulum was awesome. So was finally nailing the reacher environment.

Without a model though it does sort of feel a bit too much like bitcoin mining for presentable policies tbh. We've really got to incorporate more predictive models into RL if we want to get a heck of lot better sample efficiency. Too poor sample efficiency, and it's a heck of task training a good policy through all the muck. Significant barriers exist between $$\pi(s)$$ and $$\pi^*(s)$$. I mean we really need to start looking more carefully at the _transition model_ $$p(s_{t+1}\|s_t, a_t)$$. Every bit we learn about the environment is going to aid us our goal to find $$\pi^*(s)$$.


So it's about time for some _math_.

### The Problem
$$S_t$$  -  state at time $$t$$  
$$A_t$$  -  action at time $$t$$  
$$R_t$$  -  reward at time $$t$$  
$$\gamma$$  - discount rate (where $$\gamma \in [0,1]$$)  
$$G_t$$   -  discounted return at time $$t$$ ($$\Sigma^\infty_{k=0} \gamma^k R_{t+k+1}$$)  
$$\mathbb{S}$$    - set of all nonterminal states  
$$\mathbb{S}^+$$   -  set of all states including terminal states  
$$\mathbb{A}$$  - set of all actions  
$$\mathbb{A}(s)$$ - set of all actions available in state $$s$$  
$$\mathbb{R}$$ - set of all rewards  
$$p(s', r\|s, a)$$ - probability of next state $$s'$$ and reward $$r$$, given current state $$s$$ and current action $$a$$  

### The Solution
$$\pi$$ - policy  
- _if deterministic_: $$\pi(s) \in \mathbb{A}, $$ $$ \forall s  \in S, $$ and  $$a \in \mathbb{A}(s)$$  
- _if stochastic_: $$\pi(a\|s) = \mathbb{P}(A_t = a \|S_t = s),$$  $$\forall s \in \mathbb{S},$$ and $$a \in \mathbb{A}(s)$$  

$$v_\pi$$ - state-value function for policy $$\pi$$ ($$v_\pi(s) \doteq \mathbb{E}_\pi[G_t\|S_t = s],$$ $$\forall s \in \mathbb{S}$$)  
$$q_\pi$$ - action-value function for policy $$\pi$$ ($$q_\pi(s,a) \doteq \mathbb{E}_\pi[G_t\|S_t=s,A_t=a],$$ $$\forall s \in \mathbb{S}$$ and $$a \in \mathbb{A}(s)$$)  
$$v_*$$ - optimal state-value function ($$v_*(s) \doteq max_\pi v_\pi(s),$$ $$\forall s \in \mathbb{S}$$)  
$$q_*$$ - optimal action-value function ($$q_*(s,a) \doteq max_\pi q_\pi(s,a),$$ $$\forall s \in \mathbb{S}$$ and $$a \in \mathbb{A}(s)$$)


aaaand I'll continue that in another post. It doesn't all have to be fun with math. What's important is that I _can_ mass communicate with math through MathJax. I guess that means I'm going to be writing github pages textbooks from now on in my spare time. :joy:
