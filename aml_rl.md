## [E.1] AML - Reinforcement Learning assignment typos

<i>I would like to start a new blog series - education [E], as I am still in the process of re-qualification from "pure science" to "data science".</i>

A few months ago I have finished the fourth course on Coursera in a row from [Advanced Machine Learning specialization](https://www.coursera.org/specializations/aml) - [Practical Reinforcement Learning](https://www.coursera.org/learn/practical-rl/home/welcome).

I will copy my review of the course (mark 5/5):
<i>"This is my fourth AML course, and for now I would say it is the best one. It connects lectures and practice in the best way. On the other hand, there are mistakes all around, as it is beta-version. In my opinion, it is not fair to put the beta-version course into paid specialization."</i>

Yes, you read it right - it is **the beta-version**. Hence, a few practical tasks (or assignments), had some mistakes where they should not be, i.e. in the part of the code that should not be changed by the student. I will list all of them here and try to make somebodies life easier :)

### Week 1 / Assignment 1 - "OpenAI Gym":

There is a wrong hint:
*Hint: your action at each step should depend either on **t** or on **s**.*
One should only use **t**!!!

### Week 6 / Assignment 8 - "Bandirs & exploration":

#### Change 1 - class BernoulliBandit:

> class BernoulliBandit:
>> def pull(self, action):

line
>>> if np.random.random() > self._probs[action]:

changed to:
>>> if np.any(np.random.random() > self._probs[action]):

i.e. the condition is put under **np.any()**.

#### Change 2 - def plot_regret:

>def plot_regret(scores):

line
>> plt.legend([agent.name for agent in scores])

changed to
>> plt.legend([agent for agent in scores])

i.e. **agent.name** is changed to solely **agent**.

#### Change 3 - submission:

Instead of **submit_bandits**, make new function **submit_bandits2** in submit.py:

    def submit_bandits2(agents, scores, email, token):
        epsilon_greedy_agent = None
        ucb_agent = None
        thompson_sampling_agent = None
        for agent in agents:
            if "EpsilonGreedyAgent" in agent.name:
                epsilon_greedy_agent = agent.name
            if "UCBAgent" in agent.name:
                ucb_agent = agent.name
            if "ThompsonSamplingAgent" in agent.name:
                thompson_sampling_agent = agent.name
        assert epsilon_greedy_agent is not None
        assert ucb_agent is not None
        assert thompson_sampling_agent is not None
        grader = grading.Grader("VL9tBt7zEeewFg5wtLgZkA")
        grader.set_answer("YQLYE", (int(scores[epsilon_greedy_agent][int(1e4) - 1]) - int(scores[epsilon_greedy_agent[int(5e3) - 1])))
        grader.set_answer("FCHOZ", (int(scores[epsilon_greedy_agent][int(1e4) - 1]) - int(scores[ucb_agent][int(1e4) - 1])))
        grader.set_answer("0JWHl", (int(scores[epsilon_greedy_agent][int(5e3) - 1]) - int(scores[ucb_agent][int(5e3) - 1])))
        grader.set_answer("4rH5M", (int(scores[epsilon_greedy_agent][int(1e4) - 1]) - int(scores[thompson_sampling_agent][int(1e4) - 1])))
        grader.set_answer("TvOqm", (int(scores[epsilon_greedy_agent][int(5e3) - 1]) - int(scores[thompson_sampling_agent][int(5e3) - 1])))
        grader.submit(email, token)

### Week 6 / Assignment 9 - "MCTS":

> class WithSnapshots(Wrapper):
>> def load_snapshot(self,snapshot):

line
>>> self.render(close=True) # close popup windows since we can't load into them

changed to
>>> self.close()

___

**I hope somebody will find this helpful and please let me know if you think that something else should be here.**

*The original post is on [SteemIT](https://steemit.com/technology/@wlakinsson/ml-1-aml-reinforcement-learning-assignment-typos), but I abondened that platform few weeks ago.*
