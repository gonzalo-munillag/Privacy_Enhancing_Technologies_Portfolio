# The Impact of Structured Transparency

## Main takeaways and thoughts 

If you solve the copy problem, then data buyers no longer become the sellers competitor.

**PETs are tools that can make data scarce, thus, they are necessary for a future data economy.**

Privacy is not about hiding the identitiy of the person, a corporation might not need to know who that person is exactly, but know about the characteristics of this person so that it can target to him/her content with a larger scale malicious intent. 

DP is not ready to achieve its full potential in an exisiting corporation, available tools are not enough to consider all aspects. Privacy budgeting is the main issue. While you protect with DP your customers, then if another company has the same customers, thus we would be closer to square one with linkage attacks than we would like to.

**Federated Data Network** with privacy budget tracking must be supported by institutions to keep track of the privacy loss of individuals accross organizations, experts do not think that these institutions will be private.

The moment companies are able to analyse data in a privacy-preserving manner efficiently and accurately, then people and governments will start making regulation to make it mainstream. Companies should plan for this.

**Sometimes it is not about making something the most private, the most efficient, the most scalable, but about replicating the IFlows for community wisdom that have already worked organically and apply structured transparency to those which are broken in certain ways.**

Andrew Trask - *Who owns the data? Whoever collected it first.*

Problem of point 5 - you can sell the insights.

The use cases are still far away from being in production in my opinion.

Process:

1. Breakdown an existing IFlow in the context of structured transparency: IP, OP, IV, OV, and FG.
2. Pick the weakest components and think how to solve them. 

## Goals of the lesson, including short summaries 

1. See the impact structured transparency could have on specific groups and industries
2. Get examples of how structured transparency could be used by specific groups or industries

## #1 Academic Research

Motivation: Answer impactful questions that benefit society using data. 
The former three problems review enter into play, slowing down data usage collaboration. With structured transparency, the answer to the question of collaboration **is no longer binary.** The ideal IFlow consists of the researcher getting only the needed data, which could have been processed, while data owners still have the data in their control. 

IP: E.g. the hospital maintains control of the data, by not giving a copy, while researchers can access the data and perform their analysis, e.g. SMC.  
OP: Prevent the reverse of an ML model, with DP.  
(If there is a lack of trust between research institutions)
IV: Prove that the input dataset is the same used in another experiment, useful for reproducibility and benchmarking.  
(If there is some sort of competitions between research institutes)
OV: Prove that a key statistical result was computed by the data owner with the algorithms requested by the researcher.  
FG: Allows data that is sensitive to be accessed by a researcher, by distributing control between stakeholders like a grant funding body, bodies protecting rights of certain vulnerable groups, consortia of research institutions, or data donors.

For research to be influential and impactful, indirectly getting more funding for their workforce, using cutting edge methods like PETs, gives an edge over other institutions as one may access more data than before. 

Answer questions where the data is stored.

## #2 Industry R&D

Motivation: Scout for new technologies and with them create new business models and improve existing products, services, and internal processes.  

IP is a major concern, data or the model might be proprietary. Nonetheless, to use a certain model in production, you need FDA clearance or a CE mark for e.g. in healthcare.  
**The toughest part is to get access to private datasets that validate your algorithm.**

