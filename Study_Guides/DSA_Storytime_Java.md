# 🧒 DSA Storytime in Java
### *A child-friendly adventure through Data Structures & Algorithms*

> **How to read this guide:** Every topic is a little story. Every problem has a tiny tale that explains *why* the algorithm works, followed by clean Java code. Read like a storybook, code like a wizard. 🧙

---

# 🌍 Chapter 1: Two Pointers
### *"The Two Guards at the Palace Gate"*

Imagine a long hallway of lockers numbered 1 to 100. Two guards stand at each end. They walk **toward each other**, checking if they can find a pair that satisfies a condition. This is the **Two Pointers** trick — instead of checking every pair (slow!), two guards meet in the middle (fast!).

---

### 🏰 Valid Palindrome
*"Is the word the same forwards and backwards?"*

A knight reads a scroll. He checks the first letter and the last letter. If they match, he moves inward. If they ever don't match, the scroll is fake!

```java
public boolean isPalindrome(String s) {
    int left = 0, right = s.length() - 1;
    while (left < right) {
        // skip non-alphanumeric
        while (left < right && !Character.isLetterOrDigit(s.charAt(left))) left++;
        while (left < right && !Character.isLetterOrDigit(s.charAt(right))) right--;
        if (Character.toLowerCase(s.charAt(left)) != Character.toLowerCase(s.charAt(right)))
            return false;
        left++; right--;
    }
    return true;
}
```

---

### 🔺 3Sum
*"Three friends share a debt that sums to zero"*

Sort the friends by wealth. Fix one friend, then use two pointers on the rest to find who can balance the debt.

```java
public List<List<Integer>> threeSum(int[] nums) {
    Arrays.sort(nums);
    List<List<Integer>> result = new ArrayList<>();
    for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue; // skip duplicates
        int left = i + 1, right = nums.length - 1;
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            if (sum == 0) {
                result.add(Arrays.asList(nums[i], nums[left], nums[right]));
                while (left < right && nums[left] == nums[left + 1]) left++;
                while (left < right && nums[right] == nums[right - 1]) right--;
                left++; right--;
            } else if (sum < 0) left++;
            else right--;
        }
    }
    return result;
}
```

---

### 🎨 Sort Colors (Dutch National Flag)
*"Sort red, white, blue balloons in one pass"*

Three buckets: low (red), mid (white), high (blue). Walk through the row and swap balloons to their correct bucket.

```java
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;
    while (mid <= high) {
        if (nums[mid] == 0) { swap(nums, low++, mid++); }
        else if (nums[mid] == 1) { mid++; }
        else { swap(nums, mid, high--); }
    }
}
private void swap(int[] a, int i, int j) { int t = a[i]; a[i] = a[j]; a[j] = t; }
```

---

### 📜 Reverse Words in a String
*"Read the sentence backward, word by word"*

Split the sentence into words, reverse the list, then rejoin. Simple as flipping pancakes!

```java
public String reverseWords(String s) {
    String[] words = s.trim().split("\\s+");
    StringBuilder sb = new StringBuilder();
    for (int i = words.length - 1; i >= 0; i--) {
        sb.append(words[i]);
        if (i > 0) sb.append(" ");
    }
    return sb.toString();
}
```

---

### 📐 Squares of a Sorted Array
*"Square the numbers, biggest squares hide at the edges!"*

The array has negative numbers. Their squares might be huge. Use two pointers from both ends and fill the result from the back.

```java
public int[] sortedSquares(int[] nums) {
    int n = nums.length, left = 0, right = n - 1, pos = n - 1;
    int[] result = new int[n];
    while (left <= right) {
        int lsq = nums[left] * nums[left], rsq = nums[right] * nums[right];
        if (lsq > rsq) { result[pos--] = lsq; left++; }
        else { result[pos--] = rsq; right--; }
    }
    return result;
}
```

---

### 🗺️ Partition Labels
*"Divide the map so each letter only appears in one region"*

Find the last position of each character. Walk the string: the current partition ends at the farthest last-seen position of any character we've visited.

```java
public List<Integer> partitionLabels(String s) {
    int[] last = new int[26];
    for (int i = 0; i < s.length(); i++) last[s.charAt(i) - 'a'] = i;
    List<Integer> result = new ArrayList<>();
    int start = 0, end = 0;
    for (int i = 0; i < s.length(); i++) {
        end = Math.max(end, last[s.charAt(i) - 'a']);
        if (i == end) { result.add(end - start + 1); start = i + 1; }
    }
    return result;
}
```

---

### 🗜️ String Compression
*"Count the repeated letters and shrink the message"*

Walk through the string with two pointers. Count consecutive same letters, then write the letter + count.

```java
public int compress(char[] chars) {
    int write = 0, i = 0;
    while (i < chars.length) {
        char c = chars[i]; int count = 0;
        while (i < chars.length && chars[i] == c) { i++; count++; }
        chars[write++] = c;
        if (count > 1) for (char ch : Integer.toString(count).toCharArray()) chars[write++] = ch;
    }
    return write;
}
```

---

### 🔀 Next Permutation
*"Find the next arrangement in the dictionary"*

Find the first number from the right that is smaller than its neighbor. Swap it with the next larger number to its right. Then reverse the tail.

```java
public void nextPermutation(int[] nums) {
    int n = nums.length, i = n - 2;
    while (i >= 0 && nums[i] >= nums[i + 1]) i--;
    if (i >= 0) {
        int j = n - 1;
        while (nums[j] <= nums[i]) j--;
        swap(nums, i, j);
    }
    // reverse from i+1 to end
    int left = i + 1, right = n - 1;
    while (left < right) swap(nums, left++, right--);
}
```

---

### 🧹 Remove Duplicates from Sorted Array
*"Keep only unique items in a sorted shelf"*

One guard (slow) holds the last unique item. Another guard (fast) scouts ahead and hands unique items to the slow guard.

```java
public int removeDuplicates(int[] nums) {
    int slow = 0;
    for (int fast = 1; fast < nums.length; fast++) {
        if (nums[fast] != nums[slow]) nums[++slow] = nums[fast];
    }
    return slow + 1;
}
```

---

### 🏃 Is Subsequence
*"Can you spell the word by picking letters in order?"*

Walk through the big string. Whenever you find the next letter of the target, move the target pointer forward.

```java
public boolean isSubsequence(String s, String t) {
    int i = 0;
    for (int j = 0; j < t.length() && i < s.length(); j++) {
        if (s.charAt(i) == t.charAt(j)) i++;
    }
    return i == s.length();
}
```

---

# 🐢🐇 Chapter 2: Fast & Slow Pointers
### *"The Tortoise and the Hare"*

Imagine two runners on a circular track. The hare runs twice as fast. If the track is circular (a cycle), the hare will eventually catch the tortoise. This trick detects **cycles** in linked lists!

---

### 🔁 Linked List Cycle
*"Does the road loop forever?"*

```java
public boolean hasCycle(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
        if (slow == fast) return true;
    }
    return false;
}
```

---

### 🏁 Middle of the Linked List
*"Find the center of the bridge"*

When the hare reaches the end, the tortoise is at the middle!

```java
public ListNode middleNode(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next; fast = fast.next.next;
    }
    return slow;
}
```

---

### 🔢 Find The Duplicate Number
*"One number is lying about its locker number"*

Treat array values as pointers. The cycle starts at the duplicate.

```java
public int findDuplicate(int[] nums) {
    int slow = nums[0], fast = nums[0];
    do { slow = nums[slow]; fast = nums[nums[fast]]; } while (slow != fast);
    slow = nums[0];
    while (slow != fast) { slow = nums[slow]; fast = nums[fast]; }
    return slow;
}
```

---

### 📖 Palindrome Linked List
*"Is the chain of beads the same forwards and backwards?"*

Find the middle, reverse the second half, then compare.

```java
public boolean isPalindrome(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) { slow = slow.next; fast = fast.next.next; }
    ListNode rev = reverse(slow);
    ListNode p = head, q = rev;
    while (q != null) { if (p.val != q.val) return false; p = p.next; q = q.next; }
    return true;
}
private ListNode reverse(ListNode node) {
    ListNode prev = null;
    while (node != null) { ListNode next = node.next; node.next = prev; prev = node; node = next; }
    return prev;
}
```

---

### ➕ Maximum Twin Sum of a Linked List
*"The first and last beads are twins. Find the max twin sum."*

Reverse second half, then pair up nodes from front and back.

```java
public int pairSum(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) { slow = slow.next; fast = fast.next.next; }
    ListNode second = reverse(slow);
    int max = 0;
    ListNode first = head;
    while (second != null) { max = Math.max(max, first.val + second.val); first = first.next; second = second.next; }
    return max;
}
```

---

# 🪟 Chapter 3: Sliding Window ⭐ VERY IMPORTANT
### *"The Magic Telescope"*

Imagine looking through a telescope that slides along a number line. You can stretch or shrink the window. The goal: find the best window that satisfies a condition — without restarting from scratch each time!

---

### 🔤 Longest Substring Without Repeating Characters
*"Walk through a hallway — if you see a repeated door, shrink from the left!"*

```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int max = 0, left = 0;
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        if (map.containsKey(c)) left = Math.max(left, map.get(c) + 1);
        map.put(c, right);
        max = Math.max(max, right - left + 1);
    }
    return max;
}
```

---

### 🔁 Longest Repeating Character Replacement
*"You can change at most K characters. What's the longest uniform block?"*

Keep track of the most frequent character in the window. If `window size - max_freq > K`, shrink.

```java
public int characterReplacement(String s, int k) {
    int[] freq = new int[26]; int maxFreq = 0, left = 0, max = 0;
    for (int right = 0; right < s.length(); right++) {
        maxFreq = Math.max(maxFreq, ++freq[s.charAt(right) - 'A']);
        if (right - left + 1 - maxFreq > k) freq[s.charAt(left++) - 'A']--;
        max = Math.max(max, right - left + 1);
    }
    return max;
}
```

---

### 🔍 Minimum Window Substring
*"Find the shortest telegram that contains all required words"*

Expand right until all letters are covered. Then shrink from left while still valid.

```java
public String minWindow(String s, String t) {
    Map<Character, Integer> need = new HashMap<>(), have = new HashMap<>();
    for (char c : t.toCharArray()) need.merge(c, 1, Integer::sum);
    int formed = 0, required = need.size(), left = 0, minLen = Integer.MAX_VALUE, minL = 0;
    for (int right = 0; right < s.length(); right++) {
        char c = s.charAt(right);
        have.merge(c, 1, Integer::sum);
        if (need.containsKey(c) && have.get(c).equals(need.get(c))) formed++;
        while (formed == required) {
            if (right - left + 1 < minLen) { minLen = right - left + 1; minL = left; }
            char lc = s.charAt(left);
            have.merge(lc, -1, Integer::sum);
            if (need.containsKey(lc) && have.get(lc) < need.get(lc)) formed--;
            left++;
        }
    }
    return minLen == Integer.MAX_VALUE ? "" : s.substring(minL, minL + minLen);
}
```

---

### 📏 Minimum Size Subarray Sum
*"What's the shortest shopping list that totals at least S?"*

