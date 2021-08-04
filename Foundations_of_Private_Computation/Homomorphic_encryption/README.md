# Homomorphic Encryption

### Lesson

You have been learning about different cryptographic schemes throughout previous lessons. They mainly aim to protect confidentiality, or provide authentication. However, the ciphertexts themselves cannot be manipulated or computed on, more precisely, we cannot add two ciphertext or multiply them, which means, that anyone who wants to compute on encrypted data has to decrypt it first. This last assumption doesn't always hold, as some use cases expect the party that perform the computation to not be able to know the data he is computing on, and that's exactly what Homomorphic Encryption (HE) is trying to solve: ensuring input privacy.

Being able to compute on encrypted data without any decryption has been an open problem since 1978, until Gentry showed the world how to build a Fully Homomorphic Encryption (FHE) scheme in 2009. Since then, many techniques and improvements have been made in order to make them more efficient and practical for real world applications, although, HE is still not that simple to use even today.

With HE, a circuit computing on plain data (shown on the right), can be translated to an equivalent one (shown on the left), but computing on encrypted data. The party encrypting and decrypting isn't necessarily the same performing the computation, thus, computing on encrypted data, shouldn't reveal anything about the data itself.

A more concrete example usage of HE is shown in the figure below, where we have two separate entities. The client who wants to protect his data, and the model owner who may want to keep his model private as well. Using HE, the client can only send an encrypted version of his data, to be processed by the model on the other end. The client here doesn't know what are the exact operations that have been performed by the model owner, but only get the encrypted result at the end.

