
# EX 5A 0/1 Knapsack Problem - Branch&Bound 
## DATE: 27/08/2026
## AIM:
To Write a Java program to solve 0/1 Knapsack problem using Branch and Bound Approach.
You are heading a college entrepreneurship cell that can invest in up to N student‑startups.

For each startup i you know: cost[i]  — the amount (in ₹ lakh) required to join the showcase profit[i] — the estimated profit (in ₹ lakh) you’ll gain if it succeeds You have a total budget of B ₹ lakh. Pick a subset of startups so that the sum of costs ≤ B and the sum of profits is maximised.

Because N can be as large as 50, a plain exhaustive search (2^N) is too slow.

The recommended approach is Branch & Bound with a fractional‑knapsack upper bound (but any algorithm that meets the constraints is accepted). 

Input Format

N

B

cost[1] cost[2] … cost[N]

profit[1] profit[2] … profit[N]

1 ≤ N ≤ 50

1 ≤ B ≤ 1 000 000

1 ≤ cost[i], profit[i] ≤ 10 000 

Output Format

maxProfit

## Algorithm

1. **Start**
2. Read the number of items `N`, budget `B`, costs, and profits.
3. Sort the items in descending order of their profit-to-cost ratio.
4. Initialize `best = 0` and perform DFS Branch and Bound starting with zero cost and profit.
5. Calculate a fractional upper bound by adding complete items and, if possible, a fraction of the next item within the remaining budget.
6. If the upper bound is not greater than `best`, prune the current branch.
7. Recursively explore both choices: include the current item if within budget, or exclude it.
8. Update `best` whenever a higher valid profit is found and display it after all branches are processed.
9. **End** 

## Program:
```
/*
Program to implement Reverse a String
Developed by: Vishwaraj G
Register Number: 212223220125
*/
import java.util.*;

public class StartupShowcaseOptimizer {

    // ---------- Global data ----------
    static int N, B;
    static int[] c, p;          // cost, profit after sorting by ratio
    static int best = 0;        // incumbent best profit

    // ---------- Fractional upper bound ----------
    static double bound(int idx, int cw, int cv) {
         //Type your code
         if(cw>=B) return cv;
         double val=cv;
         int rem=B-cw;
         while(idx<N && c[idx]<=rem)
         {
             rem-=c[idx];
             val+=p[idx];
             idx++;
         }
         if(idx<N)
         {
             val+=p[idx] *(rem/(double) c[idx]);
         }
         return val;
    }

    // ---------- DFS Branch & Bound ----------
    static void dfs(int idx, int cw, int cv) {
       //Type your code
       if(idx==N)
       {
           best=Math.max(best,cv);
           return;
       }
       if(bound(idx,cw,cv)<=best) return;
       if(cw+c[idx]<=B)
       {
           dfs(idx+1,cw+c[idx],cv+p[idx]);
       }
       dfs(idx+1,cw,cv);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        N = sc.nextInt();
        B = sc.nextInt();
        int[] cost = new int[N];
        int[] prof = new int[N];
        for (int i = 0; i < N; i++) cost[i] = sc.nextInt();
        for (int i = 0; i < N; i++) prof[i] = sc.nextInt();
        sc.close();

        // Sort by profit/cost ratio descending → tighter bounds
        Integer[] idx = new Integer[N];
        Arrays.setAll(idx, i -> i);
        Arrays.sort(idx, Comparator.comparingDouble(i -> -(double) prof[i] / cost[i]));

        c = new int[N];
        p = new int[N];
        for (int i = 0; i < N; i++) {
            c[i] = cost[idx[i]];
            p[i] = prof[idx[i]];
        }

        dfs(0, 0, 0);
        System.out.println(best);
    }
}
```

## Output:
<img width="292" height="133" alt="image" src="https://github.com/user-attachments/assets/0b74dfdd-f246-4d45-82a4-08e32b1bba30" />



## Result:
The program successfully solved 0/1 Knapsack problem using branch & bound and output is verified. 
