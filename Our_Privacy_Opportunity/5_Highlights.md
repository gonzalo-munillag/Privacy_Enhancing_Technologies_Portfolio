# Information Crunch

## Insights

I realized: PETs are tools that can make data scarce, thus, they are necessary for the future data economy.

The moment companies are able to analyse data in a privacy-preserving manner efficiently and accurately, then people and governments will start making regulations to make it mainstream. Companies should plan for this.
 
Focusing on proprietary SW is a short term strategy for startups or companies as they will ultimately be replaced by open-source SW. Like it happened with ML. The long term defensible strategy is to become gatekeepers for the world's information within the forthcoming networks of data. While you only need a few packages for all of us to use, information flows are the things that companies and communities will need more of. It will not be about hoarding data either if that is not what the original data owners want. It is about creating and maintaining information flows so that people and other organizations achieve their goals in the best possible way.

Ilya Mironov, FacebookAI - SQL must be enhanced to be privacy-preserving, which is seriously tackled by multiple research teams of DP.

Bob Rogers - Problem: 16 to 30 months to validate an existing ML algorithm (With an FDA certification), 1.5 to 2.5 million dollars to do the validation across all these sites (datasets across organizations for validation) in order to get the algorithm into the marketplace.

The expected market for healthcare AI is 36 billion dollars, yet only 30 algorithms have been cleared by the FDA, i.e. there is a need to close the gap as more algorithms will be needed.

Techniques: privacy-preserving computing and confidential computing, validating algorithms without moving the data throughout pre-processing, annotation, and computation. The model weights are the IP of the product that an organization is using, so the algorithm must also be protected.

Aaron Roth - Tooling around DP is limited. We are not at a place where you can easily use DP in-house. There are some open-source algorithms, but, what we do not have much of, is an end-to-end infrastructure to use DP. Privacy does not come for free, we must see privacy as a scarce resource, we must use epsilon to keep track of it, but there is nothing out there that can make it happen yet, perhaps a solution comes from Harvard and Microsoft. Once this is solved, then DP can be widely adopted and used by companies in-house without expertise.

Aaron Roth - Privacy budgets need to be personalized, but how do you keep track of all the institutions that have your data and thus do appropriate budget accounting?
It sounds like sci-fi at the moment.

Cynthia Dwork - There is nothing other than politics for federating and maintaining global privacy controls in e.g. hospitals. She has no hopes that that happens in the commercial environment, even in hospitals too.

About analogies, data is more like [fire](https://ystrickler.medium.com/data-is-fire-92a110557ef8) than like crude oil.

Lock-in effect= monopoly: Artificially increases scarcity, and therefore prices, and reduces the need to provide the service appropriately. 

Interoperability avoids the lock-in effect. Competitive compatibility is a strategy to make a new business' application, to be compatible with a competitor's app. This is used to defeat centralization, it lowers the switching cost, switching in steps.

Privacy is not about hiding the identity of the person, a corporation might not need to know who that person is exactly, but know about the characteristics of this a person so that it can target him/her content with a larger scale malicious intent.

Privacy is about user agency, it provides the user with the means to choose the right information flow.

## Summaries 

### Problems:

Copy Problem. 
Once you share your data, you stop having control over it, it can be further copied and transferred to yet other third parties.  

Bundling Problem. 
To verify information, you sometimes need extra information, which could be potentially avoided.

Recursive Enforcement Problem. 
If there is an authority, who is the authority of the authority?

### Goals 

Create information flows within society, which in turn creates social good.   
Privacy is in service of this higher purpose, it is a subtopic. Privacy technology is not only about privacy, but it can also be used to prevent misinformation or inappropriate information flows.

The promise of privacy-enhancing technologies: How can society accomplish its goals with lower risk, higher accuracy, faster speed, more aligned incentives better than before through better information flows? This must be answered by entrepreneurs and companies.

There is a balance between privacy and transparency that must be accounted for in the design of any appropriate information flow.

### Definitions

Process:  
1. Breakdown an existing IFlow in the context of structured transparency: IP, OP, IV, OV, and FG.
2. Pick the weakest components and think how to solve them.


What is contextual integrity?
A description of when people in society feel their privacy is violated "As Helen talks about in her video - contextual integrity's core aim is to pinpoint when people feel that their privacy is violated. This is different from other definitions of privacy which attempt to create a single ontology or simple rule for when privacy is violated or not violated. But Helen points out that people in a society already know viscerally when their privacy has been violated - and contextual integrity is an attempt at describing that reaction."

Privacy and transparency are a Pareto trade-off, but with innovations, one may get more of both. Companies and researchers may have both accuracies of data and privacy of their customers.

Structured transparency framework: Breaks down a particular IFLow into the individual challenges that need to be addressed, then matches which of the many PETs may be applicable for the desirable IFlow. It is a high-level framework that allows one to map use cases with PETs without delving deep into the technology. ST's guarantees operate over an IFlow. The guarantees of ST are:

Input privacy (IP): Create IFlow between multiple parties while keeping the inputs secret.  
Output privacy (OP): Allows to disperse outputs containing some information without accidentally revelaing other information that should be kept hidden, like the input or the sender of the input.  
Input verification (IV): Allows you to verify the content, integrity and origin of an IFlow without revealing additional information. Possible to verify that an IFlow was constructed by specific holders of specific keys that we deem trustworthy. It can also be used to verify that transformations within the IFlow ocurred as it was suposed to.  
Output verification (OV): Verifies attributes about what is happening to the hidden IFlow itself. Allows for properties of an IFlow to be verified without revealing the exact transformation happening within an IFlow.  
Flow governance (FG): It is satisfied if each party with concern about how that information could be misuse, has the ability to prevnet an IFlow to be changed. All parties would need to agree to change the IFlow in that way. Sets rules so that nothing about the integrity about the other four components is compromised.

(1) and (2) guarantees refer to the information of the flow that needs to be hidden; solve the copy problem.  
(3) and (4) guarantees refer to the information of the flow that needs to be revealed in a verifiable way; solve the bundle problem.  
(5) dictates who is allowed to change the flow, including who can modify (1), (2), (3), and (4). It solves the recursive enforcement problem.
