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










