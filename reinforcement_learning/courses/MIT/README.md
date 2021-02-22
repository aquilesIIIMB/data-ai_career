We summarized some of the key points for each of the problem clinic discussions for the first session below. We will shortly be posting feedback on session two as well. Feel free to reach out to us with any questions. 

Team 1: Jesus and Sebastian

Active Learning for Supervised Machine Learning: Not only take the most confident decisions, but incorporate some notion of uncertainty.
Survey of Active Learning: https://minds.wisconsin.edu/bitstream/handle/1793/60660/TR1648.pdf?sequence=1&isAllowed=y
Active Learning for Anamoly Detection: http://web.engr.oregonstate.edu/~afern/papers/icdm16-das.pdf
Survey of Active Learning in Deep Learning: https://arxiv.org/abs/2009.00236
Series of Questions: This is similar to developing chatbots.
Reference for RL in chatbots: https://towardsdatascience.com/training-a-goal-oriented-chatbot-with-deep-reinforcement-learning-part-i-introduction-and-dce3af21d383
Something to keep in mind: There is some relevant recent research on how AI-human collaboration may inadvertently bias human decision makers, especially while the system is imperfect (e.g. during training): Vaccaro, Michelle, and Jim Waldo. "The effects of mixing machine learning and human judgment." Communications of the ACM 62, no. 11 (2019): 104-110.
Team 2: Rainer Dahms & Huib Vaessen

How to incorporate constraints:
Instead of putting constraints in the action space, put them in the reward function (e.g., no negative cash flow, diversity in portfolio etc.). This will allow for relatively simpler actions.
Discovering Attractivity Score in private investments
You mentioned a two stage process for private investments, wherein first there is price discovery and then there is the actual purchase. It worth considering use of supervised learning to predict the attractivty score.
Using past data:
Survey of Offline RL: https://arxiv.org/abs/2005.01643
Consider using off-policy RL.
Team 3: Anthony & Girithar.

The key is to first define a clear reward, and second to shape that reward. The latter is important because the reward signal in the security context is likely to be very sparse — that is, a long sequence of "correct" actions must be selected before there is an informative learning signal. The extent to which you can shape your reward to guide exploration towards the points of interest, the better. Suggestions for shaping the reward include: imitating human pentesters, imitation state-of-the-art pentesting software.
Another point to consider is whether you have access to a "simulator" for this problem — is it the real system? Are there any potential side effects of using the real system to deploy RL, e.g. increased traffic on the network? Is it possible to replicate the system or have a smaller version of the system that captures the same vulnerabilities? The underlying question is: what is the cost of obtaining data for training the RL agent?
 

Team 4: Mauricio Salazar.

Make the reward function reflect what you want, instead of encoding how you want the system to behave — this can help figure out strategies that may not be obvious as a human, but will satisfy the overall goals. I don’t think your problem is the case of multi-objective RL. It seems the overall goal is to maximize money under some constraints. Consider putting these constraints in the reward function, e.g. if the power grid trips etc.
It is not necessary to discretize the state space.
For modeling temporral dependencies:
Consider using RNNs / LSTMs to encode history.
Architecture from SNAIL: https://arxiv.org/abs/1707.03141 (it combines convolutions with self-attention)
For using past data:
Off policy RL: TD3 / SAC
Offline RL: https://arxiv.org/abs/2005.01643
Using Demonstrations + RL
 

Team 5: Aquiles & Jose Antonio

There are two different scenarios:
Scenario A: Different customers come to the website and we need to make a decision for each customer, what product to show. The customers either buy the item or leave the website. This fits formulation of contextual bandits.
Scenario B: A customer on the website can either purchase, pass or leave. In this case, the customer's internal state (e.g., his mood) can change depending on what items are being shown. This makes it a sequential decision making problem, which fits the general RL formulation.
State Space: It will be useful to incorporate history of all the suggestions made to the customer. One can use:
Consider using RNNs / LSTMs to encode history.
Architecture from SNAIL: https://arxiv.org/abs/1707.03141 (it combines convolutions with self-attention)
Reward Function: Should encourage the customer to stay as long as possible, but the reward of making a purchase should be significantly higher so that optimal strategy does not turns out to be a "pass" everytime.
If a RL algorithm is deployed live one concern is that in the exploration phase many bad recommendations could be made, which would turn away the customer. It might be important to cautiously explore product recommendations. Here is where offline RL comes in. Look at this survey article: https://arxiv.org/abs/2005.01643

