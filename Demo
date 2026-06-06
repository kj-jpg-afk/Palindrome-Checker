#include "palindrome.h"
#include <iostream>
#include <chrono>
#include <string>

std::string makeRandomString(int length) {
    std::string result(length, ' ');
    unsigned int x = (unsigned int)length;
    for (int i = 0; i < length; i++) {
        x = x * 1664525u + 1013904223u; // lcg constants
        result[i] = 'a' + (x >> 30) % 3; // alphabet size 3: a, b, c
    }
    return result;
}

int main() {
    std::cout << "=== Longest Palindromic Substring Demo ===" << std::endl;
    std::cout << std::endl;

    std::string examples[] = {
        "babad",
        "cbbd",
        "racecar",
        "forgeeksskeegfor",
        "abcba",
        "a",
        "",
        "aaaa",
        "abacaba",
        "xyzabcddcbadef"
    };

    for (const std::string& input : examples) {
        std::string result = longestPalindrome(input);
        std::cout << "input:  \"" << input << "\"" << std::endl;
        std::cout << "output: \"" << result << "\"" << std::endl;
        std::cout << std::endl;
    }

    std::cout << "=== Timing Benchmark ===" << std::endl;
    std::cout << std::endl;

    int sizes[] = {1000, 2000, 5000, 10000};

    for (int n : sizes) {
        std::string s = makeRandomString(n);

        auto start = std::chrono::high_resolution_clock::now();
        std::string result = longestPalindrome(s);
        auto end = std::chrono::high_resolution_clock::now();

        double ms = std::chrono::duration<double, std::milli>(end - start).count();

        std::cout << "n = " << n
                  << "  |  time = " << ms << " ms"
                  << "  |  longest palindrome length = " << result.size()
                  << std::endl;
    }

    return 0;
}
