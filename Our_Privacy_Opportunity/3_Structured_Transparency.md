# Structured Transparency

*How can we enable desired uses of information, without also enabling misuse?*  
This goal is called “structured transparency”: gaining the benefits of transparency, but in a structured way. The goal of structured transparency is to enable precise social or technical arrangements that determine who can see what, when, and how.

Acronyms:
Informartion floq (IFlow)
Privacy enhancing tehcnologies (PETs)
Structured transparency (ST)

## Main takeaways

Input privacy solves the copy problem, via assymetric encryption, homomorphic encryption or secure multiparty computation.
Output priavcy solves the bundling problem, via differential privacy.
Input verification solves the bundling problem, via HTTPS, active security added to HE and SMC, and zero knowledge proofs.
Distributed governance solves the recursive enforcement problem.

In my opinion, the frontiers of the 5 components they have chosen sometimes are fuzzy when mapping them to PETs. Even the speakers sometimes say output in a chapter about input privacy or verification. More so when it comes to zero knowledge proofs, as they can verify outputs and inputs.

## #1 Introduction

Examples: Secret ballots, or a dog snifing whether a bag is safe or not without open the private belongings. It is an interdisciplinary field. Zero knowledge proofs act similar with data.

**The solutions presented below, allow for higher levels of structured transparency and thus push the Pareto frontier of the transparency and privacy trade-off.**

## #2 The 5 components of structured transparency

ST framework: Breaks down a particular IFLow into the individual challenges that need to be addressed, then matches which of the many PETs may be applicable for the desirable IFlow. It is a high-level framework that allows one to map use cases with PETs without delving deep into the technology. ST's guarantees operate over an IFlow. The guarantees of ST are:

1. Input privacy (IP): Create IFlow between multiple parties while keeping the inputs secret.
2. Output privacy (OP): Allows to disperse outputs containing some information without accidentally revelaing other information that should be kept hidden, like the input or the sender of the input.
3. Input verification (IV): Allows you to verify the content, integrity and origin of an IFlow without revealing additional information. Possible to verify that an IFlow was constructed by specific holders of specific keys that we deem trustworthy. It can also be used to verify that transformations within the IFlow ocurred as it was suposed to.
4. Output verification (OV): Verifies attirbutes about what is happening to the hidden IFlow itself. Allows for properties of an IFlow to be verified without revealing the exact transformation happening within an IFlow.
5. Flow governance (FG): It is satisfied if each party with concern about how that information could be misuse, has the ability to prevnet an IFlow to be changed. All parties would need to agree to change the IFlow in that way. Sets rules so that nothing about the integrity about the other four components is compromised.

(1) and (2) guarantees refer to the information of the flow that needs to be hidden; solve the copy problem.
(3) and (4) guarantees refer to the information of the flow that needs to be revealed in a verifiable way; solve the bundle problem.
(5) dictates who is allowed to change the flow, including who can modify (1), (2), (3), and (4). It solves the recursive enforcement problem.

## #2 Input privacy

**Act of running algorithms on data with other parties does not teach you anything about the input data of other parties. The only people leanring anything throught the process, are the parties receiving the outputs.** 

IP is a guarantee that one or more people can participate in a computation in such a way that no party learns anything about any other parties' inputs to the computation, intermediary variables, or outputs unless any of them has been designed to be specifically for such party.  
No party violates privacy in the means to facilitate the IFlow. However, there is a nuance, one may say that once the IFlow is over, then the recipient could share the content of the output with any of the parties involved in the IFlow. However, this is disregarded because that event happens outside IP of the designed IFlow, this would be addressed in OP. IP however, does not account in case a party has seen the data before the input, but it is a rare case where two distrusting parties have access to each other's data (Toy example: The mailman sees you writing the letter).
IP is equivalent to a pipe that does not leak and is only one way, no one but the sender knows the input, and sender A does not know about sender B's input.