Here is part 2, where we have summarized some key points on the second problem clinic discussions. Feel free to continue the discussion below or reach out to us with any questions.

We were impressed with the range of topics we managed to cover in 2 short sessions. We encourage you to learn from the feedback and summary from other groups' problems, in addition to your own.

Group 1: Adi and Arturo

One possibility is to formulate your problem such that you treat each property as its own independent (RL) problem instance. This is suitable if, as you've identified, the outcomes of experiments are expected to be pretty uniform across the different properties. Each property then can be viewed as an episode.
For using the ~5 years of historical data you have, you may consider employing off-policy techniques. Note that in order to perform A/B testing on historical data, these off-policy methods require the past decisions to be made according to a stochastic policy (rather than a deterministic one). This is often not the case for historical data, but you may take this into account for any future data that is collected — to enable offline A/B testing in the future. Here is a pointer to get started: Multiworld Testing Decision Service: A System for Experimentation, Learning, And Decision-Making (Microsoft) https://github.com/Microsoft/mwt-ds/wiki

Group 2: Raghav & Therence

The good news is that this problem setting is ripe for deep RL — it can be framed as a sequential problem, and doesn't have good alternative solution methods (aside from heuristics or solving simplified versions of the problem). The bad news is that we aren't quite there yet; this is an active area of research. This is a good area to watch in the next couple years.
Here is one of the recent papers that kicked off the current line of work on deep RL + combinatorial optimization. This particular work learns a greedy algorithm for problems including the minimum vertex cover, maximum cut, and traveling salesman problems. Dai, Hanjun, Elias B. Khalil, Yuyu Zhang, Bistra Dilkina, and Le Song. "Learning combinatorial optimization algorithms over graphs." arXiv preprint arXiv:1704.01665 (2017). https://arxiv.org/abs/1704.01665. There is a growing literature on learning to branch and bound, learning local search, and learning direct solutions.
Group 3: Riccardo and Ade

One consideration is how much investment is being made. If the amount of investment is very large, it can effect the market dynamics. However, if the amount of investment is significantly smaller than the total trading volume, one can assume that the "system" (or the dynamics) is unaffected by the trading actions.
For inspiration, this scenario is similar to recent Google Loon project, which uses RL to help navigate high altitude balloons for the purpose of providing internet access to remote regions: Bellemare, M.G., Candido, S., Castro, P.S. et al. Autonomous navigation of stratospheric balloons using reinforcement learning. Nature 588, 77–82 (2020). https://doi.org/10.1038/s41586-020-2939-8. In particular, some of the structural similarities to your problem include: 1) an environment which is difficult to model (wind, firm value), but for which the actions do not affect the state too much, and 2) data of the environment can be measured and collected (historical wind column data, firm value fluctuation over time). As a technical note: to be precise, the actions do strongly affect the state because, for instance, the location of the balloon is part of the state, and so actions which move the balloon will clearly affect the state. However, that part of the state change is easily modeled with physics; it is the wind part of the state that is difficult to model. Similarly, the literal amount of money a firm has is directly affected by investment, but the long-term value has numerous other contributing factors.
Consider using Deep Q-Learning. For modeling long-temporal dependencies, one can make use of:
Consider using RNNs / LSTMs to encode history.
Architecture from SNAIL: https://arxiv.org/abs/1707.03141 (it combines convolutions with self-attention)
Group 4: Danilo

