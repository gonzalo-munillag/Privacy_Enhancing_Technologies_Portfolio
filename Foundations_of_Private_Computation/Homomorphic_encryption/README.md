# Homomorphic Encryption

## 1

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
Out of scope

3. Symmetric vs asymmetric

HE asymmetric - 2 pk (encryption and evaluation) and 1 sk
HE symmetric . 1 pk (evaluation) and 1 sk

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



4. Circuits that it can evaluate


5. Noise management








