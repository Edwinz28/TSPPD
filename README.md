# 2020 U of T Traveling Courier Pickup Dropoff Competition

**Note: This repository is to highlight my team's achievements in this competition. Source code is not shared to keep the competition fair in future years**

## The Problem?
The problem at hand emulates real life package pick up and drop off. The "courier" has many (emphasis on many) deliveries that need to be completed. Each delivery consists of a package pickup and package drop off point. The algorithm finds the fastest order/route to complete all deliveries. Each route is computed using A* & real geographical data meaning each route is **NOT** a straight line path and abides to all traffic laws, accounts for turns and speed limits. For more on how we designed this, check out our GIS repository [here](https://github.com/Edwinz28/Open-Street-Maps-GIS)

## The challenge
The challenge is an extension of the classic [Traveling Salesman Problem](https://en.wikipedia.org/wiki/Travelling_salesman_problem) which in itself is a NP problem. 
If we were to ignore **ALL*** of the logistics and simply consider the fact that the courier needs to visit all the points on the map, a brute force algorithm would be O(n!). This means a brute force algorithm that can compute a route in nanoseconds would take years to finish.

## Competition Rules
1) The courier must pickup a package before successfully dropping it off (duh)
2) The truck has a set weight capacity
3) There may be multiple packages at a pickup. This rule also applies to drop offs
4) The truck must start at a company truck depot and end at a company truck depot
5) The algorithm only has 45 seconds to run

## Our Algorithm
Our Algorithm consists of two parts
1) A fast & brute force algorithm/greedy algorithm
2) An optimization algorithm: [Simulated annealing](https://en.wikipedia.org/wiki/Simulated_annealing)

### The Greedy Algorithm
Our greedy algorithm emulates real life decision making. At each step of planning the route, the courier factors in several conditions
1) Truck weight capacity
2) Which packages are currently inside the truck
3) Time between each destination
4) Based on which packages are currently in inventory & which have not been picked up what are the legal moves?
5) Remaining deliveries

To improve speed, we used multithreading as well as parallelization where applicable.  

### Simulated Annealing
This algorithm is based off of real life chemical annealing. In chemistry, when the temperature is hot particles move fast and when the temperature is cold, particles slow down.
Our algorithm uses a function of time to emulate the temperature as we are constraint by 45 seconds. When there is a lot of time on the clock, our algorithms will make rapid changes/mutations (fast particles). In this state, we accept all mutations to our solution, including ones that make the solution worse. As time runs low, we start to only accept better solutions.

We used an inverse exponential model to represent our probability. See how the time is the x axis and at x = t = 0, the probablity is virtually 1 to accept **ANY** solution <br/>
<img src="https://themathpage.com/aPreCalc/Pre_IMG/exp2.gif" width="435" height="241" />

#### Why We Use Probability To Accept Any Solution Inlcuding Bad Ones!
Let's look at the graph below. Let the x-axis represent the solution space and y axis represent the time. Our greedy solution will **RANDOMLY** insert us at a x position noted by the red dot. Traversing the graph is done by using mutation operators which will be explained in the next section.<br/>
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/SA%20Greedy%201.png?raw=true" width="435" height="241" /><br/>
If we were only to take **better** solutions, eventually we will reach a local minima not a global minima.
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/SA%20Greedy%202.png?raw=true" width="435" height="241" /><br/>
Thus if a probability of taking worse solution exist, it allows for an opportunity to overcome the hill and reach a global minima.
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/SA%20Greedy%203.png?raw=true" width="435" height="241" /><br/>

##### Mutation Operators: The "Intersection Swap"
In a nutshell, the intersection swap picks two random intersections and swaps positions.
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/Intersection%20Swap.png?raw=true" width="435" height="241" /><br/>
Not all swaps are legal (see list of conditions above), however since this only affects 2 nodes/intersections, many are indeed legal.

##### Mutation Operators: 2 Opt
Unlike the intersection swap, the 2 opt affects many more nodes/intersections. The 2 opt randomly chooses 2 nodes and swaps them and additionally reverses the order of nodes inbetween the selected intersections.
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/2opt.png?raw=true" width="435" height="270" /><br/>
This is a much larger mutation and results in significantly less legal combinations.

#### In A Nutshell: Visualization
Heres a gif I found online that best represents everything above. <br/>
<img src="https://upload.wikimedia.org/wikipedia/commons/1/10/Travelling_salesman_problem_solved_with_simulated_annealing.gif" width="435" height="270" /><br/>

### Results
The following graph illustrates the effeciency of our algorithm with testcases containing hundreds of nodes.
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/SA_Results.png?raw=true" width="435" height="270" /><br/>
Our algorithm was extremely iterative with hundred of millions of combinations with a reasonable ratio of legal mutations. For smaller test cases (where n is smaller) we reach billions of combinations.

Additionally, our team placed **12th** in the competition while remaining extremely competitive with everyone up until 3rd place.
<img src="https://github.com/Edwinz28/TSPPD/blob/master/Algorithm%20Graphics/results.PNG?raw=true" width="435" height="270" /><br/>





