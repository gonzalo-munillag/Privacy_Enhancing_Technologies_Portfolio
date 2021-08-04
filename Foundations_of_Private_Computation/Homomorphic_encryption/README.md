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

### The future of HE

next game changers:

- programmable bootstrapping 
- bridges between different HE schemata
- Multi-key HE: ability to combine data from different domauns!

[Screenshot 2021-08-04 at 11 57 51](https://user-images.githubusercontent.com/57599753/128161949-27b0c4a4-f665-4fbf-a0b0-6618f1a4a4fa.png)

![Screenshot 2021-08-04 at 11 58 31](https://user-images.githubusercontent.com/57599753/128162055-39642bbf-a83a-48a0-9e70-c68de4fc84d5.png)

![Screenshot 2021-08-04 at 11 59 54](https://user-images.githubusercontent.com/57599753/128162292-d2b42e91-5cfd-48af-a2ac-eaf09682aced.png)

https://numato.com/blog/differences-between-fpga-and-asics/

![Screenshot 2021-08-04 at 12 03 33](https://user-images.githubusercontent.com/57599753/128162830-b3ac2442-f803-4feb-a558-4a280f647652.png)


CKKS in a blackbox

Previously, we learned about the Paillier cryptosystem, and implemented it from scratch. From now on, we will use a library called TenSEAL to perform tensor operations on encrypted data. TenSEAL provides different tensor types which relies on the CKKS scheme. So before diving into TenSEAL, we will learn about how CKKS works, without going much into the details or implementing it from scratch. If you want to learn more about CKKS, you can use these amazing resources later.

![Screenshot 2021-08-04 at 11 48 07](https://user-images.githubusercontent.com/57599753/128160417-3554d1fa-5ce6-4a84-ac2e-d333e939282b.png)

The CKKS scheme is mainly considered as a leveled homomorphic encryption scheme. It can encrypt messages encoded as vectors of complex numbers (thus real numbers). The size of the vector to be encrypted into a ciphertext depends on the parameters used, and is generally a power of two (e.g. 4096). So a single ciphertext will hold an entire vector of values, and operations between ciphertexts (with another ciphertext or a plaintext) are performed in an element-wise fashion. It would be our choice to either put multiple values into a ciphertext, or just a single one, but both ways imply the same computation cost. Another cool feature available in CKKS is the ability to rotate a ciphertext (to the right or left with n positions), which will be reflected as a rotation of the encrypted message vector.

CKKS has a special way to deal with ciphertext's noise, it considers it as part of the error introduced during floating point arithmetic. So no bootstrapping is required in order to reduce the noise, although, it is still a leveled HE scheme due to other constraints.

Computing on encrypted data doesn't always mean that we have to compute on ciphertexts only. CKKS allows for performing operations between ciphertexts, as well as ciphertexts and plaintexts.

### Lesson 8: Introduction to TenSEAL
Dashboard

Homomorphic Encryption | Concept 10
Introduction to TenSEAL

TenSEAL is a tensor library, just like PyTorch or Tensorflow, however, instead of manipulating tensors that holds plain data, tensors in TenSEAL holds encrypted data using mainly the CKKS scheme.
The Context

The first object you want to create whenever you deal with TenSEAL is the context. It provides ways to control how the computation is performed, generate and holds the keys (e.g. the secret-key and public-key) required during encryption and computation.

import tenseal as ts

context = ts.context(ts.SCHEME_TYPE.CKKS, poly_modulus_degree=8192, coeff_mod_bit_sizes=[60, 40, 40, 60])

The above line created a context for CKKS encryption, using those specific parameters. We will provide some intuition on how to choose those parameters shortly. The context creation above took care of generating keys required, and you can now get the secret-key for example.

sk = context.secret_key()

Intuitions for Parameter Selection in CKKS

It's hard to choose the right parameters for a certain computation, but if you have some intuitions of what every parameter might be affecting, you can make some experiments using some different variants and see which works best for your use case. Below are some intuitions for choosing the parameters:

    For a given security level (e.g. 128-bits security) and a polynomial modulus degree (e.g. 8192) there is an upper bound for the sum(coeff_mod_bit_sizes). If the upper bound is surpassed, there is a need to use a higher polynomial modulus degree (e.g. 16384) in order to make sure we still have the required security level.
    The multiplicative depth is controlled by len(coeff_mod_bit_sizes) - 2. The above context provide a multiplicative depth of 2 for example. A coeff_mod_bit_sizes=[60, 40, 40, 40, 60] would have provided 3.
    All elements of coeff_mod_bit_sizes[1: -1] should be equal in TenSEAL, since it takes care of rescaling ciphertexts. And we also want to use this same number of bits (e.g. 2 ^ 40) for the scale during encryption.
    The scale of ciphertext (which should be equal to coeff_mod_bit_sizes[1: -1]) controls the precision of the fractional part. The bigger, the more precise.
    The difference between coeff_mod_bit_sizes[-1] and coeff_mod_bit_sizes[-2] (or the scale) controls the precision in the integer part when all multiplication have been consumed. The bigger, the more precise.

Creating Tensors

Now we start creating some encrypted tensors. You can pass in any tensor-like object (it has been tested with torch and numpy), and TenSEAL would take care of encrypting it using the keys and parameters stored in the context.

import numpy as np

plain_tensor = np.random.randn(2, 3)
encrypted_tensor = ts.ckks_tensor(context, plain_tensor, scale=2**40)
encrypted_tensor

You can also set the global_scale in the context so that you never need to pass the scale again and again during tensor creation.

context.global_scale = 2 ** 40
encrypted_tensor = ts.ckks_tensor(context, plain_tensor)
print(encrypted_tensor.decrypt())
# <tenseal.tensors.plaintensor.PlainTensor object at 0x7f391eb8d7c0>

The PlainTensor object is a tensor that we mainly use internally to represent tensors with plain values. You can always call .tolist() to convert it to a list.

print(encrypted_tensor.decrypt().tolist())
# [[-0.6935322486262878, -0.1971640039349987, -0.6806255185457504], 
#  [-0.6699472410544948, 1.3804208496159256, -0.05087860773279334]]

# you can compare it to the plain tensor
print(plain_tensor)
# [[-0.69353225 -0.197164   -0.68062552]
#  [-0.66994724  1.38042085 -0.05087861]]

Compute on Encrypted Tensors

CKKSTensor support addition, subtraction, and multiplication with scalar and tensor-like values. Let's see an example computation.

encrypted_result = (encrypted_tensor + 2) * -3 - plain_tensor
expected_result = (plain_tensor + 2) * -3 - plain_tensor
print(encrypted_result.decrypt().tolist())
# [[-3.2258715329047387, -5.211344710933246, -3.277498460263318],
#  [-3.320211576555451, -11.521684756232458, -5.796486356321944]]

print(expected_result)
# [[ -3.22587101  -5.21134399  -3.27749793]
#  [ -3.32021105 -11.52168339  -5.79648557]]

We can also make dot operations!

# inner product
vec1 = np.random.randn(5)
vec2 = np.random.randn(5)
enc_vec1 = ts.ckks_tensor(context, vec1)
enc_vec2 = ts.ckks_tensor(context, vec2)
print("result:", enc_vec1.dot(enc_vec2).decrypt().tolist())
print("expected:", vec1.dot(vec2))

# result: 0.2651245105129444
# expected: 0.2651244888032714

Batched computation

We previously discussed in the CKKS concept that a single ciphertext can hold multiple values (a vector of values), without affecting the computation or memory costs. However, we didn't use that feature so far. So now, we are going to use this capability to compute on a batch of matrices at the same time.

# a single ciphertext can hold up to `poly_modulus_degree / 2` values
# so let's use all the slots available
batch_size = 8192 // 2 #  4096
mat1 = np.random.randn(batch_size, 2, 3)
mat2 = np.random.randn(3, 4)
# batch is by default set to False, we have to turn it on to use the packing feature of ciphertexts
enc_mat1 = ts.ckks_tensor(context, mat1, batch=True)
enc_mat2 = ts.ckks_tensor(context, mat2)
# let's just compare the first result matrix in the batch
print("result:", enc_mat1.dot(enc_mat2).decrypt().tolist()[0])
print("expected:", mat1.dot(mat2)[0])

# result: [[1.871707310741, -1.64646640599, 0.907704175882, 1.041594801418], 
#          [-1.568004632635, 1.12713712214, -1.687649218268, -0.580647184131]]
# expected: [[ 1.87170707 -1.64646619  0.90770405  1.04159466]
#            [-1.56800442  1.12713697 -1.68764899 -0.58064711]]

More Details

This section provides more details about the library and how some things happens under the hood.
Parallel Computation

TenSEAL takes advantage of parallel computation whenever possible. It uses by default the maximum number of threads the system can run in parallel, but someone can specify that during context creation.

non_parallel_context = ts.context(
    ts.SCHEME_TYPE.CKKS,
    poly_modulus_degree=8192,
    coeff_mod_bit_sizes=[60, 40, 40, 60],
    n_threads=1,
)

Decryption

You might have been wondering how is decryption not requiring a secret-key? But it's just because the context by default holds all the keys, and is considered a private asset. If you want to make it public, then you just call make_context_public(). Make sure you save the secret-key somewhere before that to use it later for decryption.

sk = context.secret_key()
context.make_context_public()

# now let's try decryption
enc_mat1.decrypt()
# raises ValueError: the current context of the tensor doesn't hold a secret_key, please provide one as argument

# now we need to explicitly pass the secret-key
enc_mat1.decrypt(sk)
# returns <tenseal.tensors.plaintensor.PlainTensor at 0x7f391eb8dc70>

You should always make a context public before sending it to other parties to compute on encrypted data.
Serialization

Speaking of sending the context and encrypted data, can we serialize these objects? And the answer is yes! There is a serialize method for every serializable object, like the context and tensors. Although, tensors have a slightly different ways of being loaded, let's see through an example.

ser_context = context.serialize()
type(ser_context)
# bytes

ser_tensor = encrypted_tensor.serialize()
type(ser_tensor)
# bytes

loaded_context = ts.context_from(ser_context)
loaded_context
# <tenseal.enc_context.Context at 0x7f391eb8dfa0>

As tensors always require to be linked to a context, we need to know which context to link the tensor to during deserialization.

loaded_enc_tensor = ts.ckks_tensor_from(loaded_context, ser_tensor)

However, there is also a way to do it the lazy way, deserializing, then linking it to a specific context.

lazy_loaded_enc_tensor = ts.lazy_ckks_tensor_from(ser_tensor)
# try to operate on a tensor that in not linked to a context yet
lazy_loaded_enc_tensor + 5
# raises ValueError: missing context

# You have to first link it
lazy_loaded_enc_tensor.link_context(loaded_context)
lazy_loaded_enc_tensor + 5
# returns <tenseal.tensors.ckkstensor.CKKSTensor at 0x7f391eb8d1f0>

Now we can plug all these features with a system that can pass data between parties and we can do encrypted machine learning inference, where one party encrypts its data and send it to another party that do the inference while data stays encrypted, then send back the encrypted result. The initial party can then use the secret-key to decrypt the result. And fortunately, we already have Duet in PySyft to do this!










