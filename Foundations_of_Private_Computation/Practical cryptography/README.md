# Practical cryptography 

## Discrete logarithm problem

The discrete logarithm problem is the problem of finding 𝑦 knowing 𝑥, 𝑝 (prime) and 𝑔 (generator for the group of 𝑝) such that:

x = g^y (mod p)

While a normal y = log_b(x) looks like:

<img width="700" alt="Screenshot 2021-04-22 at 10 28 31" src="https://user-images.githubusercontent.com/57599753/115682157-7d059e80-a355-11eb-9c40-31bcbc97f87f.png">

This x = g^y (mod p) looks like:

<img width="706" alt="Screenshot 2021-04-22 at 10 29 12" src="https://user-images.githubusercontent.com/57599753/115682277-973f7c80-a355-11eb-8e7d-76e8e8ffd991.png">

Finding y is tough.
**The larger the prime p, the tougher it gets to predict y. We use a generator because then y could be any number between 1 and p-1. y could be larger but because of mod p you only need a number less than p to make g multiply itself with the mod product so that it generates all the values of x between 1 and p-1. x is the randomly chosen secret key between 1 and p-1. **

You can try to crack what the value of y is based on (x, g, p). 

The concrete approach definition for computational security: A scheme is (t, e) secure if any adversary running at most during time t succeeds to break the code within probability at most e. Say a supercomputer can do c key test per unit time, then at time t he will have run c*t checks. The probability of guessing the key of length n bits is

p(c,t,n) = ct/2^n

This probability has to be smaller than e so that the scheme is (t, e) secure. Recall that as the size of the key (n) grows the probability decreases exponentially so comparing we need a lot of time (because it grows linearly) to get to the same probability.

<img width="1053" alt="Screenshot 2021-04-22 at 11 42 28" src="https://user-images.githubusercontent.com/57599753/115693142-f30f0300-a35f-11eb-8b53-8a55be0c05a4.png">

## The Diffie-Hellman Key Exchange

<img width="1040" alt="Screenshot 2021-04-22 at 11 43 16" src="https://user-images.githubusercontent.com/57599753/115693155-f6a28a00-a35f-11eb-97a4-9c74513cfdb1.png">

<img width="1040" alt="Screenshot 2021-04-22 at 11 47 34" src="https://user-images.githubusercontent.com/57599753/115693803-8ba58300-a360-11eb-8ff2-ac0e85c00adb.png">

## Linear congruential generation

A linear congruential generator (LCG) is an algorithm that yields a sequence of pseudo-randomized numbers calculated with a discontinuous piecewise linear equation.
[Source](https://en.wikipedia.org/wiki/Linear_congruential_generator)

<img width="577" alt="Screenshot 2021-04-22 at 12 43 18" src="https://user-images.githubusercontent.com/57599753/115701689-53a23e00-a368-11eb-9824-2b96e9d469be.png">

## Bits, bytes...

There is a whole section on bity and bytes and encoding

## Stream sipher

Just to show:   
We encrypt a message of N bytes into another of N bytes.
We pad (or XOR) each byte with a secret key to get the cipher text.
I think they use XOR for the shift because you have a 50/50 chance of beocoming 0 or 1 if tge secret key is a random sequence of bits. AND and OR gates are skewed to 75/25. Plues, XOR is complementary.

So far, the cipher we coded pads bit by bit or, equivalently byte by byte, this is what we know as stream cipher because we generate a stream of bytes to pad the message. 

<img width="908" alt="Screenshot 2021-04-23 at 13 39 28" src="https://user-images.githubusercontent.com/57599753/115865991-5a4cb600-a439-11eb-9116-adb6891acb84.png">

In reality, it is more complicated.









