# Whiteboard
This is a virtual whiteboard for me to flesh out some ideas I've had that may or may not be work well and make good starting points for research. The idea is that eventually I will get around to putting them to the test or realizing that they won't actually work. If you've got a similar idea, think of some challenges I might run into or something that I'm overlooking, or want to work together, feel free to open an issue, submit a pull request, or get in touch.

## Categories

[Causal Discovery](#causal-discovery)

[Reinforcement Learning](#reinforcement-learning)

[Game Theory and Other Sequential Decision-making Formalizations](#game-theory-and-other-sequential-decision-making-formalizations)

## Causal Discovery

### Causal Discovery as a Bandit Problem
1. Problem: CI test/score function scales with datapoints
    1. Solution: sample random subsets of data and aggregate over samples
        1. LLN implies that average will converge to true value for whole dataset
2. Problem: too many DAGs to enumerate
    1. Solution: causal discovery as an (infinitely-armed) bandit problem
        1. Each DAG is an arm
        2. Use score function/CI tests on subsets of data as score for arm (DAG)
            1. If using CI tests, need to apply Meek's rules afterwards.
        3. One potential algorithm is GP with minimal regret acquisition function
            1. Could use NN version of GP or infinitely-armed bandit algorithm, various algorithms already exist
            2. Problem: need to convert DAGs to unique arms, ideally without constructing each DAG
                1. Solution: bijection between DAGs and integers
                    1. Adjacency matrix of DAG is lower triangular 1s and 0s
                    2. If entry is not 1, it is 0 so really only need to focus on one or the other
                    3. Concatenate element positon of 1s (row number, colum number) to get unique integer
                    5. Example:
                           
                                        |    *     | Column 1 | Column 2 |  Column 3 |
                                        |  :---:   |   :---:  |   :---:  |   :---:   |
                                  A =   |   Row 1  |     1    |     0    |     0     |
                                        |   Row 2  |     0    |     1    |     0     |
                                        |   Row 3  |     0    |     0    |     0     |
              
                                  f(A) = 1122
                     6. Can enumerate over these integers without explicitly constructing DAGs or adjacency matrices
3. With arm IDs and way to calculate (stochastic) rewards each time we pull an arm (DAG), we can use bandit algorithm to find the best arm!
  
### Causal Discovery via MCMC
1. Same approach as above to calculating scores or independence tests
2. Same approach for assigning unique numbers to DAGs
3. Use Metropolis-Hastings MCMC to sample over graphs
    1. Ideally want to make it converge faster
        1. Maybe use temperature schedule
        2. Could also use some kind of exploration bonus
            1. Want to encourage exploration early on but quicly converge to the best DAG(s)
                1. Maybe use active learning or similar approach to Ready Policy One paper

## Reinforcement Learning

## Game Theory and Other Sequential Decision-making Formalizations
