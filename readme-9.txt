Dice Game:

Hybrid Agent:

This is the least optimal agent. As I created a dictionary that stores the number of occurrences for each integer shown from rolling the dice. Which is done by looping through all the states and updating the count variable.

Furthermore, in order for this agent to hold a good score, I made a function that iterates through all the states. If that state index contained a value of 4,5,6 and the number of occurrences was greater than 1 then I appended that index value to a list called ‘reroll’. This is because the rules of the game states that, if two or more dice shows the same values then those values are flipped upside down. For example 5 becomes 2 . 

I also implemented an alternative list called ‘dont_reroll’ in a separate function, that will contain the indices of the dices that contain the values 1,2 and if they appeared more than once. As this will be flipped to a higher value, thus resulting to a greater score. On top of that, we return the dices if the score is greater than 12.

Manual Agent:

The ‘ManualAgent’ is a slight improvement from the previous agent, due to now having several ‘if conditions’ that takes into account different possibilities of getting a particular value. Thus, I used the idea from the ‘HybridAgent’ of the ‘reroll’ and ‘dont_reroll’ lists that contained the occurrences of the different dice values and implemented it in the ‘ManualAgentClass’. I added an ‘elif’ statement, that checks if the dice index contains the value less than 3 and only occurs once. Then we appended those index value to the ‘reroll’ list, as those dices are not valuable for scoring. So, the agent chooses to reroll them in hope of getting a better value.

In addition, I added an another ‘elif’ statement but now, we append the dice indices to the ‘don’t_reroll’ list if the values are greater than or equal to 3 and are not duplicated in the state list. This is because, these dices can give you a high score, meaning if we reroll, then there is a likelihood of getting a lower score as the final score will take into account the penalties for rerolling.

Moreover, I applied a function where it iterates through the ‘reroll’ list. Which removes those indices from a ‘dice’ list that initially contained the states of all dices. Hence, once we removed those indices, we are left with dices that don’t need to be rerolled, as those have singular values greater than 3. Finally, I ended the agent with an ‘if’ and ‘else’ statement just to assure that it will hold all dices if the result is greater than or equal to 12, otherwise we reroll.





One step value iteration:

I performed a one-step value iteration, where it contained just one main body called ‘perform_single_value_iteration’. This initializes a new list for the values of each state to 0 and a variable called ‘delta’ to 0, which will keep track of the change in values.

After, I initialized a variable ‘maximum_value’ to zero, this will be used to keep track of the highest expected return found for those current states. Which is done by looping through the indices of the ‘self.states’ list.

For each current state, a for loop is made to iterate through all the possible actions that the agent can take. Thus, for each action, it obtains the information about the potential outcomes of taking a particular action. 

It starts iterating through each state, then it iterates through each action. As for each action, it calculates the expected return for that state. Once completing this, it updates the policy with the optimal action and the new value list for that state, with the action that results to the maximum expected return. In order to compute the expected return, the code would need to know the possible next states, probability of transitioning to that state and the immediate reward from taking that action. 

If the next state is not none, then the game is not over so we calculate the expected return which is added with the reward from performing that action in a particular state. Meaning, for each possible ‘next_state’ the expected return is calculated by multiplying the probability of reaching that state with the discounted value of that state, and then taking the sum of all such products. However, if the next state is none , which means the game has ended. In this case, the expected return is the probability of reaching the end state multiplied by the reward obtained at the end state. 

If the calculated expected return of the current action is greater than the previously stored maximum value. Then the maximum value is updated to the expected return. Finally, if the expected return value is greater than the previous maximum expected return value. Then, it updates the policy as this is considered to be the most optimal. Also, the algorithm checks the difference between the old and new values of the state(delta). If delta is greater than the previous delta, the loop continues as there is still improvements need to be made.


Full value iteration:

This is the most optimal agent, as we adopt the ‘perform_single_value_iteration’ method, which loops over all the states and calculates the expected return for each action for each state. As mentioned, the expected return is the sum of the immediate reward and the discounted value of the next state, weighted by the probability of transitioning to the next. state. The maximum expected value for each state is stored as the value of that state, and the optimal action is stored in the policy. This method will return delta, which is the absolute difference between the old and new values of each state. Delta is used to determine when the algorithm should stop, as if delta falls below a certain threshold such as theta, then the algorithm has converged.

Furthermore, I added an extra function called ‘value_iteration’, which repeatedly calls the ‘perform_single_value_iteration’ method until delta is smaller than theta which is 0.001. This method updates the values of each state and the policy at each iteration.
