
# 7370assignment2
#### 1. Establish a baseline performance. How well did your Deep Q-learning do on your problem? (5 Points) 
For example

total_episodes = 5000
total_test_episodes = 100
max_steps = 99
learning_rate = 0.7
gamma = 0.8
epsilon = 1.0
max_epsilon = 1.0
min_epsilon = 0.01
decay_rate = 0.01 With this baseline performance, our RL program with the Taxi-v2 Toy text gives us a score of 8.13 which is considerably not bad.

#### 2. What are the states, the actions, and the size of the Q-table? (5 Points)

  actions :['NOOP', 'FIRE', 'RIGHT', 'LEFT', 'RIGHTFIRE', 'LEFTFIRE']
  states : the image of screen, which is an array of shape (210, 160, 3) 
  size of q table: 210*160*3*6

#### 3. What are the rewards? Why did you choose them? (5 Points)

 the change in the game score is the rewards, 
 score is a delayed response from the envirenment when the player choose an actions.
 

#### 4. How did you choose alpha and gamma in the Bellman equation? Try at least one additional value for alpha and gamma. How did it change the baseline performance?  (5 Points)
 if gamma<1, then Gt(return G at time stamp t) will have a finite value. If gamma=0, the Agent is only interested in the immediate reward and discards the long-term return. Conversely, if gamma=1, the Agent will consider all future rewards equal to the immediate reward.
The learning rate alpha determines the behavior of the algorithm Sarsa. Too large values alpha will keep our algorithm far from convergence to optimal policy. If alpha=1 then Q(s_t, a_t) ← Gt, i.e. Q-value always will be most recent return, no any learning. The too small values alpha lead to learning too slow. If alpha=0 then Q(s_t, a_t) ← Q(s_t, a_t), never updated
whenI choose the alpha =0.6 gamma = 0.9, the performance change a little bit than baseline. the loss is huge value than the baseline's.

#### 5. Try a policy other than e-greedy. How did it change the baseline performance? (5 Points)
Boltzamann policy: mean reward declined 70% and mean steps increase 0.05%. Also from the training table in the data, The mean reward fluctuates greatly, reaching a maximum of 0.18 and a minimum of 0.07.

#### 6. How did you choose your decay rate and starting epsilon? Try at least one additional value for epsilon and the decay rate. How did it change the baseline performance? What is the value of epsilon when if you reach the max steps per episode? (5 Points)
 when I decrease the starting epsilon to 0.7 and increase the decay rate to 0.02, the performance of q-learning  increase 5%.   the value of epsilon is the minimum epsilon 0.01 when i reach the max steps

#### 7. What is the average number of steps taken per episode? (5 Points)
for the base line training process, the average steps are 99
for the baseline test, the average number of steps are 718.41 per episode. 
 
#### 8. Does Q-learning use value-based or policy-based iteration? (5 Points) Explain, not a yes or no question. 
Q-learning use value-based iteration; policy is deterministically computed from the q function by maximizing the reward;


#### 9. Could you use SARSA for this problem? (5 Points) Explain, not a yes or no question. 
yes, SARSA and q learning have similar principles. for this problem the envirenment is discrete and  the actions, state are finite. so establishing a q table is possible. 
 

#### 10. What is meant by the expected lifetime value in the Bellman equation?(5 Points) Explain, not a yes or no question. 
The decision a is made at moment t and the reward r is obtained, at which point the total value expectation v(t) consists of the expectation r at this moment and the total expectation v(t+1) at the next step. expected lifetime value meant the total expectation at next step, which is the part of the later v(t+1)
 bellman equation 

#### 11. When would SARSA likely do better than Q-learning? (5 Points)
Explain, not a yes or no question. 
Sarsa is not as effective as Q-learning in learning, but it converges quickly and is intuitive and simple. so when the test episodes are small, SARSA have better performance than q-learning.
 