```java
public int minSubArrayLen(int target, int[] nums) {
    int left = 0, sum = 0, min = Integer.MAX_VALUE;
    for (int right = 0; right < nums.length; right++) {
        sum += nums[right];
        while (sum >= target) { min = Math.min(min, right - left + 1); sum -= nums[left++]; }
    }
    return min == Integer.MAX_VALUE ? 0 : min;
}
```

---

### 🍎🍊 Fruit Into Baskets
*"You have 2 baskets. Each holds one fruit type. Max fruits you can pick consecutively?"*

Longest subarray with at most 2 distinct values.

```java
public int totalFruit(int[] fruits) {
    Map<Integer, Integer> basket = new HashMap<>();
    int left = 0, max = 0;
    for (int right = 0; right < fruits.length; right++) {
        basket.merge(fruits[right], 1, Integer::sum);
        while (basket.size() > 2) {
            int f = fruits[left];
            basket.merge(f, -1, Integer::sum);
            if (basket.get(f) == 0) basket.remove(f);
            left++;
        }
        max = Math.max(max, right - left + 1);
    }
    return max;
}
```

---

### 📊 Frequency of the Most Frequent Element
*"Boost some numbers by adding 1 repeatedly. Max frequency you can achieve with K operations?"*

Sort the array. Slide window. If cost to equalize > k, shrink.

```java
public int maxFrequency(int[] nums, int k) {
    Arrays.sort(nums);
    long sum = 0; int left = 0, max = 0;
    for (int right = 0; right < nums.length; right++) {
        sum += nums[right];
        while ((long) nums[right] * (right - left + 1) - sum > k) sum -= nums[left++];
        max = Math.max(max, right - left + 1);
    }
    return max;
}
```

---

### 🟦 Binary Subarrays With Sum
*"How many subarrays sum to exactly S?"*

Use prefix sum + hashmap to count subarrays.

```java
public int numSubarraysWithSum(int[] nums, int goal) {
    Map<Integer, Integer> map = new HashMap<>();
    map.put(0, 1);
    int sum = 0, count = 0;
    for (int n : nums) {
        sum += n;
        count += map.getOrDefault(sum - goal, 0);
        map.merge(sum, 1, Integer::sum);
    }
    return count;
}
```

---

### 🔄 Permutation in String
*"Is any rearrangement of s1 hiding inside s2?"*

Fixed-size window of length s1. Compare character frequencies.

```java
public boolean checkInclusion(String s1, String s2) {
    int[] freq = new int[26];
    for (char c : s1.toCharArray()) freq[c - 'a']++;
    int left = 0, count = s1.length();
    for (int right = 0; right < s2.length(); right++) {
        if (freq[s2.charAt(right) - 'a']-- > 0) count--;
        if (count == 0) return true;
        if (right - left + 1 == s1.length() && freq[s2.charAt(left++) - 'a']++ >= 0) count++;
    }
    return false;
}
```

---

### 🔢 Number of Substrings Containing All Three Characters
*"How many substrings have at least one a, b, and c?"*

```java
public int numberOfSubstrings(String s) {
    int[] last = {-1, -1, -1}; int result = 0;
    for (int i = 0; i < s.length(); i++) {
        last[s.charAt(i) - 'a'] = i;
        result += 1 + Math.min(last[0], Math.min(last[1], last[2]));
    }
    return result;
}
```

---

### 🏔️ Sliding Window Maximum
*"As a window of size k slides, what's the max in each window?"*

Use a deque to keep track of the max candidate index.

```java
public int[] maxSlidingWindow(int[] nums, int k) {
    int n = nums.length;
    int[] result = new int[n - k + 1];
    Deque<Integer> dq = new ArrayDeque<>();
    for (int i = 0; i < n; i++) {
        if (!dq.isEmpty() && dq.peekFirst() < i - k + 1) dq.pollFirst();
        while (!dq.isEmpty() && nums[dq.peekLast()] < nums[i]) dq.pollLast();
        dq.offerLast(i);
        if (i >= k - 1) result[i - k + 1] = nums[dq.peekFirst()];
    }
    return result;
}
```

---

# ⏱️ Chapter 4: Intervals
### *"The Meeting Room Chronicles"*

Picture a shared conference room. Many teams book it. Can everyone meet? Do any bookings overlap? Let's sort the meetings and figure it out!

---

### 🔗 Merge Intervals
*"Overlapping meetings become one big meeting"*

Sort by start time. If the next meeting starts before the current one ends, merge them.

```java
public int[][] merge(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    List<int[]> result = new ArrayList<>();
    for (int[] interval : intervals) {
        if (result.isEmpty() || result.get(result.size()-1)[1] < interval[0])
            result.add(interval);
        else
            result.get(result.size()-1)[1] = Math.max(result.get(result.size()-1)[1], interval[1]);
    }
    return result.toArray(new int[0][]);
}
```

---

### ➕ Insert Interval
*"A new meeting arrives. Insert it, merge if needed."*

```java
public int[][] insert(int[][] intervals, int[] newInterval) {
    List<int[]> result = new ArrayList<>();
    int i = 0, n = intervals.length;
    while (i < n && intervals[i][1] < newInterval[0]) result.add(intervals[i++]);
    while (i < n && intervals[i][0] <= newInterval[1]) {
        newInterval[0] = Math.min(newInterval[0], intervals[i][0]);
        newInterval[1] = Math.max(newInterval[1], intervals[i][1]);
        i++;
    }
    result.add(newInterval);
    while (i < n) result.add(intervals[i++]);
    return result.toArray(new int[0][]);
}
```

---

### 🏢 Meeting Rooms II
*"How many rooms do we need for all meetings?"*

Sort start times and end times separately. Simulate using a min-heap of end times.

```java
public int minMeetingRooms(int[][] intervals) {
    Arrays.sort(intervals, (a, b) -> a[0] - b[0]);
    PriorityQueue<Integer> heap = new PriorityQueue<>();
    for (int[] interval : intervals) {
        if (!heap.isEmpty() && heap.peek() <= interval[0]) heap.poll();
        heap.offer(interval[1]);
    }
    return heap.size();
}
```

---

### ✂️ Interval List Intersections
*"Find common busy times between two people"*

Two pointers on both lists. Move the one that ends earlier.

```java
public int[][] intervalIntersection(int[][] A, int[][] B) {
    List<int[]> result = new ArrayList<>();
    int i = 0, j = 0;
    while (i < A.length && j < B.length) {
        int lo = Math.max(A[i][0], B[j][0]), hi = Math.min(A[i][1], B[j][1]);
        if (lo <= hi) result.add(new int[]{lo, hi});
        if (A[i][1] < B[j][1]) i++; else j++;
    }
    return result.toArray(new int[0][]);
}
```

---

### 🗂️ Task Scheduler
*"Schedule CPU tasks with cooldown between same tasks. Minimum time?"*

The most frequent task defines idle slots needed.

```java
public int leastInterval(char[] tasks, int n) {
    int[] freq = new int[26];
    for (char c : tasks) freq[c - 'A']++;
    Arrays.sort(freq);
    int maxFreq = freq[25];
    int idleSlots = (maxFreq - 1) * n;
    for (int i = 24; i >= 0; i--) idleSlots -= Math.min(freq[i], maxFreq - 1);
    return tasks.length + Math.max(0, idleSlots);
}
```

---

### 🚗 Car Pooling
*"Can one van pick and drop all passengers without overflowing?"*

At each stop, add boarding passengers and subtract departing passengers. Check capacity.

```java
public boolean carPooling(int[][] trips, int capacity) {
    int[] stops = new int[1001];
    for (int[] t : trips) { stops[t[1]] += t[0]; stops[t[2]] -= t[0]; }
    int curr = 0;
    for (int s : stops) { curr += s; if (curr > capacity) return false; }
    return true;
}
```

---

# 🔄 Chapter 5: Linked List In-place
### *"The Chain Gang"*

A linked list is a chain of nodes. Each node knows only its neighbor. In-place means we rearrange by relinking — no extra memory!

---

### ↩️ Reverse Linked List
*"Flip the chain: the tail becomes the head"*

```java
public ListNode reverseList(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) { ListNode next = curr.next; curr.next = prev; prev = curr; curr = next; }
    return prev;
}
```

---

### 🔁 Reorder List
*"Weave the front and back of the list together"*

1. Find middle. 2. Reverse second half. 3. Merge alternately.

```java
public void reorderList(ListNode head) {
    ListNode slow = head, fast = head;
    while (fast.next != null && fast.next.next != null) { slow = slow.next; fast = fast.next.next; }
    ListNode second = reverse(slow.next); slow.next = null;
    ListNode first = head;
    while (second != null) {
        ListNode tmp1 = first.next, tmp2 = second.next;
        first.next = second; second.next = tmp1;
        first = tmp1; second = tmp2;
    }
}
```

---

### ↩️ Reverse Linked List II
*"Reverse only positions m to n in the chain"*

```java
public ListNode reverseBetween(ListNode head, int left, int right) {
    ListNode dummy = new ListNode(0); dummy.next = head;
    ListNode pre = dummy;
    for (int i = 1; i < left; i++) pre = pre.next;
    ListNode curr = pre.next;
    for (int i = 0; i < right - left; i++) {
        ListNode next = curr.next; curr.next = next.next;
        next.next = pre.next; pre.next = next;
    }
    return dummy.next;
}
```

---

### 🔀 Swap Nodes in Pairs
*"Swap every two adjacent beads in the necklace"*

```java
public ListNode swapPairs(ListNode head) {
    ListNode dummy = new ListNode(0); dummy.next = head;
    ListNode prev = dummy;
    while (prev.next != null && prev.next.next != null) {
        ListNode a = prev.next, b = prev.next.next;
        prev.next = b; a.next = b.next; b.next = a; prev = a;
    }
    return dummy.next;
}
```

---

### 🔢 Odd Even Linked List
*"Put all odd-indexed nodes first, then even-indexed nodes"*

```java
public ListNode oddEvenList(ListNode head) {
    if (head == null) return null;
    ListNode odd = head, even = head.next, evenHead = even;
    while (even != null && even.next != null) {
        odd.next = even.next; odd = odd.next;
        even.next = odd.next; even = even.next;
    }
    odd.next = evenHead;
    return head;
}
```

---

### 🌀 Rotate List
*"Spin the chain k steps to the right"*

Find the tail, count length, compute actual rotation point, re-link.

```java
public ListNode rotateRight(ListNode head, int k) {
    if (head == null) return null;
    ListNode tail = head; int len = 1;
    while (tail.next != null) { tail = tail.next; len++; }
    k %= len; if (k == 0) return head;
    tail.next = head; // make circular
    ListNode newTail = head;
    for (int i = 0; i < len - k - 1; i++) newTail = newTail.next;
    ListNode newHead = newTail.next; newTail.next = null;
    return newHead;
}
```

---

### 🔁 Reverse Nodes in k-Group *(Optional)*
*"Reverse every group of k beads"*

```java
public ListNode reverseKGroup(ListNode head, int k) {
    ListNode curr = head; int count = 0;
    while (curr != null && count < k) { curr = curr.next; count++; }
    if (count < k) return head;
    curr = reverse(head, k);
    head.next = reverseKGroup(curr, k);
    return curr; // new head after reversal (tracked by the reverse helper)
}
// note: this is a conceptual version; full impl reverses in-place
```

