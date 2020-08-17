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

## Our Algorithm
Our Algorithm consists of two parts
1) A fast & brute force algorithm/greedy algorithm
2) An optimization algorithm: [Simulated annealing](https://en.wikipedia.org/wiki/Simulated_annealing)