Bob Rogers from bee BeekeeperAI and [UCSF CDHI](https://www.centerfordigitalhealthinnovation.org/), healthcare AI:  
1. A secure infrastructure that is bespoke to each data source.
2. Run the algorithm locally.
3. Protect the data, also in preprocessing, and annotation to answer the question the algorithm is designed to address.  
4. Protect the algorithm, compute the performance of the algorithm on that data.
5. Contracting and other bureaucratic steps.  
Problem: 16 to 30 months to validate an existing ML algorithm, 1.5 to 2.5 million dollars to do the validation across all these sites in order to get the algorithm into the marketplace.
The expected market for healthcare AI is 36 billion dollars, yet only 30 algorithms have been cleared by the FDA, i.e. **there is a need to close the gap as more algorithms will be needed.**  
Techniques: privacy-preserving computing and confidential computing, validating algorithms without moving the data throughout pre-processing, annotation, and computation. The weights are the IP of the product that an organization is using, so the algorithm must also be protected. 

Holger Roth, a senior applied research scientist at NVIDIA.  
Develop DP and Federated Learning (FL) algorithms for healthcare, hospitals, and researchers. E.g. predict oxygen needs when someone comes into the hospital with covid.

## #3 Consumers need structured transparency

Primary motivations: Consumers would like to have better privacy, they do not want to be spied. While this is true, it is missing a big part. PETs are not only about privacy but about creating IFlows that maximize the good in the world. So if you just focus on products that scream privacy, you are missing the point. An interesting approach is to look into the IFlow of **community wisdom**, which has subclasses like community norms, religion, stories, advice, etc. We still make use of them daily. We have created platforms to scale this type of IFlow. However, how are you sure that someone that recommends a product is honest, or a doctor? Or can I trust someone to receive my sensitive data so that that person provides me with a service? There is a need for privacy, anonymity, or comfort. These IFlows need IP and OP and trust with IV and OV, e.g. product reviews are hard to trust. Furthermore, learning from the aggregate is yet more useful in community wisdom, as advice sometimes comes from groups, not from single individuals. 

**Sometimes it is not about making something the most private, the most efficient, the most scalable, but about replicating the IFlows for community wisdom that have already worked organically and apply structured transparency to those which are broken in certain ways.**

This is however only one type of IFlows for consumers.

## #4 News media

Fight against: screen space, fake news, click bait, etc. 

An example of structured transparency is a journalist protecting his/her sources but getting the messsage out. Manual form of IP, OP, as the journalists ensure that you cannot get back to the source by modifying bits of the information, furtheremore, the journalist provides IV by testifying that the source is trustworthy as the journalist discloses that the source belongs to certain organization. Moreover, there is OV as the journalist is subject to be reviewed by an editor or organization, and there is FG as the organization and the journalist and the source can talk about which information is diclosed.  
*So, are htere any parts of an structured transparency IFlow that could be improved?* Pain points, efficiency, etc.

I cannot message someoone anonymously, in current apps, a phone number and a profile is associated with you. How could you however stay anonymous and prove at the same time that you work or belong to certain group?

## #5 ML startups and companies participating in data markets

Motivation: raise money, users, brand, find talent, etc. But the key is, do you have the data? Chicken and an egg problem. You need a strategy to get access to data, which is usually done by consulting with a larger corporation, they then would get the data, and can start developing a product they can later sell.

Data markets are bifurcated: a race to the bottom or never tell a soul kind of industry. E.g. in financial services, some kinds of data are traded so fast that entities pay huge amounts so that the trading happens faster, like buying warehouses in downtown Manhattan so that a company's servers are closer to the central trading infrastructure than their competitors. And other types of data are kept secret as if someone else finds out, then such an entity would be able to trade against you.  
If you sell data, then every customer becomes a competitor, for further selling or direct use. So you either sell the data as fast as possible or never sell it.  
If you are a large corporation, then you have the leverage to keep data secret. If you are a startup, then you sell the data because it is unlikely that you have so many customers already and use cases that you can leverage the data internally.  
No one will give data to a startup unless it is public, or the data provider owns part of the startup so that it does not cannibalize the provider.  
The marketplace for data is broken as it is bifurcated as we have seen above.  

If the copy problem is solved, then the original data curator can charge money for any potential derivative use. Thus, the prices would raise prices for data that is currently being sold as fast as possible, whose value drops to almost nothing as it can be copied. All of the sudden, the data would become scarce. Likewise, for the corporations that keep data secret, the data can be now monetized without losing it. And your customers would not instantly become a competitor. This prevents a monopoly, as before, only that one company used the secret data.

The solution utilizes the 5 components, **Federated Data Network**. Instead of selling data, you sell access to data (The opportunity of someone training an ML model on your data). One may also use federated learning.

A true healthy privacy-preserving data market would be a huge benefit to startups, as they can finally have access to data, and thus, bring more innovation into society. 

Today companies have the data, but in the future, individuals would not like to miss the opportunity to extract revenue from their own data, there would be no incentive to do otherwise. An economic incentive subtracts the need of having regulation to impose data protection "People owning and having agency over their data".

## #6 Consumers Need Structured Transparency Institutions 

There is a missing institution within a data marketplace, which would play a role in protecting consumers from harm while facilitating a healthy data marketplace.

**No individual holder of data is in a good position to ensure that the people behind their dataset does not get hurt, because they do not know where else an individual's data might also be hosted, leading to a potential linkage attack.**

Economic perspective: Do not sell data, but insights. However, if too many insights are out, eventually you can recreate a dataset and compete with the original data owner. With DP, you can put a probability to the likelihood of someone reconstructing your dataset. With a budget, you can keep track of it. **Epsilon thus becomes the scarce resource**, the lower the budget left, the price for your data increases. When you sell insights, you must include how much privacy budget you are selling in the process from what is left.  
Piece of privacy infrastructure that is not mature: **Automatic privacy budgeting for remote data science.** This may be the tipping point of federated data networks, as this can let networks run themselves, automatically managing their privacy budget. 

Aaron Roth - Tooling around DP is limited. We are not at a place where you can easily use DP in-house. There are some open-source algorithms, but, what we do not have much of, is an end-to-end infrastructure to use DP. Privacy does not come for free, we must see privacy as a scarce resource, we must use epsilon to keep track of it, but there is nothing out there that can make it happen yet, perhaps between Harvard and Microsoft. Once this is solved, then DP can be widely adopted and used by companies in-house without expertise. 

Aaron Roth - Privacy budgets need to be personalized, but how do you keep track of all the institutions that have your data and thus do appropriate budget accounting?
It sounds like sci-fi at the moment.

Cynthia Dwork - Going larger is better. There is nothing other than politics for federating and maintaining global privacy controls in e.g. hospitals. She has no hopes that that happens in the commercial environment, even in hospitals too.

This leaves public institutions for the task. 

## #7 Intelligence, Stats Services & Regulators Need Structured Transparency

What information is appropriate for a government to collect from its citizens?  
The stats from governments are very useful, but there could be mass surveillance. 

Cynthia Dwork - If governments do not use techniques to guarantee privacy in their census, "It would be their last census.".

Database queries: When a government intelligence asks a company to reveal a piece of information about a user but the government does not want to reveal which user it is. Or, two government agencies collaborate but do not want to share their respective citizens' information. To do the formerly, in a way that the company does not find out who the person is, the agency would interview or request the data of thousands of people, which has privacy implications and inefficiencies. You could, however, could make a HE query so that the company does not find out who it was. 

Pascal Pallier - You can use HE for detecting money laundering. You could verify that a passport number is included in an organization with HE, otherwise, you could only reveal the number in case you have evidence of malicious behavior of the person, but without checking the activity of such passport number in the database, there is no proof of that behavior, it is a chicken and an egg problem sometimes. 

Cynthia Dwork - Privacy loss analogy to radiation. Database reconstruction theorem in 2003 (Nissim), overly accurate estimates of too many statistics will divulge the entire database, no matter how one blunts the attack by introducing inaccuracies. This is a hard limit on the number of measurements before privacy is destroyed. The limit is tide to the accuracy, how many data points can you safely take before the radiation dosage of each data point accrues to a dangerous amount. DP is programmable and one can control these dosages.

This global perspective might be more useful for making a regulation, holistic privacy protection against cumulative privacy breaches along with someone's life, instead of regulation focusing only on individual harms of the particular data release. - I disagree to some extent. If you nickel and dime each event, then overall, you protect all your events.

## #8 The Next Steps for Structured Transparency 

*When are these changes going to happen?*  
Some have already happened, e.g. FL is used in your phone.

*What are the next steps?*
Ilya Mironov, FacebookAI - SQL must be enhanced to be privacy-preserving, which is seriously tackled by multiple research teams for DP. 

Focusing on proprietary SW is a short term strategy for startups as they will ultimately be replaced by open-source SW. Like it happened with ML. The long term defensible strategy is to become gatekeepers for the world's information within the forthcoming networks of data. While you only need a few packages for all of us to use, information flows are the things that companies and communities will need more of. It will not be about hoarding data either if that is not what the original data owners want. It is about creating and maintaining information flows so that people and other organizations achieve their goals in the best possible way. 

Any novel technique that is not yet mature, it is an opportunity for research, entrepreneurs, etc. 

#### Interesting links and other things

Cameras which sign each picture or video with cryptographic signatures, to prevent deep fakes.

Pascal Pallier - The biggest problem is to access the data.

Aaron Roth - It could be that, by adding more privacy, then you get more data, and thus, you end up with better accuracy.

Andrew Trask - "Data about people, starts with people. So the most profitable thing to do is to never let go of the data and let the market come to them".

Aaron Roth - DP provides a means by which people can quantify their cost for privacy without understanding in datail what is going to happen with their data downstream. 