There are nontechnical approaches for IP, like NDAs, as parties pledge that all the inputs are kept secret and it is only revealed what all the parties agree upon.

**IP solves the copy, as the parties cannot make a copy of the information they will never see.**

Public key cryptography (PKC), asymmetric encryption: Alice generates a public (disclosed) and a private key (secret). A public key can encrypt a message that can only be decrypted only with your secret key. It is a one-way pipe from anywhere in the world to you. The simplest form of IP.  
PKC makes any method of transfer IP compliant.

Homomorphic encryption (HE): One can compute over encrypted data. The output will always be encrypted with the same key one used to encrypt the data. IP is preserved while also facilitating arbitrary computations. A bank for example would never know how much money you have while operations can still be made: loans, transactions, etc. One can also store information in a HE way and such information is at rest for any computation to be run on it at any time. Combining this with PCK, a group of people can encrypt data with a public key, a third party runs the computations, and the respective outputs may be decrypted with the corresponding private key. We are not only talking only about data flows but also about data at rest. **Use cases where sharing the data is too risky is where HE is suitable**. 

Secure multiparty computation (SMC), additive secret sharing (AddSS): Generalization of HE. Defines an algorithm wherein multiple people can calculate the output of a function while keeping their inputs secret from each other. It is a formal group of computational algorithms that satisfy IP. One of them is AddSS, which allows multiple people to share ownership of a number, the number is divided into parts for each shareholder to control, this shared control is only possible because AddSS is IP compliant, it solves the copy problem. E.g., you split 5 into -1 and 6, together they represent 5, but separately they could have meant any other number because these numbers are chosen randomly, they could have been -5864 and 5869. Carol gives one piece to Alice and another one to Bob, Bob has no idea what number could Alice or Carol may have. Bob or Alice would be able to copy the encrypted number 5. It requires Bob and Alice to agree to decrypt the number, this is true shared governance over the number. One may be able to compute arithmetic operations like multiplication, e.g. if Bob and Alice multiply each share by 2, Carol would get the two results and would attain 10. There has been an operation carried out over "encrypted data". 

SMC requires intensive messaging, which might not be ideal where networks are not reliable. HE does not need networking capabilities but it is very computationally intensive.

**It is not only about sending information, one may also store information while also preserving IP.**

## #3 Output privacy

If I have an IFlow with inputs and outputs, how much can I reverse engineer about the inputs by reading the outputs? An IFlow, while complying with IP (Protecting the information at the input and during the travel to the recipient, like in end-to-end encryption), the recipient may use the output to infringe the sender's privacy. OP solves this problem.

**OP ensures that certain subsets of information do not make it through the IFlow.** OP is concerned with the bundling problem. E.g. in audio, your tone may convey information that you would like to keep private.

## #4 Technical tools for output privacy

Differential privacy, DP: Adds noise in a clever way to the output of an algorithm so that it is indistinguishable between the reality of an individual being included in the input and the reality where the individual is not. It is useful for concrete use cases, aggregate statistics over a large group of people. It unbundles your participation in a survey from a practitioner studying the results. This inspires data donation.

**It provides holistic protection from privacy leakage throughout all your data sharing activities.**

An interesting attack is to impersonate x amount of participants in a survey and ask an individual to provide a specific data point. Even if the process complies with IP, because the impersonator knows the rest of the values (they were created just for the scam), then the impersonator can find out your data point after the result is revealed. 

Aaron Roth about the right value of epsilon: "There is no universal answer to this", what he added was useful to think about DP, but even then it is still hard-set a number to epsilon. A helpful view of DP is that you can see e^epsilon as to how many more times an event is more likely to occur in the eyes of an attacker. Or, the probability of any future event is only e^epsilon times larger than the probability of those events happening in the future when you did not participate in a study.

