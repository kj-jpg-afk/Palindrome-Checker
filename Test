#include "palindrome.h"
#include <cassert>
#include <iostream>
#include <string>

bool checkIsPalindrome(const std::string& s) {
    int left = 0;
    int right = (int)s.size() - 1;
    while (left < right) {
        if (s[left] != s[right]) return false;
        left++;
        right--;
    }
    return true;
}

std::string bruteForce(const std::string& s) {
    int n = (int)s.size();
    if (n == 0) return "";
    int bestStart = 0;
    int bestLen = 1;
    for (int i = 0; i < n; i++) {
        for (int j = i; j < n; j++) {
            std::string sub = s.substr(i, j - i + 1);
            if (checkIsPalindrome(sub) && (int)sub.size() > bestLen) {
                bestLen = (int)sub.size();
                bestStart = i;
            }
        }
    }
    return s.substr(bestStart, bestLen);
}

std::string makeString(int length, int seed) {
    std::string s(length, ' ');
    for (int i = 0; i < length; i++) {
        s[i] = 'a' + (i * seed + length) % 4;
    }
    return s;
}

void testEdgeCases() {
    std::cout << "running edge case tests..." << std::endl;

    assert(longestPalindrome("") == "");

    assert(longestPalindrome("a") == "a");
    assert(longestPalindrome("z") == "z");

    std::string r = longestPalindrome("aa");
    assert(r == "aa");

    r = longestPalindrome("ab");
    assert(r.size() == 1);
    assert(checkIsPalindrome(r));

    r = longestPalindrome("aaaa");
    assert(r == "aaaa");

    r = longestPalindrome("aaaaa");
    assert(r == "aaaaa");

    r = longestPalindrome("racecar");
    assert(r == "racecar");

    r = longestPalindrome("abba");
    assert(r == "abba");

    std::cout << "edge case tests passed" << std::endl;
}

void testNormalCases() {
    std::cout << "running normal case tests..." << std::endl;

    std::string r = longestPalindrome("babad");
    assert(r.size() == 3);
    assert(checkIsPalindrome(r));

    r = longestPalindrome("cbbd");
    assert(r == "bb");

    r = longestPalindrome("abbaXY");
    assert(r == "abba");

    r = longestPalindrome("XYracecar");
    assert(r == "racecar");

    r = longestPalindrome("forgeeksskeegfor");
    assert(r == "geeksskeeg");
    assert(r.size() == 10);

    r = longestPalindrome("abacaba");
    assert(r == "abacaba");

    r = longestPalindrome("xyzabcddcbadef");
    assert(r == "abcddcba");
    assert(r.size() == 8);

    r = longestPalindrome("1221");
    assert(r == "1221");

    std::string inputs[] = {"aacabdkacaa", "abcba", "aaabaaaa", "xyzyx", "noon"};
    for (const std::string& input : inputs) {
        r = longestPalindrome(input);
        assert(checkIsPalindrome(r));
        assert(input.find(r) != std::string::npos);
    }

    std::cout << "normal case tests passed" << std::endl;
}

void testIsPalindrome() {
    std::cout << "running isPalindrome tests..." << std::endl;

    std::string s = "racecar";
    assert(isPalindrome(s, 0, 6) == true);
    assert(isPalindrome(s, 0, 5) == false);
    assert(isPalindrome(s, 3, 3) == true); 

    std::string t = "abacaba";
    assert(isPalindrome(t, 0, 6) == true);
    assert(isPalindrome(t, 2, 4) == true);  
    assert(isPalindrome(t, 0, 3) == false);

    std::string u = "abba";
    assert(isPalindrome(u, 0, 3) == true);
    assert(isPalindrome(u, 1, 2) == true);  
    assert(isPalindrome(u, 0, 2) == false);

    std::cout << "isPalindrome tests passed" << std::endl;
}

void testStress() {
    std::cout << "running stress tests (2000 random strings, comparing vs brute force)..." << std::endl;

    int passed = 0;
    for (int seed = 1; seed <= 100; seed++) {
        for (int len = 0; len <= 20; len++) {
            std::string s = makeString(len, seed);
            std::string fast = longestPalindrome(s);
            std::string ref  = bruteForce(s);

            assert(fast.size() == ref.size());
            assert(checkIsPalindrome(fast));

            if (!fast.empty()) {
                assert(s.find(fast) != std::string::npos);
            }
            passed++;
        }
    }

    std::cout << "stress tests passed (" << passed << " cases)" << std::endl;

    std::cout << "checking large inputs (n = 1000, 5000, 10000)..." << std::endl;
    for (int n : {1000, 5000, 10000}) {
        std::string s = makeString(n, 3);
        std::string r = longestPalindrome(s);
        assert(checkIsPalindrome(r));
        assert(!r.empty());
        assert(s.find(r) != std::string::npos);
        std::cout << "  n = " << n << "  longest = " << r.size() << " chars  OK" << std::endl;
    }
}

int main() {
    std::cout << "===============================" << std::endl;
    std::cout << " Palindrome Tests" << std::endl;
    std::cout << "===============================" << std::endl;
    std::cout << std::endl;

    testEdgeCases();
    testIsPalindrome();
    testNormalCases();
    testStress();

    std::cout << std::endl;
    std::cout << "all tests passed" << std::endl;

    return 0;
}
