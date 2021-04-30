# Asymmetric Cryptographic Systems

## RSA

Public key cryptography = asymmetric cryptography. RSA is the de factor algorithm
There are two keys, one for encrypting and one for decrypting.

In symmetric encryption, there is only one key which must be exchanged between two parties, this means that for N parties to communicate with each other, there is a need for N(N-1)/2 keys.
From the perspective of an entity, the entitiy communicates with N-1 other entities. There are N entities, so there are N*(N-1) connections. For each pair of connections, we only need one key, so that is why we divide by 2.


Other asymmetric key cryptosystems are Paillier and ElGamal.

## Homomorphism

Let's put some formalism first. Let (𝐺,★) and (𝐻,◻) be algebraic groups. A group homomorphism from 𝐺 to 𝐻

is a function

𝑓:𝐺→𝐻

such that

𝑓(𝑥★𝑦)=𝑓(𝑥)◻𝑓(𝑦)
∀𝑥,𝑦∈𝐺

As a simple example, take the two groups (ℝ,+)
and (ℝ+,⋅), i.e. the real numbers with addition group and real positive numbers with multiplication group. Take the function 𝑓(𝑥)=𝑒𝑥𝑝(𝑥), then 𝑓

defines an homomorphism with the two groups since

𝑓(𝑥+𝑦)=𝑒𝑥+𝑦=𝑒𝑥⋅𝑒𝑦=𝑓(𝑥)⋅𝑓(𝑦)

Homomorphism on the RSA

RSA cryptosystem defines a homomorphism on (ℤ𝑝,⋅)

𝐸𝑛𝑐:(ℤ𝑁,⋅)→(ℤ𝑁,⋅)

Again, this cryptosystem has been explained in another notebook (I remind you though that here 𝑁
is a public parameter product of two randomly chosen primes 𝑝 and 𝑞).

We will test that:

𝐷𝑒𝑐(𝐸𝑛𝑐(𝑚𝑥)⋅𝐸𝑛𝑐(𝑚𝑦))=𝑚𝑥⋅𝑚𝑦

Homomorphism on Paillier

Paillier cryptosystem defines an homomorphism on the group (ℤ𝑁2,+)
where 𝑓

is the encryption function, this is:

𝐸𝑛𝑐:(ℤ𝑁,+)→(ℤ𝑁2,⋅)

where the function 𝐸𝑛𝑐(𝑥)

is

𝐸𝑛𝑐(𝑥)=𝑔𝑥⋅𝑟𝑁(mod𝑁2)

and 𝑁
is the product of two prime numbers 𝑝 and 𝑞 such that the maximum common multiple of 𝑁 and (𝑝−1)(𝑞−1) is 1. At the same time, 𝑔 is a random element of ℤ𝑁2 and 𝑟 is a random number the range 0<𝑟<𝑁 and part of the group (ℤ𝑁,⋅) i.e. 𝑔𝑐𝑚(𝑟,𝑁)=1

.

There is another calculated parameter kept private

𝜇=(𝐿(𝑔𝜆(mod𝑁2)))−1(mod𝑁)

where the function 𝐿

is defined as

𝐿(𝑥)=𝑥−1𝑛

taking the integer part of the divison and 𝜆
is the least common multiple of the order of the primes i.e. of 𝑝−1 and 𝑞−1

.

One can decrypt the ciphertext 𝑐
and recover the original message 𝑥

as

𝑥=𝐿(𝑐𝜆(mod𝑁2))⋅𝜇(mod𝑁)

𝐸𝑛𝑐(𝑚𝑥+𝑚𝑦)=𝐸𝑛𝑐(𝑚𝑥)⋅𝐸𝑛𝑐(𝑚𝑦)

Thus the encryption of two plaintexts in 𝑁2
is the multipication of their ciphertexts. Let's try to show this in some examples, the proof of the homomorphic encryption can be found elsewhere.


Homomorphism on ElGamal

El Gamal cryptosystem defines a homomorphism on (ℤ𝑝,⋅)

𝐸𝑛𝑐:(ℤ𝑝,⋅)→(ℤ𝑝,⋅)×(ℤ𝑝,⋅)

s. t

𝐸𝑛𝑐(𝑚)=𝑐=(𝑐1,𝑐2)

This cryptosystem has been explained in another notebook so I refer the reader there to understand it better. The muliplication in the plaintext is defined the usual way but on the ciphertext we multiply pointwise (Shorr):

𝐸𝑛𝑐(𝑚𝑥)=(𝑐𝑥1,𝑐𝑥2)
𝐸𝑛𝑐(𝑚𝑦)=(𝑐𝑦1,𝑐𝑦2)
𝐸𝑛𝑐(𝑚𝑥)⋅𝐸𝑛𝑐(𝑚𝑦)=(𝑐𝑥1⋅𝑐𝑦1,𝑐𝑥2⋅𝑐𝑦2)

We have to test the homomorphism:

𝐸𝑛𝑐(𝑚𝑥⋅𝑚𝑦)=𝐸𝑛𝑐(𝑚𝑥)⋅𝐸𝑛𝑐(𝑚𝑦)=(𝑐𝑥1⋅𝑐𝑦1,𝑐𝑥2⋅𝑐𝑦2)

or equivalently

𝐷𝑒𝑐(𝐸𝑛𝑐(𝑚𝑥)⋅𝐸𝑛𝑐(𝑚𝑦))=𝑚𝑥⋅𝑚𝑦

Up until now we have seen that RSA, ElGamal and Paillier encryption schemes are homomorphic with a certain operation. Furthermore this operation can be applied to all elements of the group (i.e. no matter what are the two oringinal messages as long as they belong to the initial group set). This properties defines what we know as partial homomorphic encryption.
Fully homomorphic encryption

Ideally we would like to define encryption functions such that they do not only work in one operation (say sum or product) but with the two at the same time. This is what the community coins as fully homomorphic encryption. During many years there was a quest to find a fully homomorphic encryption scheme and finally Craig Gentry published his PhD thesis in 2009 with the first fully homomorphic encryption scheme based on algebraic lattices.