---

# ⛏️ Chapter 6: Heaps / Priority Queue
### *"The Magic Sorting Hat"*

A heap is like a hat that always gives you the smallest (or largest) item first. It's perfect when you need repeated access to the "best" item.

---

### 📊 Find Median from Data Stream
*"At any moment, what's the middle value?"*

Use two heaps: a max-heap for the lower half, a min-heap for the upper half.

```java
class MedianFinder {
    PriorityQueue<Integer> lo = new PriorityQueue<>(Collections.reverseOrder()); // max-heap
    PriorityQueue<Integer> hi = new PriorityQueue<>(); // min-heap
    public void addNum(int num) {
        lo.offer(num);
        hi.offer(lo.poll());
        if (lo.size() < hi.size()) lo.offer(hi.poll());
    }
    public double findMedian() {
        return lo.size() > hi.size() ? lo.peek() : (lo.peek() + hi.peek()) / 2.0;
    }
}
```

---

### 🏢 Meeting Rooms III
*"Which room hosts the most meetings?"*

Use two heaps: one for unused rooms, one for (end_time, room) of active meetings.

```java
public int mostBooked(int n, int[][] meetings) {
    Arrays.sort(meetings, (a, b) -> a[0] - b[0]);
    PriorityQueue<Integer> free = new PriorityQueue<>();
    PriorityQueue<long[]> busy = new PriorityQueue<>((a, b) -> a[0] != b[0] ? Long.compare(a[0], b[0]) : Long.compare(a[1], b[1]));
    int[] count = new int[n];
    for (int i = 0; i < n; i++) free.offer(i);
    for (int[] m : meetings) {
        while (!busy.isEmpty() && busy.peek()[0] <= m[0]) free.offer((int) busy.poll()[1]);
        if (!free.isEmpty()) { int room = free.poll(); count[room]++; busy.offer(new long[]{m[1], room}); }
        else { long[] earliest = busy.poll(); count[(int) earliest[1]]++; busy.offer(new long[]{earliest[0] + m[1] - m[0], earliest[1]}); }
    }
    int maxRoom = 0;
    for (int i = 1; i < n; i++) if (count[i] > count[maxRoom]) maxRoom = i;
    return maxRoom;
}
```

---

### 🪢 Minimum Cost to Connect Sticks
*"Merge the cheapest two sticks first, always!"*

Greedy with a min-heap: always combine the two smallest.

```java
public int connectSticks(int[] sticks) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int s : sticks) pq.offer(s);
    int cost = 0;
    while (pq.size() > 1) {
        int combined = pq.poll() + pq.poll();
        cost += combined;
        pq.offer(combined);
    }
    return cost;
}
```

---

### 📈 Maximum Average Pass Ratio
*"Add extra students to classes to maximize average pass rate"*

Greedily add each student to the class with the maximum gain in pass ratio.

```java
public double maxAverageRatio(int[][] classes, int extraStudents) {
    PriorityQueue<double[]> pq = new PriorityQueue<>((a, b) -> Double.compare(gain(b), gain(a)));
    for (int[] c : classes) pq.offer(new double[]{c[0], c[1]});
    while (extraStudents-- > 0) {
        double[] top = pq.poll();
        pq.offer(new double[]{top[0] + 1, top[1] + 1});
    }
    double sum = 0;
    while (!pq.isEmpty()) { double[] c = pq.poll(); sum += c[0] / c[1]; }
    return sum / classes.length;
}
private double gain(double[] c) { return (c[0] + 1) / (c[1] + 1) - c[0] / c[1]; }
```

---

### 🔍 Find Right Interval
*"For each interval's end, find the interval that starts at or just after it"*

Sort start points with their indices. For each end, binary search.

```java
public int[] findRightInterval(int[][] intervals) {
    TreeMap<Integer, Integer> starts = new TreeMap<>();
    for (int i = 0; i < intervals.length; i++) starts.put(intervals[i][0], i);
    int[] result = new int[intervals.length];
    for (int i = 0; i < intervals.length; i++) {
        Map.Entry<Integer, Integer> e = starts.ceilingEntry(intervals[i][1]);
        result[i] = e == null ? -1 : e.getValue();
    }
    return result;
}
```

---

# 🔀 Chapter 7: K-way Merge
### *"Merging Many Sorted Rivers"*

Imagine k rivers flowing downward, each already sorted. You want to merge them into one sorted river. Always take the smallest current element across all rivers!

---

### 🔗 Merge K Sorted Lists
*"Merge k sorted linked lists into one"*

Use a min-heap to always pick the smallest head.

```java
public ListNode mergeKLists(ListNode[] lists) {
    PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
    for (ListNode l : lists) if (l != null) pq.offer(l);
    ListNode dummy = new ListNode(0), curr = dummy;
    while (!pq.isEmpty()) {
        ListNode node = pq.poll();
        curr.next = node; curr = curr.next;
        if (node.next != null) pq.offer(node.next);
    }
    return dummy.next;
}
```

---

### 👫 Find K Pairs with Smallest Sums
*"From two sorted arrays, find k pairs with smallest sums"*

Start with pairs (i=0, j=0..k). Use a min-heap, expand by incrementing i.

```java
public List<List<Integer>> kSmallestPairs(int[] nums1, int[] nums2, int k) {
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> (nums1[a[0]] + nums2[a[1]]) - (nums1[b[0]] + nums2[b[1]]));
    List<List<Integer>> result = new ArrayList<>();
    for (int j = 0; j < Math.min(k, nums2.length); j++) pq.offer(new int[]{0, j});
    while (!pq.isEmpty() && k-- > 0) {
        int[] p = pq.poll();
        result.add(Arrays.asList(nums1[p[0]], nums2[p[1]]));
        if (p[0] + 1 < nums1.length) pq.offer(new int[]{p[0] + 1, p[1]});
    }
    return result;
}
```

---

### 🔢 Kth Smallest Element in a Sorted Matrix
*"A matrix sorted by row and column. Find the kth smallest."*

Min-heap: start from (0,0), expand right and down.

```java
public int kthSmallest(int[][] matrix, int k) {
    int n = matrix.length;
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[0] - b[0]);
    for (int i = 0; i < n; i++) pq.offer(new int[]{matrix[i][0], i, 0});
    while (k-- > 1) {
        int[] curr = pq.poll();
        if (curr[2] + 1 < n) pq.offer(new int[]{matrix[curr[1]][curr[2] + 1], curr[1], curr[2] + 1});
    }
    return pq.poll()[0];
}
```

---

# 🏆 Chapter 8: Top K Elements
### *"The Talent Show — Find the Best K!"*

We need the top K items from a large set. Instead of sorting everything (expensive), we keep a small heap of size K!

---

### 📊 Top K Frequent Elements
*"Which k numbers appear most often in the list?"*

```java
public int[] topKFrequent(int[] nums, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : nums) freq.merge(n, 1, Integer::sum);
    PriorityQueue<Integer> pq = new PriorityQueue<>((a, b) -> freq.get(a) - freq.get(b));
    for (int num : freq.keySet()) {
        pq.offer(num);
        if (pq.size() > k) pq.poll();
    }
    return pq.stream().mapToInt(Integer::intValue).toArray();
}
```

---

### 📍 K Closest Points to Origin
*"Which k points are nearest to (0,0)?"*

Use a max-heap of size k; eject the farthest when full.

```java
public int[][] kClosest(int[][] points, int k) {
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> dist(b) - dist(a));
    for (int[] p : points) {
        pq.offer(p);
        if (pq.size() > k) pq.poll();
    }
    return pq.toArray(new int[0][]);
}
private int dist(int[] p) { return p[0]*p[0] + p[1]*p[1]; }
```

---

### 🥇 Kth Largest Element in an Array
*"Find the kth biggest trophy"*

Min-heap of size k. When full, eject the smallest.

```java
public int findKthLargest(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int n : nums) { pq.offer(n); if (pq.size() > k) pq.poll(); }
    return pq.peek();
}
```

---

### 🎵 Reorganize String
*"Arrange characters so no two adjacent are the same"*

Always pick the most frequent remaining character that isn't the last used.

```java
public String reorganizeString(String s) {
    int[] freq = new int[26];
    for (char c : s.toCharArray()) freq[c - 'a']++;
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> b[1] - a[1]);
    for (int i = 0; i < 26; i++) if (freq[i] > 0) pq.offer(new int[]{i, freq[i]});
    StringBuilder sb = new StringBuilder();
    while (pq.size() >= 2) {
        int[] a = pq.poll(), b = pq.poll();
        sb.append((char)('a' + a[0])); sb.append((char)('a' + b[0]));
        if (--a[1] > 0) pq.offer(a);
        if (--b[1] > 0) pq.offer(b);
    }
    if (!pq.isEmpty()) {
        int[] rem = pq.poll();
        if (rem[1] > 1) return "";
        sb.append((char)('a' + rem[0]));
    }
    return sb.length() == s.length() ? sb.toString() : "";
}
```

---

### 🗑️ Least Number of Unique Integers after K Removals
*"Remove k elements. Minimize the number of unique values left."*

Remove rarest elements first.

```java
public int findLeastNumOfUniqueInts(int[] arr, int k) {
    Map<Integer, Integer> freq = new HashMap<>();
    for (int n : arr) freq.merge(n, 1, Integer::sum);
    List<Integer> counts = new ArrayList<>(freq.values());
    Collections.sort(counts);
    int removed = 0;
    for (int i = 0; i < counts.size(); i++) {
        if (k >= counts.get(i)) { k -= counts.get(i); removed++; }
        else break;
    }
    return counts.size() - removed;
}
```

---

### ⬆️ Maximum Product After K Increments
*"Increment the minimum element k times to maximize the product"*

```java
public int maximumProduct(int[] nums, int k) {
    PriorityQueue<Integer> pq = new PriorityQueue<>();
    for (int n : nums) pq.offer(n);
    while (k-- > 0) pq.offer(pq.poll() + 1);
    long product = 1;
    final int MOD = 1_000_000_007;
    while (!pq.isEmpty()) product = product * pq.poll() % MOD;
    return (int) product;
}
```

---

# 🔍 Chapter 9: Binary Search ⭐ VERY HIGH ROI
### *"The Encyclopedia Lookup"*

Imagine finding a word in a dictionary. You don't start from page 1! You open the middle. Too far? Go left. Not far enough? Go right. **Binary Search** halves the problem every step — it's blazing fast!

---

### 📖 Binary Search
*"Find the target in a sorted bookshelf"*

```java
public int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return -1;
}
```

---

### 🌀 Search in Rotated Sorted Array
*"The bookshelf was rotated. Find the target anyway."*

One half is always sorted. Check which half the target is in.

```java
public int search(int[] nums, int target) {
    int left = 0, right = nums.length - 1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) return mid;
        if (nums[left] <= nums[mid]) { // left half sorted
            if (target >= nums[left] && target < nums[mid]) right = mid - 1;
            else left = mid + 1;
        } else { // right half sorted
            if (target > nums[mid] && target <= nums[right]) left = mid + 1;
            else right = mid - 1;
        }
    }
    return -1;
}
```

