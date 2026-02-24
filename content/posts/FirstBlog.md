+++
date = '2026-02-24T19:06:50+07:00'
draft = false
title = 'FirstBlog'
math = true
+++

# ssmal



> When they leak the high bits of p+q, the rest is just a distributed search — rent the cloud and flex.



---



## Challenge Description

`chall.py`

```python

from Crypto.Util.number import getPrime, isPrime



p = getPrime(256)

q = getPrime(256) 

N = p*q



e = 65537



flag = b'BPCTF{redact}' 

c = pow(int.from_bytes(flag, 'big'), e, N)

gift = (p+q)>>40

print(f'N = {N}\nc = {c}\ngift = {gift}')





"""

N = 5758124415184468271370250630048687746812715972269092676700260830924771547226161680827118153372606993872590019171624226415454063566537634596851695999313069

c = 4258014490469377191207443169980969026536758269486705363402307773455639773007422079769567310663689852817179059312032143236005345809847891632360620594960862

gift = 139200565274113272217771369795858181556454302427519574149545982701

"""



```



The program leaks `N = p*q`, the ciphertext `c`, and `gift = (p+q) >> 40` — an approximation of `s = p+q` with the lower 40 bits removed. Recovering `p` and `q` (and thus `d`) reduces to finding the unknown 40 lower bits of `s`. Once `p,q` are recovered, decrypt `c` to obtain the flag.



---



## Code Review



This is a classic **partial-sum leak** RSA problem:



* If `s = p + q` were known exactly, `p` and `q` are roots of `x^2 - s x + N = 0`.

* With `gift = s >> 40`, we have `s = (gift << 40) + k` for unknown `k` in `[0, 2^40)`.

* For each candidate `k` compute `D = s^2 - 4N`. If `D` is a perfect square then `p = (s + sqrt(D)) // 2` and `q = (s - sqrt(D)) // 2`. Verify `p*q == N`.

* So the problem is an **exhaustive search over 2^40 candidates**, with plenty of ways to prune and parallelize.



This leakage is fatal but straightforward: leaking the high bits of `p+q` turns factorization into a bounded brute-force search rather than requiring subexponential factoring.



---



## Solution



1. Compute `s0 = gift << 40`.

2. For `k` in `0 .. 2^40 - 1` (parallelize!):



   * `s = s0 + k`

   * `D = s*s - 4*N`

   * If `D < 0` continue. Let `r = isqrt(D)`. If `r*r == D` then candidate found.

   * Compute `p = (s + r) // 2`, `q = (s - r) // 2`. Verify `p*q == N`.

3. Compute `d = inverse(e, (p-1)*(q-1))` and `m = pow(c, d, N)`; convert `m` to bytes to get the flag.
