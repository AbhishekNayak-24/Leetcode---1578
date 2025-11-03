# Leetcode---1578
Minimum Time to Make Rope Colorful
//code in java 
class Solution {
    public int minCost(String colors, int[] neededTime) {
        int totalCost = 0;
        // maxNeededTime tracks the maximum removal time within the current consecutive group of same-colored balloons.
        int maxNeededTime = 0; 

        // Initialize with the first balloon's needed time if the string is not empty.
        // This handles the case of a single balloon or the start of the first group.
        if (colors.length() > 0) {
            maxNeededTime = neededTime[0];
        }

        // Iterate from the second balloon to compare with the previous one.
        for (int i = 1; i < colors.length(); i++) {
            // If the current balloon has the same color as the previous one
            if (colors.charAt(i) == colors.charAt(i - 1)) {
                // To make the rope colorful, one of these must be removed.
                // We keep the one with the higher 'neededTime' and add the lower one to totalCost.
                totalCost += Math.min(maxNeededTime, neededTime[i]);
                // Update maxNeededTime to ensure we always keep the most expensive one in the current group.
                maxNeededTime = Math.max(maxNeededTime, neededTime[i]);
            } else {
                // If the colors are different, the current group of same-colored balloons ends.
                // Reset maxNeededTime to the current balloon's needed time, starting a new potential group.
                maxNeededTime = neededTime[i];
            }
        }
        return totalCost;
    }
}