---

### 📍 Find K Closest Elements
*"Find k numbers closest to x in a sorted array"*

Binary search for the left boundary of the k-element window.

```java
public List<Integer> findClosestElements(int[] arr, int k, int x) {
    int left = 0, right = arr.length - k;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (x - arr[mid] > arr[mid + k] - x) left = mid + 1;
        else right = mid;
    }
    List<Integer> result = new ArrayList<>();
    for (int i = left; i < left + k; i++) result.add(arr[i]);
    return result;
}
```

---

### 🔍 Single Element in a Sorted Array
*"Every number appears twice except one. Find the lone wolf."*

```java
public int singleNonDuplicate(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (mid % 2 == 1) mid--; // make mid even
        if (nums[mid] == nums[mid + 1]) left = mid + 2;
        else right = mid;
    }
    return nums[left];
}
```

---

### 🍌 Koko Eating Bananas
*"Eat all bananas in h hours. Find minimum speed k."*

Binary search on the speed. Check if that speed is enough.

```java
public int minEatingSpeed(int[] piles, int h) {
    int left = 1, right = Arrays.stream(piles).max().getAsInt();
    while (left < right) {
        int mid = left + (right - left) / 2;
        int hours = 0;
        for (int p : piles) hours += (p + mid - 1) / mid;
        if (hours <= h) right = mid; else left = mid + 1;
    }
    return left;
}
```

---

### ⛰️ Find Peak Element
*"Find any peak (greater than neighbors)"*

Binary search: move toward the higher neighbor.

```java
public int findPeakElement(int[] nums) {
    int left = 0, right = nums.length - 1;
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] < nums[mid + 1]) left = mid + 1;
        else right = mid;
    }
    return left;
}
```

---

### 🎯 Find First and Last Position
*"Find the starting and ending index of target in sorted array"*

Two binary searches: one for leftmost, one for rightmost.

```java
public int[] searchRange(int[] nums, int target) {
    return new int[]{findFirst(nums, target), findLast(nums, target)};
}
private int findFirst(int[] nums, int target) {
    int left = 0, right = nums.length - 1, idx = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) { idx = mid; right = mid - 1; }
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return idx;
}
private int findLast(int[] nums, int target) {
    int left = 0, right = nums.length - 1, idx = -1;
    while (left <= right) {
        int mid = left + (right - left) / 2;
        if (nums[mid] == target) { idx = mid; left = mid + 1; }
        else if (nums[mid] < target) left = mid + 1;
        else right = mid - 1;
    }
    return idx;
}
```

---

### 📦 Split Array Largest Sum
*"Split array into m parts to minimize the largest part sum"*

Binary search on the answer (the max sum). Check if m parts are enough.

```java
public int splitArray(int[] nums, int m) {
    int left = Arrays.stream(nums).max().getAsInt(), right = Arrays.stream(nums).sum();
    while (left < right) {
        int mid = left + (right - left) / 2;
        if (canSplit(nums, m, mid)) right = mid; else left = mid + 1;
    }
    return left;
}
private boolean canSplit(int[] nums, int m, int limit) {
    int parts = 1, sum = 0;
    for (int n : nums) {
        if (sum + n > limit) { parts++; sum = n; if (parts > m) return false; }
        else sum += n;
    }
    return true;
}
```

---

# 🌳 Chapter 10: Backtracking
### *"The Maze Explorer"*

Backtracking is like exploring a maze. Try a path. If it leads to a dead end, go back and try another way. It's exhaustive but smart — we only go back when we're stuck.

---

### 🧩 Subsets
*"All possible groups from a bag of items"*

```java
public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, 0, new ArrayList<>(), result);
    return result;
}
private void backtrack(int[] nums, int start, List<Integer> current, List<List<Integer>> result) {
    result.add(new ArrayList<>(current));
    for (int i = start; i < nums.length; i++) {
        current.add(nums[i]);
        backtrack(nums, i + 1, current, result);
        current.remove(current.size() - 1);
    }
}
```

---

### 🔢 Permutations
*"All arrangements of numbers"*

```java
public List<List<Integer>> permute(int[] nums) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(nums, new ArrayList<>(), new boolean[nums.length], result);
    return result;
}
private void backtrack(int[] nums, List<Integer> curr, boolean[] used, List<List<Integer>> result) {
    if (curr.size() == nums.length) { result.add(new ArrayList<>(curr)); return; }
    for (int i = 0; i < nums.length; i++) {
        if (used[i]) continue;
        used[i] = true; curr.add(nums[i]);
        backtrack(nums, curr, used, result);
        used[i] = false; curr.remove(curr.size() - 1);
    }
}
```

---

### 🔣 Generate Parentheses
*"Build all valid bracket combinations"*

```java
public List<String> generateParenthesis(int n) {
    List<String> result = new ArrayList<>();
    backtrack("", 0, 0, n, result);
    return result;
}
private void backtrack(String s, int open, int close, int n, List<String> result) {
    if (s.length() == 2 * n) { result.add(s); return; }
    if (open < n) backtrack(s + "(", open + 1, close, n, result);
    if (close < open) backtrack(s + ")", open, close + 1, n, result);
}
```

---

### 📱 Letter Combinations of a Phone Number
*"Map each digit to letters. Find all combinations."*

```java
public List<String> letterCombinations(String digits) {
    if (digits.isEmpty()) return new ArrayList<>();
    String[] map = {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};
    List<String> result = new ArrayList<>();
    backtrack(digits, 0, new StringBuilder(), map, result);
    return result;
}
private void backtrack(String digits, int i, StringBuilder curr, String[] map, List<String> result) {
    if (i == digits.length()) { result.add(curr.toString()); return; }
    for (char c : map[digits.charAt(i) - '0'].toCharArray()) {
        curr.append(c);
        backtrack(digits, i + 1, curr, map, result);
        curr.deleteCharAt(curr.length() - 1);
    }
}
```

---

### 🔤 Word Search
*"Find the word hidden in the grid"*

```java
public boolean exist(char[][] board, String word) {
    for (int i = 0; i < board.length; i++)
        for (int j = 0; j < board[0].length; j++)
            if (dfs(board, word, i, j, 0)) return true;
    return false;
}
private boolean dfs(char[][] board, String word, int i, int j, int k) {
    if (k == word.length()) return true;
    if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] != word.charAt(k)) return false;
    char temp = board[i][j]; board[i][j] = '#';
    boolean found = dfs(board, word, i+1, j, k+1) || dfs(board, word, i-1, j, k+1)
                 || dfs(board, word, i, j+1, k+1) || dfs(board, word, i, j-1, k+1);
    board[i][j] = temp;
    return found;
}
```

---

### 🔢 Combinations
*"Choose k numbers from 1 to n"*

```java
public List<List<Integer>> combine(int n, int k) {
    List<List<Integer>> result = new ArrayList<>();
    backtrack(n, k, 1, new ArrayList<>(), result);
    return result;
}
private void backtrack(int n, int k, int start, List<Integer> curr, List<List<Integer>> result) {
    if (curr.size() == k) { result.add(new ArrayList<>(curr)); return; }
    for (int i = start; i <= n; i++) {
        curr.add(i);
        backtrack(n, k, i + 1, curr, result);
        curr.remove(curr.size() - 1);
    }
}
```

---

### 👑 N-Queens *(Understand the pattern)*
*"Place N queens on an N×N board so none attack each other"*

```java
public List<List<String>> solveNQueens(int n) {
    List<List<String>> result = new ArrayList<>();
    int[] queens = new int[n]; Arrays.fill(queens, -1);
    Set<Integer> cols = new HashSet<>(), diag1 = new HashSet<>(), diag2 = new HashSet<>();
    backtrack(n, 0, queens, cols, diag1, diag2, result);
    return result;
}
private void backtrack(int n, int row, int[] queens, Set<Integer> cols, Set<Integer> diag1, Set<Integer> diag2, List<List<String>> result) {
    if (row == n) { result.add(buildBoard(queens, n)); return; }
    for (int col = 0; col < n; col++) {
        if (cols.contains(col) || diag1.contains(row - col) || diag2.contains(row + col)) continue;
        queens[row] = col; cols.add(col); diag1.add(row - col); diag2.add(row + col);
        backtrack(n, row + 1, queens, cols, diag1, diag2, result);
        queens[row] = -1; cols.remove(col); diag1.remove(row - col); diag2.remove(row + col);
    }
}
private List<String> buildBoard(int[] queens, int n) {
    List<String> board = new ArrayList<>();
    for (int q : queens) {
        char[] row = new char[n]; Arrays.fill(row, '.'); row[q] = 'Q'; board.add(new String(row));
    }
    return board;
}
```

---

# 💰 Chapter 11: Greedy
### *"Always Take the Best Deal Right Now"*

Greedy means making the locally optimal choice at each step, trusting it leads to a globally optimal solution. Like always picking the ripest fruit first!

---

### 🦘 Jump Game I
*"Can you reach the last index?"*

Track the farthest reachable index.

```java
public boolean canJump(int[] nums) {
    int reach = 0;
    for (int i = 0; i < nums.length; i++) {
        if (i > reach) return false;
        reach = Math.max(reach, i + nums[i]);
    }
    return true;
}
```

---

### 🦘 Jump Game II
*"Minimum jumps to reach the end"*

```java
public int jump(int[] nums) {
    int jumps = 0, currEnd = 0, farthest = 0;
    for (int i = 0; i < nums.length - 1; i++) {
        farthest = Math.max(farthest, i + nums[i]);
        if (i == currEnd) { jumps++; currEnd = farthest; }
    }
    return jumps;
}
```

---

### ⛽ Gas Station
*"Can you complete the circuit? From which station?"*

If total gas >= total cost, a solution exists. Start tracking where the deficit resets.

```java
public int canCompleteCircuit(int[] gas, int[] cost) {
    int total = 0, tank = 0, start = 0;
    for (int i = 0; i < gas.length; i++) {
        total += gas[i] - cost[i];
        tank += gas[i] - cost[i];
        if (tank < 0) { start = i + 1; tank = 0; }
    }
    return total >= 0 ? start : -1;
}
```

---

### 🚣 Boats to Save People
*"Pair heaviest and lightest if possible — min boats needed"*

```java
public int numRescueBoats(int[] people, int limit) {
    Arrays.sort(people);
    int left = 0, right = people.length - 1, boats = 0;
    while (left <= right) {
        if (people[left] + people[right] <= limit) left++;
        right--; boats++;
    }
    return boats;
}
```

---

### 🍬 Candy
*"Give each child at least 1 candy. Higher-rated kids get more than neighbors."*

Two passes: left-to-right (honor right neighbor), right-to-left (honor left neighbor).

```java
public int candy(int[] ratings) {
    int n = ratings.length;
    int[] candy = new int[n]; Arrays.fill(candy, 1);
    for (int i = 1; i < n; i++) if (ratings[i] > ratings[i-1]) candy[i] = candy[i-1] + 1;
    for (int i = n - 2; i >= 0; i--) if (ratings[i] > ratings[i+1]) candy[i] = Math.max(candy[i], candy[i+1] + 1);
    return Arrays.stream(candy).sum();
}
```

