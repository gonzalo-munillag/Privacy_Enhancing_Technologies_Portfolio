# Secure multiparty computation

Secure multi-party computation (also known as secure computation, multi-party computation (MPC), or privacy-preserving computation) is a subfield of cryptography with the goal of creating methods for parties to jointly compute a function over their inputs while keeping those inputs private. Unlike traditional cryptographic tasks, where cryptography assures security and integrity of communication or storage and the adversary is outside the system of participants (an eavesdropper on the sender and receiver), the cryptography in this model protects participants' privacy from each other.   
[Ref](https://en.wikipedia.org/wiki/Secure_multi-party_computation)


<img width="1060" alt="Screenshot 2021-08-10 at 18 21 05" src="https://user-images.githubusercontent.com/57599753/128896733-c5ff9bd6-49ce-4307-aa33-fd6cce33e176.png">

MPC Security Models

What do we mean when we talk about security?

For secure MPC to be 'secure', it must be able to allow a group of participants to learn the correct output of an agreed-upon function without revealing anything else about their private inputs.

In this section, we will provide a more formal statement of the properties that secure MPC attempts to guarantee.

In particular, we will explore two different 'adversarial models' under which we can guarantee security. This means that we will attempt to formalize the different ways in which participants can try to break our security goals. We can vary the assumptions we make about these potential adversaries to make sure we can handle any behavior that falls under these assumptions.
Honest-but-Curious model

An honest-but-curious adversary (sometimes referred to as semi-honest) is one who corrupts parties, but follows the protocol as specified. In other words, the corrupt parties run the MPC protocol honestly, but they may try to learn as much as possible about the private inputs of other parties.

This could include, for instance, several corrupt parties who collude with each other in order to learn information about the other honest parties. They can combine all the messages they receive in the process of running the MPC protocol.

However, note that these parties cannot take any other actions outside of observing the protocol's execution - in this sense, they are often considered 'passive' adversaries.
Malicious model

A malicious (sometimes referred to as active) adversary may instead cause corrupted parties to deviate from the agreed-upon protocol in an attempt to violate security.

These adversaries are strictly more powerful than the honest-but-curious adversaries - they can still try to learn as much as possible by following the protocol honestly or pooling information with multiple corrupt parties, but they may also deviate arbitrarily from the protocol execution. This could include an adversary that can control, manipulate, and arbitrarily inject messages on the network.

Under the malicious model, there are two subcategories of security:

The weaker subcategory is known as 'security with abort'. In this setting, the honest parties may not be able to receive the correct output of the protocol function. Instead, once they detect the presence of corrupted parties, they abort the protocol. This guarantees that input privacy is maintained, but gives no guarantee of output correctness.

The stronger subcategory also guarantees 'robustness', meaning that the correct output will be sent to honest parties, even in the presence of corrupted ones.

Whether or not robustness can be achieved often depends on the number of corrupted parties. In an 'honest majority', strictly less than half of the parties are corrupt, assuming some limit on the power of a malicious adversary. Robustness is still achievable in this setting. However, in a 'dishonest majority', up to n-1 out of n players may be corrupted, meaning that robustness cannot be guaranteed. Of course, it's much more difficult to achieve security in the presence of a dishonest majority, but there are still schemes that do so!

Various theoretical results show the computational complexity of these different security models [cite]. Generally speaking, the weaker the security model, the more efficient an MPC protocol can be made.

Relaxation: Covert Security

Covert security offers a relaxation of the malicious security model, trying to capture a more realistic setting. In this model, adversaries are still willing to deviate from the protocol arbitrarily, but only if they will not be caught. This can be useful in settings where a corrupt party could have their reputation damaged, or could be removed from future computations that could be useful to them.

In a covertly secure scheme, we make an assumption that if a party deviates from a protocol, they will be caught with high probability. In this case, covert adversaries are often forced to act as if they are honest-but-curious, for fear of being caught.
Security Definition

Computational security relies on the hardness of mathematical problems, like factoring. It relies on computational limits of existing (and projected) hardware. It gives guarantees based on the infeasible amount of time that even a powerful adversary would have to spend to break security.

Information-theoretic security is a stronger security model. In this setting, the system cannot be broken even if the adversary has unlimited computing power, because its security comes purely from information theory - that is, there is simply not enough information present for an adversary to break privacy.

Most MPC models are secure in the information-theoretic setting - meaning that they are secure regardless of adversarial power or exponential increases in computational power.

There may be other assumptions that we make in an MPC model - e.g., that participants use a synchronized network, or that a secure communication channel exists between every pair of participants. These assumptions weaken the power of a malicious adversary, who may not be able to read, modify, or generate messages.


A malicious adversary has a lot of assumed power, but they don't have to use it all! They may behave just like an honest-but-curious adversary. However, for an MPC protocol to be secure against a malicious adversary, it must be able to protect against all of these different kinds of deviations.