Check my [blog](https://github.com/gonzalo-munillag/Blog) to know more about DP.

## #5 Input verification

*How do you know the input information is true?*

This is related to internal consistency, it refers that someone in the real world can recognize how things are usually constructed, when you are trying to spot a fake, you are looking for internal consistency. Traditionally, one adds more information to the input so that one may assess whether the input is fake or not.  
Naturally one uses internal consistency to verify the authenticity of IFlow inputs, however, with enough effort, internal consistency may be faked itself. Furthermore, usually, internal consistency requires more bundled data.

Cryptographic signatures, like the ones used in [HTTPS](https://en.wikipedia.org/wiki/HTTPS), may be used for IV. The principal motivations for HTTPS are authentication of the accessed website, and protection of the privacy and integrity of the exchanged data while in transit. It protects against man-in-the-middle attacks, eavesdropping, and tampering. - Wikipedia. However, this is only useful when receiving data, but what happens if in the middle there has been a computation, how do you verify that the computation is being correctly executed? Zero-knowledge proofs, and encrypted computations (e.g. HE and SMC) with additive security. These PETs provide a signature for when the information within an IFlow is processed, such that there is cryptographic evidence that allows anyone who participated in the computation to verify that their input was used in the computation. **The signature of the output still has the signatures of the inputs.** You can verify e.g. that your data was inputted into an ML model and that such ML model was used.
These techniques, therefore, verify that the inputs have been altered in a very specific way and not in any other, and the former technique using asymmetric encryption verifies the entity from where the input came from.

A public-private key pair does not need to be attached to your real identity, but an anonymous identity. You can prove you are the same person from before, but no one knows who you really are. Furthermore, you may have an infinite number of public-private key pairs, that way it is more difficult to pinpoint you as the individual. Your public key may be associated with a group, so you do not need to say who you are, but it is known that your anonymous identity belongs to this group. 

You cannot make trust out of anywhere, in a setting where e.g. the data you are selling cannot be accessed directly by the customers. You first need to make a thing with low trust, and then when it indeed works, you scale this up with these cryptographic technologies. Reputation systems are very useful, as you can build trust with them. If you do not trust the reviews, you could use your own network to verify whose public key is the one that signed the review, and if each person of the chain between you and that reviewer trusts each other, then there is a chain of trust, and therefore the review is truthful.

## #6 Output verification

*How do we verify that the outputs received from a hidden IFlow contain the desired properties?*  
OV allows you to audit whether an algorithm you do not know, but that is affecting your life, is actually good. 

OpenMined argues for algorithms to be more transparent, which allows for an open discussion, seeing algorithms as an agreed decision-making process. However, humans are better at many things than algorithms, e.g. when things are fuzzy; but at the same time, humans can have a bias. However, it is easier to audit an algorithm than a person. 
But, if one wants to keep the algorithm private, this would not work. For this case, then a trusted third party could verify an algorithm. But in turn, perhaps there is e.g. no regulator for a specific algorithm. **Therefore, there is a need to construct a new IFlow with a publicly verified algorithm whose purpose, in turn, is to verify an algorithm from the intended IFlow via IP and OP techniques**, i.e. using structured transparency to evaluate the algorithm while keeping it secret. It alleviates the risk of disclosing any intellectual property contained in the algorithm.

## #7 Flow governace

*When an IFlow is set, who has the ability to modify its design?* Without appropiate governance structure, the integrity of the other 4 components are compromised.  
With consensus based systems, distributing governance, then decisions about who can enter the system, or voting, is done democrately. The downside, however, has a problem in case X number of members of the system get together or are malicious in cooperation, e.g. with a 51% attack. 

You can either have a system where a person is able to veto transactions that person does not want. Or a person can delegate his/her information to a set of parties that he/she knows will not collude against him/her.

**Distributed governance systems solve the problem of recursive enforcemebt problem. You could split the dataset into chunks, and each chunk is stored by different parties. Any computation, then needs to be signed off by every member, otherwise, not all members will provide the data.**

#### Interesting links and other things

Advertisers scrap pictures in your social media app to find objects you like or you need, like medications.