---

### 🔢 Remove K Digits
*"Remove k digits to make the smallest number possible"*

Use a monotonic stack. Keep smaller digits, remove larger ones greedily.

```java
public String removeKdigits(String num, int k) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : num.toCharArray()) {
        while (k > 0 && !stack.isEmpty() && stack.peek() > c) { stack.pop(); k--; }
        stack.push(c);
    }
    while (k-- > 0) stack.pop();
    StringBuilder sb = new StringBuilder();
    while (!stack.isEmpty()) sb.append(stack.pollLast());
    // remove leading zeros
    int start = 0;
    while (start < sb.length() - 1 && sb.charAt(start) == '0') start++;
    return sb.substring(start);
}
```

---

### 📈 Best Time to Buy and Sell Stock II
*"Buy and sell multiple times for maximum profit"*

Grab every uphill gain!

```java
public int maxProfit(int[] prices) {
    int profit = 0;
    for (int i = 1; i < prices.length; i++)
        if (prices[i] > prices[i-1]) profit += prices[i] - prices[i-1];
    return profit;
}
```

---

# 🧠 Chapter 12: Dynamic Programming ⭐ MOST IMPORTANT
### *"Remember Your Past Work"*

DP is like a memory notebook. Instead of solving the same sub-problem again, you write down the answer and look it up. It turns exponential problems into polynomial ones!

---

### 🪙 Coin Change
*"Minimum coins to make amount N"*

```java
public int coinChange(int[] coins, int amount) {
    int[] dp = new int[amount + 1]; Arrays.fill(dp, amount + 1);
    dp[0] = 0;
    for (int i = 1; i <= amount; i++)
        for (int coin : coins)
            if (coin <= i) dp[i] = Math.min(dp[i], dp[i - coin] + 1);
    return dp[amount] > amount ? -1 : dp[amount];
}
```

---

### ✖️ Maximum Product Subarray
*"Find the contiguous subarray with the largest product"*

Track both max and min (negatives flip sign!).

```java
public int maxProduct(int[] nums) {
    int max = nums[0], min = nums[0], result = nums[0];
    for (int i = 1; i < nums.length; i++) {
        int tempMax = Math.max(nums[i], Math.max(max * nums[i], min * nums[i]));
        min = Math.min(nums[i], Math.min(max * nums[i], min * nums[i]));
        max = tempMax;
        result = Math.max(result, max);
    }
    return result;
}
```

---

### 💬 Word Break
*"Can the string be segmented into dictionary words?"*

```java
public boolean wordBreak(String s, List<String> wordDict) {
    Set<String> dict = new HashSet<>(wordDict);
    boolean[] dp = new boolean[s.length() + 1]; dp[0] = true;
    for (int i = 1; i <= s.length(); i++)
        for (int j = 0; j < i; j++)
            if (dp[j] && dict.contains(s.substring(j, i))) { dp[i] = true; break; }
    return dp[s.length()];
}
```

---

### 🔤 Longest Common Subsequence
*"Longest sequence present in both strings (not necessarily contiguous)"*

```java
public int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length(), n = text2.length();
    int[][] dp = new int[m + 1][n + 1];
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            dp[i][j] = text1.charAt(i-1) == text2.charAt(j-1)
                ? dp[i-1][j-1] + 1
                : Math.max(dp[i-1][j], dp[i][j-1]);
    return dp[m][n];
}
```

---

### 🔢 Decode Ways
*"How many ways to decode the digit string?"*

```java
public int numDecodings(String s) {
    int n = s.length();
    int[] dp = new int[n + 1]; dp[0] = 1;
    dp[1] = s.charAt(0) == '0' ? 0 : 1;
    for (int i = 2; i <= n; i++) {
        int one = s.charAt(i-1) - '0';
        int two = Integer.parseInt(s.substring(i-2, i));
        if (one >= 1) dp[i] += dp[i-1];
        if (two >= 10 && two <= 26) dp[i] += dp[i-2];
    }
    return dp[n];
}
```

---

### 🧗 Climbing Stairs
*"1 or 2 steps at a time. How many ways to climb n stairs?"*

```java
public int climbStairs(int n) {
    if (n <= 2) return n;
    int a = 1, b = 2;
    for (int i = 3; i <= n; i++) { int c = a + b; a = b; b = c; }
    return b;
}
```

---

### ⚖️ Partition Equal Subset Sum
*"Can you split the array into two equal-sum halves?"*

0/1 Knapsack: can we make sum/2?

```java
public boolean canPartition(int[] nums) {
    int total = Arrays.stream(nums).sum();
    if (total % 2 != 0) return false;
    int target = total / 2;
    boolean[] dp = new boolean[target + 1]; dp[0] = true;
    for (int n : nums)
        for (int j = target; j >= n; j--)
            dp[j] = dp[j] || dp[j - n];
    return dp[target];
}
```

---

### 🏠 House Robber II
*"Houses in a circle. Rob max without robbing adjacent."*

Rob range [0, n-2] or [1, n-1], take the max.

```java
public int rob(int[] nums) {
    int n = nums.length;
    if (n == 1) return nums[0];
    return Math.max(robRange(nums, 0, n - 2), robRange(nums, 1, n - 1));
}
private int robRange(int[] nums, int lo, int hi) {
    int prev = 0, curr = 0;
    for (int i = lo; i <= hi; i++) { int next = Math.max(curr, prev + nums[i]); prev = curr; curr = next; }
    return curr;
}
```

---

### 📐 Triangle
*"Find minimum path sum from top to bottom of triangle"*

```java
public int minimumTotal(List<List<Integer>> triangle) {
    int n = triangle.size();
    int[] dp = new int[n];
    for (int i = 0; i < n; i++) dp[i] = triangle.get(n-1).get(i);
    for (int i = n - 2; i >= 0; i--)
        for (int j = 0; j <= i; j++)
            dp[j] = triangle.get(i).get(j) + Math.min(dp[j], dp[j+1]);
    return dp[0];
}
```

---

### 🔀 Interleaving String
*"Can s3 be formed by interleaving s1 and s2?"*

```java
public boolean isInterleave(String s1, String s2, String s3) {
    int m = s1.length(), n = s2.length();
    if (m + n != s3.length()) return false;
    boolean[][] dp = new boolean[m + 1][n + 1]; dp[0][0] = true;
    for (int i = 1; i <= m; i++) dp[i][0] = dp[i-1][0] && s1.charAt(i-1) == s3.charAt(i-1);
    for (int j = 1; j <= n; j++) dp[0][j] = dp[0][j-1] && s2.charAt(j-1) == s3.charAt(j-1);
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++)
            dp[i][j] = (dp[i-1][j] && s1.charAt(i-1) == s3.charAt(i+j-1))
                     || (dp[i][j-1] && s2.charAt(j-1) == s3.charAt(i+j-1));
    return dp[m][n];
}
```

---

### 🧗 Min Cost Climbing Stairs
*"Minimum cost to reach the top"*

```java
public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
    int a = cost[0], b = cost[1];
    for (int i = 2; i < n; i++) { int c = cost[i] + Math.min(a, b); a = b; b = c; }
    return Math.min(a, b);
}
```

---

### 📈 Longest Increasing Subsequence
*"Longest subsequence where numbers keep increasing"*

```java
public int lengthOfLIS(int[] nums) {
    int[] dp = new int[nums.length]; Arrays.fill(dp, 1);
    int max = 1;
    for (int i = 1; i < nums.length; i++) {
        for (int j = 0; j < i; j++)
            if (nums[j] < nums[i]) dp[i] = Math.max(dp[i], dp[j] + 1);
        max = Math.max(max, dp[i]);
    }
    return max;
}
```

---

### 🔤 Distinct Subsequences
*"How many ways to choose subsequence of t from s?"*

```java
public int numDistinct(String s, String t) {
    int m = s.length(), n = t.length();
    int[][] dp = new int[m+1][n+1];
    for (int i = 0; i <= m; i++) dp[i][0] = 1;
    for (int i = 1; i <= m; i++)
        for (int j = 1; j <= n; j++) {
            dp[i][j] = dp[i-1][j];
            if (s.charAt(i-1) == t.charAt(j-1)) dp[i][j] += dp[i-1][j-1];
        }
    return dp[m][n];
}
```

---

### 📊 Maximum Subarray (Kadane's Algorithm)
*"Largest sum from a contiguous subarray"*

```java
public int maxSubArray(int[] nums) {
    int max = nums[0], curr = nums[0];
    for (int i = 1; i < nums.length; i++) {
        curr = Math.max(nums[i], curr + nums[i]);
        max = Math.max(max, curr);
    }
    return max;
}
```

---

### 🏠 House Robber
*"Rob max without robbing adjacent houses"*

```java
public int rob(int[] nums) {
    int prev = 0, curr = 0;
    for (int n : nums) { int next = Math.max(curr, prev + n); prev = curr; curr = next; }
    return curr;
}
```

---

### 🗺️ Unique Paths
*"How many ways to reach bottom-right of a grid?"*

```java
public int uniquePaths(int m, int n) {
    int[] dp = new int[n]; Arrays.fill(dp, 1);
    for (int i = 1; i < m; i++)
        for (int j = 1; j < n; j++)
            dp[j] += dp[j - 1];
    return dp[n - 1];
}
```

---

# 🗺️ Chapter 13: Graphs
### *"The City Map"*

A graph is a city. Nodes are places, edges are roads. BFS explores layer by layer (shortest path). DFS dives deep (cycle detection, connectivity).

---

### 🔁 Clone Graph
*"Make a deep copy of the graph"*

```java
public Node cloneGraph(Node node) {
    if (node == null) return null;
    Map<Node, Node> map = new HashMap<>();
    return dfs(node, map);
}
private Node dfs(Node node, Map<Node, Node> map) {
    if (map.containsKey(node)) return map.get(node);
    Node clone = new Node(node.val);
    map.put(node, clone);
    for (Node neighbor : node.neighbors) clone.neighbors.add(dfs(neighbor, map));
    return clone;
}
```

---

### ⏱️ Network Delay Time
*"Shortest time for signal to reach all nodes (Dijkstra)"*

```java
public int networkDelayTime(int[][] times, int n, int k) {
    Map<Integer, List<int[]>> graph = new HashMap<>();
    for (int[] t : times) graph.computeIfAbsent(t[0], x -> new ArrayList<>()).add(new int[]{t[1], t[2]});
    PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]);
    pq.offer(new int[]{k, 0});
    int[] dist = new int[n + 1]; Arrays.fill(dist, Integer.MAX_VALUE); dist[k] = 0;
    while (!pq.isEmpty()) {
        int[] curr = pq.poll();
        int node = curr[0], d = curr[1];
        if (d > dist[node]) continue;
        for (int[] next : graph.getOrDefault(node, new ArrayList<>())) {
            if (dist[node] + next[1] < dist[next[0]]) {
                dist[next[0]] = dist[node] + next[1];
                pq.offer(new int[]{next[0], dist[next[0]]});
            }
        }
    }
    int max = 0;
    for (int i = 1; i <= n; i++) { if (dist[i] == Integer.MAX_VALUE) return -1; max = Math.max(max, dist[i]); }
    return max;
}
```

