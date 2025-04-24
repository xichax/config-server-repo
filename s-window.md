# Longest Substring Without Repeating Characters

## Problem

Given a string `s`, return the length of the **longest substring** without repeating characters.

---

## Example

**Input:**

s = "abcabcbb"

**Output:**

3

**Explanation:**  
The substring `"abc"` has no repeating characters and is the longest such substring.

---

## Approach: Sliding Window

- Use two pointers (`left` and `right`) to represent the current window.
- Use a `HashSet` to store unique characters in the window.
- Move `right` forward:
  - If the character is not in the set, add it and update max length.
  - If it's already in the set, remove characters from the left until it's gone.

---

## Time and Space Complexity

- **Time:** O(n) — Each character is visited at most twice.
- **Space:** O(k) — Where `k` is the number of unique characters (e.g., 128 for ASCII).

---

## Java Code

```java
import java.util.HashSet;

public class LongestUniqueSubstring {
    public static int lengthOfLongestSubstring(String s) {
        HashSet<Character> set = new HashSet<>();
        int left = 0, maxLength = 0;

        for (int right = 0; right < s.length(); right++) {
            while (set.contains(s.charAt(right))) {
                set.remove(s.charAt(left));
                left++;
            }
            set.add(s.charAt(right));
            maxLength = Math.max(maxLength, right - left + 1);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        System.out.println(lengthOfLongestSubstring("abcabcbb")); // Output: 3
    }
}
