#include "palindrome.h"

// two pointer palindrome check
bool isPalindrome(const std::string& s, int left, int right) {
    while (left < right) {
        if (s[left] != s[right]) {
            return false;
        }
        left++;
        right--;
    }
    return true;
}


std::string longestPalindrome(const std::string& s) {
    if (s.empty()) return "";

    int bestStart = 0;
    int bestLength = 1; 

    for (int centre = 0; centre < (int)s.size(); centre++) {

        // e.g. "racecar" -> centre is the 'e', expands to the full string
        int left = centre;
        int right = centre;
        while (left > 0 && right < (int)s.size() - 1 && s[left - 1] == s[right + 1]) {
            left--;
            right++;
        }
        if (isPalindrome(s, left, right)) {
            int length = right - left + 1;
            if (length > bestLength) {
                bestLength = length;
                bestStart = left;
            }
        }

        if (centre + 1 < (int)s.size() && s[centre] == s[centre + 1]) {
            left = centre;
            right = centre + 1;
            while (left > 0 && right < (int)s.size() - 1 && s[left - 1] == s[right + 1]) {
                left--;
                right++;
            }
            if (isPalindrome(s, left, right)) {
                int length = right - left + 1;
                if (length > bestLength) {
                    bestLength = length;
                    bestStart = left;
                }
            }
        }
    }

    return s.substr(bestStart, bestLength);
}