---

### 🎲 Path with Maximum Probability
*"Highest probability path between two nodes"*

Modified Dijkstra (maximize instead of minimize).

```java
public double maxProbability(int n, int[][] edges, double[] succProb, int start, int end) {
    Map<Integer, List<double[]>> graph = new HashMap<>();
    for (int i = 0; i < edges.length; i++) {
        graph.computeIfAbsent(edges[i][0], x -> new ArrayList<>()).add(new double[]{edges[i][1], succProb[i]});
        graph.computeIfAbsent(edges[i][1], x -> new ArrayList<>()).add(new double[]{edges[i][0], succProb[i]});
    }
    double[] prob = new double[n]; prob[start] = 1.0;
    PriorityQueue<double[]> pq = new PriorityQueue<>((a, b) -> Double.compare(b[1], a[1]));
    pq.offer(new double[]{start, 1.0});
    while (!pq.isEmpty()) {
        double[] curr = pq.poll(); int node = (int) curr[0]; double p = curr[1];
        if (node == end) return p;
        for (double[] next : graph.getOrDefault(node, new ArrayList<>())) {
            double newP = p * next[1];
            if (newP > prob[(int) next[0]]) { prob[(int) next[0]] = newP; pq.offer(new double[]{next[0], newP}); }
        }
    }
    return 0;
}
```

---

### 🏝️ Max Area of Island
*"Find the biggest connected island (DFS)"*

```java
public int maxAreaOfIsland(int[][] grid) {
    int max = 0;
    for (int i = 0; i < grid.length; i++)
        for (int j = 0; j < grid[0].length; j++)
            if (grid[i][j] == 1) max = Math.max(max, dfs(grid, i, j));
    return max;
}
private int dfs(int[][] grid, int i, int j) {
    if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] == 0) return 0;
    grid[i][j] = 0;
    return 1 + dfs(grid, i+1, j) + dfs(grid, i-1, j) + dfs(grid, i, j+1) + dfs(grid, i, j-1);
}
```

---

### 🏝️ Number of Islands
*"Count disconnected land masses"*

```java
public int numIslands(char[][] grid) {
    int count = 0;
    for (int i = 0; i < grid.length; i++)
        for (int j = 0; j < grid[0].length; j++)
            if (grid[i][j] == '1') { dfs(grid, i, j); count++; }
    return count;
}
private void dfs(char[][] grid, int i, int j) {
    if (i < 0 || i >= grid.length || j < 0 || j >= grid[0].length || grid[i][j] != '1') return;
    grid[i][j] = '0';
    dfs(grid, i+1, j); dfs(grid, i-1, j); dfs(grid, i, j+1); dfs(grid, i, j-1);
}
```

---

### 📚 Course Schedule
*"Can you finish all courses? (Cycle detection in directed graph)"*

```java
public boolean canFinish(int numCourses, int[][] prerequisites) {
    List<List<Integer>> graph = new ArrayList<>();
    for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
    for (int[] p : prerequisites) graph.get(p[1]).add(p[0]);
    int[] state = new int[numCourses]; // 0=unvisited, 1=visiting, 2=done
    for (int i = 0; i < numCourses; i++) if (hasCycle(graph, state, i)) return false;
    return true;
}
private boolean hasCycle(List<List<Integer>> graph, int[] state, int node) {
    if (state[node] == 1) return true;
    if (state[node] == 2) return false;
    state[node] = 1;
    for (int next : graph.get(node)) if (hasCycle(graph, state, next)) return true;
    state[node] = 2;
    return false;
}
```

---

### 📚 Course Schedule II
*"Topological sort: give a valid order to take courses"*

```java
public int[] findOrder(int numCourses, int[][] prerequisites) {
    List<List<Integer>> graph = new ArrayList<>();
    int[] inDegree = new int[numCourses];
    for (int i = 0; i < numCourses; i++) graph.add(new ArrayList<>());
    for (int[] p : prerequisites) { graph.get(p[1]).add(p[0]); inDegree[p[0]]++; }
    Queue<Integer> queue = new LinkedList<>();
    for (int i = 0; i < numCourses; i++) if (inDegree[i] == 0) queue.offer(i);
    int[] order = new int[numCourses]; int idx = 0;
    while (!queue.isEmpty()) {
        int node = queue.poll(); order[idx++] = node;
        for (int next : graph.get(node)) if (--inDegree[next] == 0) queue.offer(next);
    }
    return idx == numCourses ? order : new int[]{};
}
```

---

### 📖 Word Ladder
*"Minimum steps to transform one word to another, changing one letter at a time"*

BFS — each neighbor differs by exactly one character.

```java
public int ladderLength(String beginWord, String endWord, List<String> wordList) {
    Set<String> dict = new HashSet<>(wordList);
    Queue<String> queue = new LinkedList<>();
    queue.offer(beginWord); int steps = 1;
    while (!queue.isEmpty()) {
        int size = queue.size();
        while (size-- > 0) {
            String word = queue.poll();
            char[] chars = word.toCharArray();
            for (int i = 0; i < chars.length; i++) {
                char orig = chars[i];
                for (char c = 'a'; c <= 'z'; c++) {
                    chars[i] = c;
                    String next = new String(chars);
                    if (next.equals(endWord)) return steps + 1;
                    if (dict.remove(next)) queue.offer(next);
                }
                chars[i] = orig;
            }
        }
        steps++;
    }
    return 0;
}
```

---

### 🌊 Pacific Atlantic Water Flow
*"Which cells can flow to both oceans?"*

BFS from both oceans inward. Find the intersection.

```java
public List<List<Integer>> pacificAtlantic(int[][] heights) {
    int m = heights.length, n = heights[0].length;
    boolean[][] pac = new boolean[m][n], atl = new boolean[m][n];
    Queue<int[]> pq = new LinkedList<>(), aq = new LinkedList<>();
    for (int i = 0; i < m; i++) { pq.offer(new int[]{i, 0}); pac[i][0] = true; aq.offer(new int[]{i, n-1}); atl[i][n-1] = true; }
    for (int j = 0; j < n; j++) { pq.offer(new int[]{0, j}); pac[0][j] = true; aq.offer(new int[]{m-1, j}); atl[m-1][j] = true; }
    bfs(heights, pq, pac); bfs(heights, aq, atl);
    List<List<Integer>> result = new ArrayList<>();
    for (int i = 0; i < m; i++) for (int j = 0; j < n; j++) if (pac[i][j] && atl[i][j]) result.add(Arrays.asList(i, j));
    return result;
}
private void bfs(int[][] h, Queue<int[]> q, boolean[][] visited) {
    int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
    while (!q.isEmpty()) {
        int[] cell = q.poll();
        for (int[] d : dirs) {
            int ni = cell[0] + d[0], nj = cell[1] + d[1];
            if (ni >= 0 && ni < h.length && nj >= 0 && nj < h[0].length && !visited[ni][nj] && h[ni][nj] >= h[cell[0]][cell[1]]) {
                visited[ni][nj] = true; q.offer(new int[]{ni, nj});
            }
        }
    }
}
```

---

### 🍊 Rotting Oranges
*"How many minutes until all oranges rot? (Multi-source BFS)"*

```java
public int orangesRotting(int[][] grid) {
    Queue<int[]> queue = new LinkedList<>();
    int fresh = 0;
    for (int i = 0; i < grid.length; i++) for (int j = 0; j < grid[0].length; j++) {
        if (grid[i][j] == 2) queue.offer(new int[]{i, j});
        if (grid[i][j] == 1) fresh++;
    }
    int minutes = 0; int[][] dirs = {{1,0},{-1,0},{0,1},{0,-1}};
    while (!queue.isEmpty() && fresh > 0) {
        minutes++;
        int size = queue.size();
        while (size-- > 0) {
            int[] cell = queue.poll();
            for (int[] d : dirs) {
                int ni = cell[0]+d[0], nj = cell[1]+d[1];
                if (ni >= 0 && ni < grid.length && nj >= 0 && nj < grid[0].length && grid[ni][nj] == 1) {
                    grid[ni][nj] = 2; fresh--; queue.offer(new int[]{ni, nj});
                }
            }
        }
    }
    return fresh == 0 ? minutes : -1;
}
```

---

### 🌐 Number of Provinces
*"How many independent friend groups?"*

Union Find / DFS on adjacency matrix.

```java
public int findCircleNum(int[][] isConnected) {
    int n = isConnected.length; boolean[] visited = new boolean[n]; int provinces = 0;
    for (int i = 0; i < n; i++) if (!visited[i]) { dfs(isConnected, visited, i); provinces++; }
    return provinces;
}
private void dfs(int[][] g, boolean[] visited, int i) {
    visited[i] = true;
    for (int j = 0; j < g.length; j++) if (g[i][j] == 1 && !visited[j]) dfs(g, visited, j);
}
```

---

# 🌲 Chapter 14: Trees ⭐ VERY IMPORTANT
### *"The Family Tree"*

Trees are hierarchical. The root is the ancestor. DFS digs deep (pre/in/post-order). BFS visits level by level.

---

## 🔍 DFS on Trees

### 👴 Lowest Common Ancestor
*"Who is the closest common grandparent of two nodes?"*

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    return left != null && right != null ? root : (left != null ? left : right);
}
```

---

### ✅ Validate BST
*"Is every left child smaller and every right child bigger?"*

```java
public boolean isValidBST(TreeNode root) { return validate(root, Long.MIN_VALUE, Long.MAX_VALUE); }
private boolean validate(TreeNode node, long min, long max) {
    if (node == null) return true;
    if (node.val <= min || node.val >= max) return false;
    return validate(node.left, min, node.val) && validate(node.right, node.val, max);
}
```

---

### 📏 Maximum Depth
*"How tall is the tree?"*

```java
public int maxDepth(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
}
```

---

### 🔢 Kth Smallest in BST
*"In-order traversal gives sorted order!"*

```java
int count, result;
public int kthSmallest(TreeNode root, int k) {
    count = k; inorder(root); return result;
}
private void inorder(TreeNode node) {
    if (node == null) return;
    inorder(node.left);
    if (--count == 0) result = node.val;
    inorder(node.right);
}
```

---

### 📐 Diameter of Binary Tree
*"Longest path between any two nodes"*

```java
int diameter = 0;
public int diameterOfBinaryTree(TreeNode root) { height(root); return diameter; }
private int height(TreeNode node) {
    if (node == null) return 0;
    int l = height(node.left), r = height(node.right);
    diameter = Math.max(diameter, l + r);
    return 1 + Math.max(l, r);
}
```

---

### 👀 Binary Tree Right Side View
*"What do you see looking from the right?"*

BFS, take the last node at each level.

```java
public List<Integer> rightSideView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>(); queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size(); TreeNode last = null;
        while (size-- > 0) {
            last = queue.poll();
            if (last.left != null) queue.offer(last.left);
            if (last.right != null) queue.offer(last.right);
        }
        result.add(last.val);
    }
    return result;
}
```

---

### ➕ Path Sum
*"Does any root-to-leaf path sum to target?"*

```java
public boolean hasPathSum(TreeNode root, int targetSum) {
    if (root == null) return false;
    if (root.left == null && root.right == null) return root.val == targetSum;
    return hasPathSum(root.left, targetSum - root.val) || hasPathSum(root.right, targetSum - root.val);
}
```

---

### 🔐 Serialize and Deserialize Binary Tree
*"Convert tree to string and back"*

```java
public String serialize(TreeNode root) {
    if (root == null) return "null,";
    return root.val + "," + serialize(root.left) + serialize(root.right);
}
int idx = 0;
public TreeNode deserialize(String data) {
    String[] nodes = data.split(","); return build(nodes);
}
private TreeNode build(String[] nodes) {
    if (nodes[idx].equals("null")) { idx++; return null; }
    TreeNode node = new TreeNode(Integer.parseInt(nodes[idx++]));
    node.left = build(nodes); node.right = build(nodes);
    return node;
}
```

---

## 🌊 BFS on Trees

### 📊 Level Order Traversal
*"Visit the tree floor by floor"*

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>(); queue.offer(root);
    while (!queue.isEmpty()) {
        int size = queue.size(); List<Integer> level = new ArrayList<>();
        while (size-- > 0) {
            TreeNode node = queue.poll(); level.add(node.val);
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        result.add(level);
    }
    return result;
}
```