#### 12. How does SARSA differ from Q-learning? (5 Points)  Details including pseudocode and math.
For q-learning, when the q function updated,we choose the optimal q value without ε-greedy, and so far we haven't known which the next action is actually chose to interact with envirenment until model choose next action using policy.
Meanwhile when the algorithm update the q value, the expected lifetime value is deterministic,which is the <img src="http://chart.googleapis.com/chart?cht=tx&chl= max_{\alpha}Q_k(s_2,a_2)" style="border:none;"> but for the SARSA, the value is  <img src="http://chart.googleapis.com/chart?cht=tx&chl= {\alpha}Q_k(s_2,A_2)" style="border:none;"> (A2 is choosen by policy)
 
 for the pseudocode part ,SARSA choose the A2 before the q value being updated. 
#### 13. Explain the Q-learning algorithm. (5 Points)  Details including pseudocode and math. 
Consider a computational agent moving around some discrete, finite world, choosing one from a finite collection of actions at every time step. initialize state1, choose A1 using policy derived from q,then observe S2,R2, update q value: 

<img src="http://chart.googleapis.com/chart?cht=tx&chl=Q_{k+1}(S_1,A_1)=Q_k(S_1,A_1)" style="border:none;">+<img src="http://chart.googleapis.com/chart?cht=tx&chl={\alpha}[R_{2}" style="border:none;">+<img src="http://chart.googleapis.com/chart?cht=tx&chl={\gamma}max_{\alpha}Q_k(S_2,a_2)-Q_k(S_1,A_1)]" style="border:none;">

        pseudocode:
        algorithms parameters: step size alpha belong to (0,1] small epsilon >0;
         Initial Q(s,a), for all s belong to collection S, a belong to collection A, arbitrarily except that Q(terminal, .) =0
         Loop for each episode 
            Initialize S
            loop for each step of episode:
                choose A from S using policy derived from Q
                Take action A, observe R,S'
                Q(S,A) <-Q(S,A) + alpha [R+ gamma max_alpha Q(S',a)-Q(S,A)]
                S <- S'
            until S is terminal

#### 14. Explain the SARSA algorithm. (5 Points)  Details including pseudocode and math. 
initialize state1, choose A1 using policy derived from q,then observe S2,R2,an then choose A2 using policy derived from  Q, update q value: 

<img src="http://chart.googleapis.com/chart?cht=tx&chl=Q_{k+1}(S_1,A_1)=Q_k(S_1,A_1)" style="border:none;">+<img src="http://chart.googleapis.com/chart?cht=tx&chl={\alpha}[R_{2}" style="border:none;">+<img src="http://chart.googleapis.com/chart?cht=tx&chl={\gamma}{\alpha}Q_k(S_2,A_2)-Q_k(S_1,A_1)]" style="border:none;">


        pseudocode:
        algorithms parameters: step size alpha belong to (0,1] small epsilon >0;
         Initial Q(s,a), for all s belong to collection S, a belong to collection A, arbitrarily except that Q(terminal, .) =0
         Loop for each episode 
           Initialize S
            choose A from S using policy derived from Q
            loop for each step of episode:
               Take action A, observe R,S'
               choose A' from S' using policy derived from Q
               Q(S,A) <-Q(S,A) + alpha [R+ gamma Q(S',A')-Q(S,A)]
                S <- S'
            until S is terminal
 

#### 15. What code is yours and what have you adapted? (5 Points)You must explain what code you wrote and what you have done that is different. Failure to cite ANY code will result in a zero for this section.
boltzman q learning 
adapted the parameter of q learning
 

#### 16. Did I explain my code clearly? (10 Points)Your code review score will be scaled to a range of 0 to 10 and be used for this score.

 yes

#### 17. Did I explain my licensing clearly? (5 Points)Failure to cite a clear license will result in a zero for this section.
yse
 

#### 18. Professionalism (10 Points)Variable naming, style guide, conduct, behavior, and attitude.