![Screenshot 2021-08-04 at 10 20 43](https://user-images.githubusercontent.com/57599753/128147443-70584005-048b-4f58-b3d4-1614d3f43214.png)

Most recent HE schemes operate in similar manners where they hide the plaintext by adding a secret part, that can be taken off only by using the secret key, plus a noise that should not affect decryption. This noise inside ciphertexts will grow as computation is performed (noises being added and multiplied). So this kind of schemes have to set a strategy for managing noise growth. If this noise exceeds a certain threshold, the decryption might become erroneous.

![Screenshot 2021-08-04 at 10 21 53](https://user-images.githubusercontent.com/57599753/128147626-cff3ac7a-3f5d-4458-b7f5-e868673627e0.png)

You will often hear the term bootstrapping in the HE literature, which is an operation that is performed on ciphertexts, with a goal of reducing ciphertext's noise. As we said previously, operations on a ciphertext can increase its noise, which shouldn't reach a certain threshold, otherwise, the decryption would be erroneous. So bootstrapping will lower this noise, in order to be able to carry out more operations. Bootstrapping is the building block for Fully Homomorphic Encryption schemes.

Try to think about the inverse solution of the second figure, where the model is encrypted and sent to the client for local evaluation on plain data. What do you think of this use case? Do you have any issue with the protocol?

In that case, the model architecture will be known to the data owner, but the weights would be encrypted, which also means that the output would be encrypted. So the data owner will at this point need to decrypt the output, but the one being able to do so is the model owner. So we might need another round of communication to decrypt the output. Another issue may arise here, since the model owner doesn't really know if the data owner have sent the output, or one of the weights.

### My notes

Asymmetric encryption has 2 keys. For HE we have a third called evaluation key. 
This key allows to perform operations bet ciphertexts.

Addtion - xor
multiplication - and

You can build any arbitrary function with these two gates.

You can also make an operation between a cipher text and a plain text.

Noise
most morphic schemata must add noise to the underlying encrypted values to make it secure.
When it is decrypted, the noise goes away, but -> only when the noise is below certain thredhold. If it exceeds it, then it overflows the underlying plaintext. The ciphertext becomes uncryptable, ie, you do not get the original plaintext - only junk.

The homomorphic operation aggregates the noises and can amplify them significantly, more so when it is a multiplication.
Hoever, HE provides an additional operation called bootstrapping. It can be applied to noise ciphertzexts to reset the noise to nominal level. This can be done while preserving the value of the underlying plaintext. Bootstrapping requires the public evaluation key (like the other homomorphic operations). It is used as a maintenance device to clean ciphertexts as they go homomorphic processing. Bootsrapping can be more or less efficient depending on the characteristics.
Thus there are different noise strategies.

A ML can be decomoswed in a sequence of H operations.

In comparison to SMC, HE does not require a complex deployment. HE only adds a layer of encryprtion. No change on the service architecture.

## 2

HE schemata have 5 main characteristics:

1. Security
2. How effciently can it be implemented?
Out of scope (1-2)
3. Noise management


4. Symmetric vs asymmetric

HE asymmetric - 2 pk (encryption and evaluation) and 1 sk
HE symmetric . 1 pk (evaluation) and 1 sk

5. Circuits that it can evaluate

These schemata are equivalent for HE (not in conventional encryption), one can build on the other. Many schemata have been conceived as symmetric, they create a pk from the sk.

![Screenshot 2021-08-04 at 10 31 49](https://user-images.githubusercontent.com/57599753/128149175-66370feb-54f1-4381-8319-ce44585ecb77.png)

![Screenshot 2021-08-04 at 10 33 05](https://user-images.githubusercontent.com/57599753/128149346-0824e34f-3bfd-47d6-ac4f-8e84c3ee6e57.png)

![Screenshot 2021-08-04 at 10 33 58](https://user-images.githubusercontent.com/57599753/128149470-8be3061d-af5d-4c7a-a447-da95563a2e96.png)

![Screenshot 2021-08-04 at 10 35 43](https://user-images.githubusercontent.com/57599753/128149741-86f65c08-d306-4960-92fb-93f2f9446bd6.png)

![Screenshot 2021-08-04 at 10 36 35](https://user-images.githubusercontent.com/57599753/128149873-f3ab2dc0-1fdd-4cf0-9583-eb0a7b0c61a9.png)

![Screenshot 2021-08-04 at 10 42 25](https://user-images.githubusercontent.com/57599753/128150687-8177c609-1ca7-47ac-9fa0-63293ff3ddf3.png)

FHE - Does not limit the depth of the circuit. They so not require to know the circuit in advance. The circuit can be determined at running time. No limit on the number of homomorphic operations. Everything happens as in the plaintext world, but values are encrypted.

SHE - impose limitations on the topology of the circuit or the circuit needs to be given in advance. 

Leveled HE need noise. Tightly predicts how the level of noise evolves. They have a bootstrapping capability, but it is so inefficient that is not used, limiting thee scheme to SHE. If bootstrapping is used, then FHE.

HE schemes are classified into three main types, depending on the possible operations you can compute on encrypted data, and how many operation can be chained on a ciphertext, while still being able to decrypt it to the correct value. We first define what a circuit is, then discuss the 3 types of HE schemes, namely, partially, somewhat and fully homomorphic encryption.

A circuit is a way to represent a function f() as a directed acyclic graph. It is composed of inputs, gates (e.g. boolean or arithmetic gates), edges connecting those gates, and a final output. Inputs will flow through the graph to compute the final output. When doing HE, we often use the multiply and add gates with two inputs. Circuits have two properties of interest, namely, size and depth. The size is the number of gates a circuit has, it impacts directly the computation needed to evaluate the circuit. The depth is the largest distance between every input and the output, this number is very important for HE schemes as it represent the maximum number of operations we need to chain on a ciphertext to evaluate the circuit. Figure 1 shows a circuit of a function f(x, y) = x · y + 3x. This circuit has a size of 3 and a depth of 2.

![Screenshot 2021-08-04 at 10 55 15](https://user-images.githubusercontent.com/57599753/128152593-608b4875-b492-43d4-b0ef-d8d6455e182c.png)

PHE:

This type of schemes can evaluate any circuit composed of a single type of gate, addition or multiplication. It does not restrict the size or the depth of the circuit. This type is not sufficient for many use cases, especially deep learning. The Paillier cryptosystem, which we will study later in this lesson, is an example of a PHE that allows an unbounded number of modular additions.

![Screenshot 2021-08-04 at 10 47 19](https://user-images.githubusercontent.com/57599753/128151379-8f63bee4-fe6b-4524-95bc-ed024f8ec612.png)

They only support one unique type of operation, eg addition. And one single operation. 

SHE

This type of schemes can evaluate circuits composed of both addition and multiplication gates, but with a maximum depth $d$. Leveled Homomorphic Encryption (LHE) is a subset of SHE, it can evaluate circuits with variable depth, but the depth must be set prior to encryption (during parameter selection). BGN is an example SHE scheme that can evaluate a single multiplication on encrypted data. SHE is useful for evaluating low degree polynomials up to some level, however, we sometimes need to evaluate circuits of arbitrary depth, and that's where we will need FHE. (SHE cannot multiply twice)

![Screenshot 2021-08-04 at 10 48 48](https://user-images.githubusercontent.com/57599753/128151622-98cf3bb1-6ca5-4398-a3c8-d6a2bdfd7666.png)

Leveled HE (LHE)

![Screenshot 2021-08-04 at 10 49 47](https://user-images.githubusercontent.com/57599753/128151773-b858f3ed-0ad4-4383-82de-2ae6668fe31f.png)

FHE

FHE schemes can evaluate circuits composed of both addition and multiplication gate, but in contrast to SHE, FHE has an unlimited circuit depth, which makes it suitable for deep learning applications. Although many FHE schemes have been proposed, it has been difficult to use them in practice. An example of this kind of schemes is BFV.

![Screenshot 2021-08-04 at 10 52 30](https://user-images.githubusercontent.com/57599753/128152190-05b9edf4-5108-4abc-bea9-301d388120dc.png)

Machine Learning and the Different Types

Knowing the different types of schemes, it might be obvious that FHE is the ideal type in terms of possible computations. However, using this type of schemes can introduce a high overhead compared to SHE and PHE. Machine learning models generally require both addition and multiplication during evaluation, which makes PHE non trivial to use in this context. SHE and FHE both provide those operations, but with different properties. SHE and LHE have been the first choice for ML applications due to their practicability compared to FHE, but this had a direct impact on the kind of ML models used. SHE can't evaluate arbitrarily deep models as promised by FHE, but have been more practical for years due to the fact that the bootstrapping in FHE schemes, was taking minutes to be executed. In contrast, ML evaluation using SHE, was taking seconds. A lot of work has been done since then to improve FHE schemes, and we have started seeing FHE used for evaluating models with more than 20 layers.

![Screenshot 2021-08-04 at 11 02 08](https://user-images.githubusercontent.com/57599753/128153580-d7d71c4c-857e-4b99-b700-611644c57620.png)

![Screenshot 2021-08-04 at 11 03 44](https://user-images.githubusercontent.com/57599753/128153828-5899e65d-bd5f-49cb-8d07-15918a07e2bc.png)

![Screenshot 2021-08-04 at 11 04 06](https://user-images.githubusercontent.com/57599753/128153901-f1aba5b6-2e59-4930-b0a8-c28b205d4a21.png)

## Paillier Cryptosystems

What is the Paillier cryptosystem?

In this section you will learn about the Paillier cryptosystem, which was published in 1999. This is a partial homomorphic encryption scheme based on public key cryptography and modular arithmetic.

This is an additive homomorphic cryptosystem, which basically means that we can add encrypted integers together. More specifically, the process looks like this:

    Alice generates a private/public key pair.
    Anybody can encrypt an integer under Alice’s public key, and Alice can use her private key to decrypt such ciphertexts.
    Given Alice‘s public key and two ciphertexts, anybody can compute an encrypted output which will decrypt to the result of adding those two integers together.
    In a similar fashion, we can also perform multiplication of an encrypted integer by a plaintext integer.

In the rest of this section we will cover:

    Key generation
    Encryption and decryption (with a worked example)
    Homomorphic addition and multiplication (with a worked example)
    
    
![Screenshot 2021-08-04 at 11 07 43](https://user-images.githubusercontent.com/57599753/128154462-1a12e010-ce65-4059-8025-d33de4a0bb38.png)

![Screenshot 2021-08-04 at 11 35 47](https://user-images.githubusercontent.com/57599753/128158616-8bc5f72a-83fc-40f3-8395-9f714e4df9d7.png)


Gotchas

There are a couple of special cases which need to be handled carefully. The first is multiplying by 0. Because any number to the power of 0 is 1, if we multiply a ciphertext by a plaintext 0 using the method above, the result will always be 1, and anyone who sees this "encrypted" value will know that it decrypts to 0. Luckily we can use an alternative method for this case. Multiplying any number by 0 gives 0, which means we can just skip the calculations and encrypt a 0 directly using the standard public key encryption scheme. Since encryption step introduces a random number, nobody without the private key will be able to know what the plaintext is.

The other case is multiplying by 1. Because any number x to the power of 1 is x, if we multiply a ciphertext by a plaintext 1 using the normal method, the output will be the same as the input. This is less severe than the case with 0 where the encrypted value could be inferred, but still a problem because anybody who is watching the communication between whoever holds the private key and whoever is multiplying numbers will be able to work out that the number was multiplied by 0. The solution here is another workaround: instead of multiplying by 1, we perform an equivalent operation: adding 0! We just freshly encrypt a 0 and perform the usual addition procedure to obtain a secure ciphertext.