---

### 🔀 Zigzag Traversal
*"Alternate left-to-right and right-to-left at each level"*

```java
public List<List<Integer>> zigzagLevelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;
    Queue<TreeNode> queue = new LinkedList<>(); queue.offer(root); boolean leftToRight = true;
    while (!queue.isEmpty()) {
        int size = queue.size(); LinkedList<Integer> level = new LinkedList<>();
        while (size-- > 0) {
            TreeNode node = queue.poll();
            if (leftToRight) level.addLast(node.val); else level.addFirst(node.val);
            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }
        result.add(level); leftToRight = !leftToRight;
    }
    return result;
}
```

---

### 🪞 Symmetric Tree
*"Is the tree a mirror of itself?"*

```java
public boolean isSymmetric(TreeNode root) { return isMirror(root.left, root.right); }
private boolean isMirror(TreeNode l, TreeNode r) {
    if (l == null && r == null) return true;
    if (l == null || r == null) return false;
    return l.val == r.val && isMirror(l.left, r.right) && isMirror(l.right, r.left);
}
```

---

# 📚 Chapter 15: Stack
### *"The Pancake Stack"*

A stack is a pile of pancakes. You can only add or remove from the top. LIFO — Last In, First Out!

---

### ✅ Valid Parentheses
*"Every open bracket must be closed in the right order"*

```java
public boolean isValid(String s) {
    Deque<Character> stack = new ArrayDeque<>();
    for (char c : s.toCharArray()) {
        if (c == '(' || c == '[' || c == '{') stack.push(c);
        else {
            if (stack.isEmpty()) return false;
            char top = stack.pop();
            if (c == ')' && top != '(') return false;
            if (c == ']' && top != '[') return false;
            if (c == '}' && top != '{') return false;
        }
    }
    return stack.isEmpty();
}
```

---

### 🔤 Decode String
*"Expand 3[abc] to abcabcabc"*

```java
public String decodeString(String s) {
    Deque<Integer> counts = new ArrayDeque<>();
    Deque<StringBuilder> strings = new ArrayDeque<>();
    StringBuilder curr = new StringBuilder(); int k = 0;
    for (char c : s.toCharArray()) {
        if (Character.isDigit(c)) k = k * 10 + (c - '0');
        else if (c == '[') { counts.push(k); strings.push(curr); curr = new StringBuilder(); k = 0; }
        else if (c == ']') {
            int times = counts.pop(); StringBuilder prev = strings.pop();
            String repeated = curr.toString().repeat(times);
            curr = prev.append(repeated);
        } else curr.append(c);
    }
    return curr.toString();
}
```

---

### 🌡️ Daily Temperatures
*"How many days until a warmer temperature?"*

Monotonic decreasing stack of indices.

```java
public int[] dailyTemperatures(int[] temps) {
    int[] result = new int[temps.length];
    Deque<Integer> stack = new ArrayDeque<>();
    for (int i = 0; i < temps.length; i++) {
        while (!stack.isEmpty() && temps[i] > temps[stack.peek()]) {
            int idx = stack.pop(); result[idx] = i - idx;
        }
        stack.push(i);
    }
    return result;
}
```

---

### 🔢 Basic Calculator
*"Evaluate a math expression with +, -, and parentheses"*

```java
public int calculate(String s) {
    Deque<Integer> stack = new ArrayDeque<>();
    int result = 0, sign = 1, num = 0;
    for (char c : s.toCharArray()) {
        if (Character.isDigit(c)) num = num * 10 + (c - '0');
        else if (c == '+') { result += sign * num; num = 0; sign = 1; }
        else if (c == '-') { result += sign * num; num = 0; sign = -1; }
        else if (c == '(') { stack.push(result); stack.push(sign); result = 0; sign = 1; }
        else if (c == ')') { result += sign * num; num = 0; result *= stack.pop(); result += stack.pop(); }
    }
    return result + sign * num;
}
```

---

### ✅ Longest Valid Parentheses
*"Longest substring of valid brackets"*

```java
public int longestValidParentheses(String s) {
    Deque<Integer> stack = new ArrayDeque<>(); stack.push(-1);
    int max = 0;
    for (int i = 0; i < s.length(); i++) {
        if (s.charAt(i) == '(') stack.push(i);
        else {
            stack.pop();
            if (stack.isEmpty()) stack.push(i);
            else max = Math.max(max, i - stack.peek());
        }
    }
    return max;
}
```

---

### 📊 Largest Rectangle in Histogram
*"Find the largest rectangle fitting within the histogram"*

```java
public int largestRectangleArea(int[] heights) {
    Deque<Integer> stack = new ArrayDeque<>();
    int max = 0, n = heights.length;
    for (int i = 0; i <= n; i++) {
        int h = i == n ? 0 : heights[i];
        while (!stack.isEmpty() && h < heights[stack.peek()]) {
            int height = heights[stack.pop()];
            int width = stack.isEmpty() ? i : i - stack.peek() - 1;
            max = Math.max(max, height * width);
        }
        stack.push(i);
    }
    return max;
}
```

---

### ☄️ Asteroid Collision
*"Asteroids moving left/right collide. What survives?"*

```java
public int[] asteroidCollision(int[] asteroids) {
    Deque<Integer> stack = new ArrayDeque<>();
    for (int a : asteroids) {
        boolean destroyed = false;
        while (!stack.isEmpty() && a < 0 && stack.peek() > 0) {
            if (stack.peek() < -a) { stack.pop(); continue; }
            if (stack.peek() == -a) stack.pop();
            destroyed = true; break;
        }
        if (!destroyed) stack.push(a);
    }
    return stack.stream().mapToInt(Integer::intValue).toArray();
}
```

---

### 🔢 Evaluate Reverse Polish Notation
*"Calculate 2 3 + = 5 (postfix notation)"*

```java
public int evalRPN(String[] tokens) {
    Deque<Integer> stack = new ArrayDeque<>();
    for (String t : tokens) {
        if ("+-*/".contains(t)) {
            int b = stack.pop(), a = stack.pop();
            switch (t) {
                case "+": stack.push(a + b); break;
                case "-": stack.push(a - b); break;
                case "*": stack.push(a * b); break;
                case "/": stack.push(a / b); break;
            }
        } else stack.push(Integer.parseInt(t));
    }
    return stack.pop();
}
```

---

# 🌳 Chapter 16: Trie
### *"The Word Tree"*

A Trie is a tree where each path from root to leaf spells a word. Perfect for prefix lookups and autocomplete!

---

### 📖 Implement Trie
*"Build the word tree"*

```java
class Trie {
    private Trie[] children = new Trie[26];
    private boolean isEnd = false;
    public void insert(String word) {
        Trie node = this;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (node.children[idx] == null) node.children[idx] = new Trie();
            node = node.children[idx];
        }
        node.isEnd = true;
    }
    public boolean search(String word) {
        Trie node = this;
        for (char c : word.toCharArray()) {
            int idx = c - 'a';
            if (node.children[idx] == null) return false;
            node = node.children[idx];
        }
        return node.isEnd;
    }
    public boolean startsWith(String prefix) {
        Trie node = this;
        for (char c : prefix.toCharArray()) {
            int idx = c - 'a';
            if (node.children[idx] == null) return false;
            node = node.children[idx];
        }
        return true;
    }
}
```

---

### 🔍 Word Search II
*"Find all dictionary words in the grid"*

Build Trie from words, then DFS the grid.

```java
public List<String> findWords(char[][] board, String[] words) {
    Trie root = new Trie();
    for (String w : words) root.insert(w);
    Set<String> result = new HashSet<>();
    for (int i = 0; i < board.length; i++)
        for (int j = 0; j < board[0].length; j++)
            dfs(board, i, j, root, new StringBuilder(), result);
    return new ArrayList<>(result);
}
private void dfs(char[][] board, int i, int j, Trie node, StringBuilder path, Set<String> result) {
    if (i < 0 || i >= board.length || j < 0 || j >= board[0].length || board[i][j] == '#') return;
    char c = board[i][j];
    Trie next = node.children[c - 'a'];
    if (next == null) return;
    path.append(c); board[i][j] = '#';
    if (next.isEnd) result.add(path.toString());
    dfs(board, i+1, j, next, path, result); dfs(board, i-1, j, next, path, result);
    dfs(board, i, j+1, next, path, result); dfs(board, i, j-1, next, path, result);
    path.deleteCharAt(path.length() - 1); board[i][j] = c;
}
```

---

### 💡 Search Suggestions System
*"Autocomplete: show top 3 suggestions as you type"*

Insert all products in Trie. For each prefix, collect up to 3 matches.

```java
public List<List<String>> suggestedProducts(String[] products, String searchWord) {
    Arrays.sort(products);
    List<List<String>> result = new ArrayList<>();
    String prefix = "";
    for (char c : searchWord.toCharArray()) {
        prefix += c;
        List<String> suggestions = new ArrayList<>();
        for (String p : products) {
            if (p.startsWith(prefix)) { suggestions.add(p); if (suggestions.size() == 3) break; }
        }
        result.add(suggestions);
    }
    return result;
}
```

---

# 🔗 Chapter 17: Union Find
### *"The Social Network"*

Union-Find tracks which people are in the same group. Find: who's your leader? Union: merge two groups!

---

### 🏝️ Number of Islands (Union Find approach)
*"Count disconnected components"*

```java
class UnionFind {
    int[] parent, rank; int count;
    UnionFind(int n) { parent = new int[n]; rank = new int[n]; count = n; for (int i = 0; i < n; i++) parent[i] = i; }
    int find(int x) { if (parent[x] != x) parent[x] = find(parent[x]); return parent[x]; }
    void union(int x, int y) {
        int px = find(x), py = find(y); if (px == py) return;
        if (rank[px] < rank[py]) { int t = px; px = py; py = t; }
        parent[py] = px; if (rank[px] == rank[py]) rank[px]++;
        count--;
    }
}
```

---

