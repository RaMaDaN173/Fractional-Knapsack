# Fractional-Knapsack

## Greedy Algorithm
---

A greedy algorithm is a simple and intuitive approach to solving optimization problems, where the goal is to find the best solution among a set of possible solutions. The greedy algorithm makes locally optimal choices at each stage with the hope that these choices will lead to a globally optimal solution.

The key characteristic of a greedy algorithm is that, at each step, it makes the best possible choice based on the current information, without considering the consequences of that choice on future steps. In other words, a greedy algorithm is myopic and doesn't backtrack or reconsider its decisions.

Here's a general outline of how a greedy algorithm works:

1. **Initialization:** Start with an empty solution.

2. **Greedy Choice:** At each step, make the best possible choice considering the current information.

3. **Feasibility Check:** Check if the choice made at the current step is feasible and doesn't violate any constraints.

**Update Solution:** Update the current solution with the chosen element or action.

**Termination:** Repeat steps 2-4 until a complete solution is obtained or a specific condition is met.

The effectiveness of a greedy algorithm depends on the problem's nature. Greedy algorithms are particularly useful for optimization problems with the greedy-choice property, meaning that a globally optimal solution can be reached by consistently making locally optimal choices.

However, it's important to note that greedy algorithms don't guarantee finding the globally optimal solution for every problem. Sometimes, they may produce suboptimal solutions. Therefore, careful analysis is required to ensure the correctness and optimality of the greedy approach for a specific problem.

Examples of problems where greedy algorithms are often applied include:

`Fractional Knapsack` Problem: Given a set of items with weights and values, determine the maximum value that can be obtained by filling a knapsack of limited capacity.


It's important to approach problems with a greedy strategy thoughtfully and validate the correctness of the chosen greedy choices for the specific context.

## Fractional Knapsack
---
The Fractional Knapsack Problem is a classic optimization problem in which the goal is to determine the most valuable combination of items to include in a knapsack, given that each item has a weight and a value. Unlike the 0/1 Knapsack Problem, where items can only be selected or rejected as a whole, in the Fractional Knapsack Problem, fractions of items can be taken, allowing for a more flexible solution.

Here's a more detailed explanation of the Fractional Knapsack Problem:

1. Problem Statement:

   * Given a set of items, each with a weight (wᵢ) and a value (vᵢ).
   * Also given a knapsack with a maximum weight capacity (W).

2. Objective:

   * Find the most valuable combination of items to include in the knapsack without exceeding its weight capacity.

3. Greedy Approach:

   * The greedy approach for the Fractional Knapsack Problem is to sort the items based on their value-to-weight ratio (vᵢ / wᵢ) in descending order.
   * The idea is to prioritize items with a higher value-to-weight ratio, as they provide more value per unit of weight.

4. Algorithm:

   1. Sort the items based on their value-to-weight ratio in descending order.
   2. Initialize the total value of the knapsack (V) to 0.
   3. Initialize the remaining capacity of the knapsack (remaining_capacity) to the maximum capacity (W).
   4. Iterate through the sorted list of items.
      * For each item, if adding the entire item doesn't exceed the remaining capacity, add the entire item to the knapsack.
      * If adding the entire item exceeds the remaining capacity, add a fraction of the item to fill the remaining capacity, maximizing the value.
   5. Stop when the knapsack is full or there are no more items to consider.

5. Complexity:

   * Sorting the items takes O(n log n) time, where n is the number of items.
   * The main loop iterates through the sorted items once, taking O(n) time.
   * Overall, the time complexity of the Fractional Knapsack Algorithm is O(n log n).

The Fractional Knapsack Problem illustrates how a greedy algorithm can be effective when optimizing for a specific criterion, such as maximizing value-to-weight ratio in this case.

## Explan Code
---
This Java code implements the Fractional Knapsack algorithm to solve the classic knapsack problem. The problem is defined as follows: Given a set of items, each with a weight and a value, determine the maximum value that can be obtained by selecting a subset of the items such that the total weight does not exceed a given limit.

Here's a breakdown of the code:

`KnapsackPackage` Class:
   * Represents a knapsack package with weight, value, and cost (value/weight).
   * The constructor initializes the weight, value, and cost of the package.
   * Provides getter methods to retrieve the weight, value, and cost of the package.

`Fractional_Knapsack` Class:
   * `main` method: This is the entry point of the program where an example set of weights (`W`) and values (`V`) are provided, and the FractionalKnapsack method is called.

`FractionalKnapsack` method:

   * Takes arrays of weights, values, the maximum weight the knapsack can hold (`MaxWeight`), and the number of elements/items (`NumberOfElement`).
   * Creates an array of `KnapsackPackage` objects based on the provided weights and values.
   * Sorts the array of packages in non-increasing order of their cost (value/weight).
   * Iterates through the sorted packages and adds them to the knapsack until the knapsack is full.
   * Outputs the selected items (their weights and values) and the maximum value that can be obtained.

Example in `main` method:

   * An example set of weights (W) and values (V) is provided.
   * The `FractionalKnapsack` method is called with the given parameters.

**Output:**

   * The code outputs the selected items (their weights and values) and the maximum value that can be obtained from the knapsack.

Note: The Fractional Knapsack algorithm allows taking fractions of items into the knapsack, optimizing for the maximum value per unit weight.

## Code in Java
---

### Class KnapsackPackage

    public class KnapsackPackage {
    private double Weight;
    private double Value;
    private Double Cost;

    public KnapsackPackage(double weight, double value) {
        Weight = weight;
        Value = value;
        Cost =new Double (value / weight);
    }

    public double getWeight() {
        return Weight;
    }

    public double getValue() {
        return Value;
    }

    public Double getCost() {
        return Cost;
    }
    }

---
### Fractional_Knapsack class

    import java.util.Arrays;

    public class Fractional_Knapsack {
    public static void main(String[] args) {
        int[] W = {1, 3, 5, 4, 1, 3, 2};
        int[] V = {5, 10, 15, 7, 8, 9, 4};
        FractionalKnapsack(W, V, 15, 7);

    }

    public static void FractionalKnapsack(int[] ArrayOfWeights, int[] ArrayOfValues, int MaxWeight, int NumberOfElement) {
        KnapsackPackage[] Pack = new KnapsackPackage[NumberOfElement];
        for (int i = 0; i < NumberOfElement; i++) {
            Pack[i] = new KnapsackPackage(ArrayOfWeights[i], ArrayOfValues[i]);
        }
        Arrays.sort(Pack, (kPackA, kPackB) -> kPackB.getCost().compareTo(kPackA.getCost()));
        int Reminder = MaxWeight;
        double Result = 0;
        boolean Stop = false;
        int i = 0;
        while (!Stop) {
            if (Pack[i].getWeight() <= Reminder) {
                Reminder -= Pack[i].getWeight();
                Result += Pack[i].getValue();
                System.out.println("Pack " + i + " - Weight " + Pack[i].getWeight() + " - Value " + Pack[i].getValue());
                i++;
            } else if (Reminder > 0) {
                double res = ((Pack[i].getValue() * Reminder) / Pack[i].getWeight());
                Result += res;
                Reminder = 0;
                System.out.println("Pack " + i + " - Weight " + Pack[i].getWeight() + "- Value " + res);
                Stop = true;
            } else {
                Stop = true;
            }
        }
        System.out.println("Max Value:\t" + Result);
    }
    }

