# Palindrome-Checker, FEE3/150531/2025

1. Problem Statement
Given a string s of length n, find the longest contiguous substring that reads the same forwards and backwards (a palindrome). For example, in "forgeeksskeegfor" the answer is "geeksskeeg" (length 10). The solution must handle edge cases such as the empty string, single characters, and strings whose entire content is a palindrome.

2. Chosen Data Structures and Algorithm:
The input is stored as a std::string. The algorithm used is the Expand-Around-Centre algorithm. This works because a palindrome must have a centre: either a single character (odd length) or the gap between two identical adjacent characters (even length). For a string of length n there are exactly 2n − 1 such centres. For each centre, the algorithm expands outward character by character while the left and right characters match. The palindrome found at each centre has maximal length for that centre.

    •  expandAroundCentre(s, left, right)  expands while left ≥ 0, right < n, and s[left] == s[right]. It returns the total length of the palindrome found (right − left − 1 after the loop exits).
    
    •  longestPalindrome() iterates over all n centres for odd-length palindromes and all n − 1 centres for even-length palindromes (handled by passing centre, centre+1 as the initial right pointer). It keeps running maximums and recovers the start index from the length at the end.
    
    •  longestPalindromeRange() returns the half-open interval [start, end) so callers can extract or annotate the substring without copying.

3. Complexity Analysis
Time Complexity:
Let n = |s|.
Outer loop:  The algorithm iterates over all 2n − 1 centres once, giving Θ(n) iterations.
Inner expansion:  For centre i, expandAroundCentre performs at most min(i, n−1−i) + 1 character comparisons in each direction, i.e., at most ⌊n/2⌋ + 1 steps.

Worst case — all characters identical (e.g., "aaaa…a"):
T(n) = Σ_{i=0}^{n-1} 2·min(i, n-1-i) + (n-1)  ≈  n²/2  →  O(n²)

Best case — all characters distinct (e.g., "abcdef…"):
T(n) = Σ_{i=0}^{n-1} 1 = n  →  Ω(n)

Tight bound:  In the worst case the algorithm examines O(n²) character pairs, so the time complexity is O(n²). Because there exist inputs (all-same characters) that force Θ(n²) work, the tight Θ bound for the worst case is Θ(n²). For random strings over a large alphabet the expected number of comparisons is Θ(n log n), but the O(n²) worst-case guarantee is what matters here.

Space Complexity:
Beyond the input string itself, the algorithm uses only a fixed number of integer variables (bestStart, bestLen, left, right, oddLen, evenLen). The output is a substring copy of length at most n, which the caller may or may not create. Ignoring output:
Space = O(1) auxiliary

4. Empirical Timing Measurements
All timings were measured using std::chrono::high_resolution_clock. The test inputs are pseudo-random strings over the 5-character alphabet {a, b, c, d, e}

Results and observation: Going from n = 1 000 to n = 10 000 (10× increase) raises elapsed time from 0.008 ms to 0.076 ms — approximately a 9.5× increase. Hence O(n²) complexity\\\\\\\\

