# 1brc-simd
Process 1 billion row of text data as fast as possible

https://www.morling.dev/blog/one-billion-row-challenge/

-----------
# Test result on a shared server with AMD 2950x at 2.2 GHz:
- 32 threads, input assumption:
Runtime inside main = 683.349ms
real 0m0.847s
user 0m17.386s
sys 0m1.009s

- 32 threads, no input assumption:
Runtime inside main = 712.453ms
real    0m0.912s
user    0m20.750s
sys     0m0.664s

Use sha256sum to check that output is same as reference output
016930801788eb421a15cf6def8ea435b4b47fb5f41df09e02ecdd7fbc9ac92b  result.txt

I used this file (generated by `./create_measurements.sh 1000000000`) to test:
https://drive.google.com/file/d/1HEyNw4M453n0tnuaAm9nwaCiLydQYnpo/view?usp=sharing

To run, just download the file above, extract, then `./run_cpp.sh`

--------------
# Main indeas:
+ Unsigned int overflow hashing
+ SIMD hashing
+ SIMD for string comparison in hash table probing
+ Notice properties of actual data (length of station names, -99.9 <= recorded temperature <= 99.9)
+ Use some extra properties (not allowed by the rules) in `1brc_assume.cpp` to optimize more
+ Use mmap for fast file reading
+ Multi threads
+ Other random tricks