The problem posed is a combination of knapsack, scheduling, and possibly additional combinatorial problems. The good news is that this is a perfect problem for RL. The bad news is that each one of these may be difficult enough alone for RL, let alone all three.
One key point to consider when formulating this problem in the RL framework is how many actions do you need to "get right" in a row in order to succeed in your task? Current RL algorithms struggle with long problem horizons (and, horizon = # actions) — due to issues of variance and exploration. If you have 10 actions and expect to need 100 actions to succeed, then in the worst case there are 10^100 action sequences to explore. (In class, we discussed a similar idea in the context of the state space. For combinatorial optimization problems, this reasoning roughly applies to the action space as well.) However, there is an opportunity to reframe your problem such that the problem horizon is shorter by making the individual actions "more powerful." That is, instead of an action being atomic, such as moving an item one at a time, you could design actions which retrieve an item. Retrieving an item could consist of a sequence of moves, which could be solved directly or with a heuristic. These could be considered as "subpolicies" that are directed by an overall policy. In the literature, these subpolicies would be referred to as temporally extended actions, as compared to the individual primitive actions. Now, you might still have 10 actions, but you may expect to only require 10 actions to succeed in your task (supposing that each of the subpolicies took 10 primitive actions), resulting in "only" needing to explore 10^10 action sequences. Much better!
Once you have something working with subpolicies, there are more sophisticated approaches that can be attempted. One promising example in particular is the options-critic architecture in hierarchical reinforcement learning, to automatically learn the subpolicies (called options): Bacon, Pierre-Luc, Jean Harb, and Doina Precup. "The option-critic architecture." In Proceedings of the AAAI Conference on Artificial Intelligence, vol. 31, no. 1. 2017. https://ojs.aaai.org/index.php/AAAI/article/view/10916. However, this might not be necessary if one can already construct sufficiently good subroutines.
A note on algorithms: It may be worth trying Q-learning first. If going with DQN, considering encoding the state space with a "pixel" representation (think about Atari game examples), which is compatible with convolutional neural network (CNN) architectures.
Group 5: Carmine Gioia

The literature on personalized health recommendation may be a good starting point for your project, due to similarities in the target individual’s changing internal and contextual state. Here are a few pointers:
This paper discusses some practical challenges of using RL for personalized recommendations, concerning imperfect data: Shortreed, Susan M., Eric Laber, Daniel J. Lizotte, T. Scott Stroup, Joelle Pineau, and Susan A. Murphy. "Informing sequential clinical decision-making through reinforcement learning: an empirical study." Machine learning 84, no. 1-2 (2011): 109-136. https://link.springer.com/content/pdf/10.1007/s10994-010-5229-0.pdf
Due the data limitations it can be helpful to construct a model from data for improved sample efficiency of RL. Here is an approach for building out the MDP dynamics (described here in the language of causal models): Klasnja, Predrag, Eric B. Hekler, Saul Shiffman, Audrey Boruvka, Daniel Almirall, Ambuj Tewari, and Susan A. Murphy. "Microrandomized trials: An experimental design for developing just-in-time adaptive interventions." Health Psychology 34, no. S (2015): 1220. https://psycnet.apa.org/doiLanding?doi=10.1037/hea0000305
This is fancier work, but may be of interest: Lei, Huitian, Ambuj Tewari, and Susan A. Murphy. "An actor-critic contextual bandit algorithm for personalized mobile health interventions." arXiv preprint arXiv:1706.09090 (2017). https://arxiv.org/abs/1706.09090
Group 6: Salvatore

Although the reinforcement learning framework cannot tell you what you (or your company) care about, by iterating on the reward function and inspecting the resulting policy, RL can help to inform you about when you have achieved a suitable reward function.
Concerning the use of RL vs supervised learning: a starting point to think about this is whether the learning objective (e.g. reward) can be directly evaluated / calculated (e.g. by a human expert), or is more abstract or has long-term dependencies that are hard to directly characterize. An example of the former could be fraud vs not fraud, for a given account. Its operational costs may also be calculated directly. An example of the latter could be the impact of flagging an account as fraudulent on the number of new customers next year.
To model long-term dependencies:
Consider using RNNs / LSTMs to encode state information.
Architecture from SNAIL: https://arxiv.org/abs/1707.03141 (it combines convolutions with self-attention)
- 
- 