### 🔁 Redundant Connection
*"Which edge creates a cycle? (Remove it!)"*

```java
public int[] findRedundantConnection(int[][] edges) {
    int n = edges.length;
    int[] parent = new int[n + 1]; for (int i = 0; i <= n; i++) parent[i] = i;
    for (int[] e : edges) {
        int px = find(parent, e[0]), py = find(parent, e[1]);
        if (px == py) return e;
        parent[px] = py;
    }
    return new int[]{};
}
private int find(int[] parent, int x) { if (parent[x] != x) parent[x] = find(parent, parent[x]); return parent[x]; }
```

---

### 👥 Accounts Merge
*"Merge accounts that share an email"*

Union all emails by account. Group them under their leader.

```java
public List<List<String>> accountsMerge(List<List<String>> accounts) {
    Map<String, String> parent = new HashMap<>(), emailToName = new HashMap<>();
    for (List<String> acc : accounts) {
        String name = acc.get(0);
        for (int i = 1; i < acc.size(); i++) {
            parent.putIfAbsent(acc.get(i), acc.get(i));
            emailToName.put(acc.get(i), name);
            union(parent, acc.get(1), acc.get(i));
        }
    }
    Map<String, TreeSet<String>> groups = new HashMap<>();
    for (String email : parent.keySet()) groups.computeIfAbsent(find(parent, email), k -> new TreeSet<>()).add(email);
    List<List<String>> result = new ArrayList<>();
    for (Map.Entry<String, TreeSet<String>> e : groups.entrySet()) {
        List<String> list = new ArrayList<>(); list.add(emailToName.get(e.getKey())); list.addAll(e.getValue()); result.add(list);
    }
    return result;
}
private String find(Map<String, String> parent, String x) { if (!parent.get(x).equals(x)) parent.put(x, find(parent, parent.get(x))); return parent.get(x); }
private void union(Map<String, String> parent, String x, String y) { parent.put(find(parent, x), find(parent, y)); }
```

---

### 📏 Longest Consecutive Sequence
*"Find the longest streak of consecutive numbers"*

```java
public int longestConsecutive(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int n : nums) set.add(n);
    int max = 0;
    for (int n : set) {
        if (!set.contains(n - 1)) { // start of a new sequence
            int curr = n, len = 1;
            while (set.contains(curr + 1)) { curr++; len++; }
            max = Math.max(max, len);
        }
    }
    return max;
}
```

---

# 🏗️ Chapter 18: Design / LLD-style Coding
### *"Build Your Own Tools"*

These problems teach you to design data structures from scratch — like building your own Swiss Army Knife!

---

### 🗄️ LRU Cache
*"The magic box that evicts the least recently used item"*

Use a doubly linked list + HashMap. O(1) get and put.

```java
class LRUCache {
    private final int capacity;
    private final Map<Integer, Node> map = new HashMap<>();
    private final Node head = new Node(0, 0), tail = new Node(0, 0);
    public LRUCache(int capacity) { this.capacity = capacity; head.next = tail; tail.prev = head; }
    public int get(int key) {
        if (!map.containsKey(key)) return -1;
        Node node = map.get(key); move(node); return node.val;
    }
    public void put(int key, int value) {
        if (map.containsKey(key)) { map.get(key).val = value; move(map.get(key)); return; }
        if (map.size() == capacity) { map.remove(tail.prev.key); remove(tail.prev); }
        Node node = new Node(key, value); map.put(key, node); insert(node);
    }
    private void move(Node n) { remove(n); insert(n); }
    private void remove(Node n) { n.prev.next = n.next; n.next.prev = n.prev; }
    private void insert(Node n) { n.next = head.next; n.prev = head; head.next.prev = n; head.next = n; }
    class Node { int key, val; Node prev, next; Node(int k, int v) { key = k; val = v; } }
}
```

---

### ⏰ Time-Based Key-Value Store
*"Store value with timestamp, retrieve the latest value at or before T"*

```java
class TimeMap {
    Map<String, List<int[]>> map = new HashMap<>();
    public void set(String key, String value, int timestamp) {
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(new int[]{timestamp, value.hashCode()});
    }
    // (simplified) Full version stores strings, uses binary search
}
```

---

### 🎲 Insert Delete GetRandom O(1)
*"A set with constant-time random access"*

ArrayList for random + HashMap for O(1) remove.

```java
class RandomizedSet {
    Map<Integer, Integer> map = new HashMap<>(); List<Integer> list = new ArrayList<>();
    Random rand = new Random();
    public boolean insert(int val) {
        if (map.containsKey(val)) return false;
        map.put(val, list.size()); list.add(val); return true;
    }
    public boolean remove(int val) {
        if (!map.containsKey(val)) return false;
        int idx = map.get(val), last = list.get(list.size() - 1);
        list.set(idx, last); map.put(last, idx); list.remove(list.size() - 1); map.remove(val); return true;
    }
    public int getRandom() { return list.get(rand.nextInt(list.size())); }
}
```

---

### 📦 Min Stack
*"A stack that also knows its minimum at any time"*

```java
class MinStack {
    Deque<int[]> stack = new ArrayDeque<>(); // [val, currentMin]
    public void push(int val) { stack.push(new int[]{val, stack.isEmpty() ? val : Math.min(val, stack.peek()[1])}); }
    public void pop() { stack.pop(); }
    public int top() { return stack.peek()[0]; }
    public int getMin() { return stack.peek()[1]; }
}
```

---

### 🔁 LFU Cache *(Understand the pattern)*
*"Evict least frequently used item. Ties broken by least recently used."*

Use a min-frequency tracker + frequency-to-doubly-linked-list map.

```java
// Key insight: maintain a map of freq -> LRU list of keys at that freq
// On access/update: increment freq, move node to freq+1 list
// On eviction: remove LRU node from minFreq's list
// Full implementation is ~60 lines — understand the 3 maps pattern:
// key->val, key->freq, freq->LinkedHashSet<key>
```

---

# 🗺️ Chapter 19: Hashing
### *"The Magic Dictionary"*

A HashMap lets you look up any value in O(1)! It's the secret weapon behind dozens of interview problems.

---

### 🔤 Group Anagrams
*"Sort each word's letters — anagrams become identical keys"*

```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();
    for (String s : strs) {
        char[] chars = s.toCharArray(); Arrays.sort(chars);
        map.computeIfAbsent(new String(chars), k -> new ArrayList<>()).add(s);
    }
    return new ArrayList<>(map.values());
}
```

---

### ➕ Continuous Subarray Sum
*"Is there a subarray of size ≥ 2 whose sum is a multiple of k?"*

Prefix sum mod k. If same remainder seen before (with gap ≥ 2), we found it.

```java
public boolean checkSubarraySum(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>(); map.put(0, -1);
    int sum = 0;
    for (int i = 0; i < nums.length; i++) {
        sum = (sum + nums[i]) % k;
        if (map.containsKey(sum)) { if (i - map.get(sum) >= 2) return true; }
        else map.put(sum, i);
    }
    return false;
}
```

---

### 🔢 Valid Sudoku
*"Check if the board is valid"*

Track rows, columns, and 3x3 boxes.

```java
public boolean isValidSudoku(char[][] board) {
    Set<String> seen = new HashSet<>();
    for (int i = 0; i < 9; i++) for (int j = 0; j < 9; j++) {
        char c = board[i][j]; if (c == '.') continue;
        String row = "r" + i + c, col = "c" + j + c, box = "b" + (i/3) + (j/3) + c;
        if (!seen.add(row) || !seen.add(col) || !seen.add(box)) return false;
    }
    return true;
}
```

---

### 🔄 Contiguous Array
*"Longest subarray with equal 0s and 1s"*

Replace 0 with -1. Find longest subarray summing to 0 (prefix sum trick).

```java
public int findMaxLength(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>(); map.put(0, -1);
    int sum = 0, max = 0;
    for (int i = 0; i < nums.length; i++) {
        sum += nums[i] == 0 ? -1 : 1;
        if (map.containsKey(sum)) max = Math.max(max, i - map.get(sum));
        else map.put(sum, i);
    }
    return max;
}
```

---

### 🏛️ Roman to Integer
*"Convert Roman numerals to numbers"*

If a smaller value appears before a larger one, subtract it.

```java
public int romanToInt(String s) {
    Map<Character, Integer> map = Map.of('I', 1, 'V', 5, 'X', 10, 'L', 50, 'C', 100, 'D', 500, 'M', 1000);
    int result = 0;
    for (int i = 0; i < s.length(); i++) {
        int curr = map.get(s.charAt(i));
        int next = i + 1 < s.length() ? map.get(s.charAt(i + 1)) : 0;
        result += curr < next ? -curr : curr;
    }
    return result;
}
```

---

### ➕ Two Sum
*"Find two numbers that add up to target"*

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int comp = target - nums[i];
        if (map.containsKey(comp)) return new int[]{map.get(comp), i};
        map.put(nums[i], i);
    }
    return new int[]{};
}
```

---

### 🔍 Contains Duplicate
*"Does any number appear more than once?"*

```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int n : nums) if (!set.add(n)) return true;
    return false;
}
```

---

### ✖️ Product of Array Except Self
*"For each position, multiply all other elements (no division!)"*

Left pass then right pass.

```java
public int[] productExceptSelf(int[] nums) {
    int n = nums.length; int[] result = new int[n]; result[0] = 1;
    for (int i = 1; i < n; i++) result[i] = result[i-1] * nums[i-1];
    int right = 1;
    for (int i = n - 1; i >= 0; i--) { result[i] *= right; right *= nums[i]; }
    return result;
}
```

---

## 🎓 The End — You Made It!

> You've now traveled through **19 kingdoms** of DSA, from the Two Pointer Palace to the Hashing Bazaar. Each problem is a puzzle, and now you have the story behind every trick. Code it, break it, fix it — and soon you'll solve them without even thinking!

### 🗺️ Quick Reference Map

| Chapter | Topic | Importance |
|---|---|---|
| 1 | Two Pointers | ⭐⭐⭐ |
| 2 | Fast & Slow Pointers | ⭐⭐⭐ |
| 3 | Sliding Window | ⭐⭐⭐⭐⭐ |
| 4 | Intervals | ⭐⭐⭐ |
| 5 | Linked List In-place | ⭐⭐⭐ |
| 6 | Heaps / Priority Queue | ⭐⭐⭐⭐ |
| 7 | K-way Merge | ⭐⭐⭐ |
| 8 | Top K Elements | ⭐⭐⭐ |
| 9 | Binary Search | ⭐⭐⭐⭐⭐ |
| 10 | Backtracking | ⭐⭐⭐⭐ |
| 11 | Greedy | ⭐⭐⭐ |
| 12 | Dynamic Programming | ⭐⭐⭐⭐⭐ |
| 13 | Graphs | ⭐⭐⭐⭐ |
| 14 | Trees | ⭐⭐⭐⭐⭐ |
| 15 | Stack | ⭐⭐⭐⭐ |
| 16 | Trie | ⭐⭐⭐ |
| 17 | Union Find | ⭐⭐⭐ |
| 18 | Design / LLD | ⭐⭐⭐⭐ |
| 19 | Hashing | ⭐⭐⭐⭐ |
